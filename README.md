SQLite Database for HackRF Drone Detection System

📁 Database Setup Script
Create setup_database.sql:

sql
-- =====================================================
-- HackRF Drone Detection System - Database Schema
-- Version: 2.0.0
-- Date: 2024-01-15
-- =====================================================

-- Drop existing tables if they exist (for clean install)
DROP TABLE IF EXISTS detections;
DROP TABLE IF EXISTS alerts;
DROP TABLE IF EXISTS system_metrics;
DROP TABLE IF EXISTS config;
DROP TABLE IF EXISTS drone_signatures;
DROP TABLE IF EXISTS rf_analysis;
DROP TABLE IF EXISTS sensor_health;
DROP TABLE IF EXISTS geolocation;
DROP TABLE IF EXISTS threat_intel;

-- =====================================================
-- 1. DETECTIONS TABLE - Main detection records
-- =====================================================

CREATE TABLE detections (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    drone_type TEXT NOT NULL,
    drone_model TEXT,
    confidence REAL DEFAULT 0.0,
    threat_level TEXT DEFAULT 'LOW',
    
    -- Position data
    position_x REAL DEFAULT 0.0,
    position_y REAL DEFAULT 0.0,
    position_z REAL DEFAULT 0.0,
    position_accuracy REAL DEFAULT 0.0,
    
    -- Velocity data
    velocity_x REAL DEFAULT 0.0,
    velocity_y REAL DEFAULT 0.0,
    velocity_z REAL DEFAULT 0.0,
    
    -- RF Data
    frequency_hz INTEGER DEFAULT 0,
    signal_strength_dbm REAL DEFAULT -100.0,
    snr_db REAL DEFAULT 0.0,
    bandwidth_hz INTEGER DEFAULT 0,
    modulation TEXT,
    
    -- Visual data (from camera)
    visual_confidence REAL DEFAULT 0.0,
    visual_detection_method TEXT,
    
    -- Sensor fusion
    sensor_count INTEGER DEFAULT 0,
    fusion_method TEXT DEFAULT 'weighted_average',
    
    -- Additional metadata
    detection_method TEXT DEFAULT 'rf_only',
    processing_time_ms REAL DEFAULT 0.0,
    operator_notes TEXT,
    
    -- Indexing fields
    event_number INTEGER,
    is_confirmed BOOLEAN DEFAULT 0
);

-- =====================================================
-- 2. ALERTS TABLE - Security alerts
-- =====================================================

CREATE TABLE alerts (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    alert_type TEXT NOT NULL,
    severity TEXT DEFAULT 'MEDIUM',  -- CRITICAL, HIGH, MEDIUM, LOW, INFO
    message TEXT NOT NULL,
    detection_id INTEGER,
    drone_type TEXT,
    threat_level TEXT,
    position_x REAL,
    position_y REAL,
    position_z REAL,
    action_taken TEXT,
    acknowledged BOOLEAN DEFAULT 0,
    acknowledged_by TEXT,
    acknowledged_at DATETIME,
    resolved BOOLEAN DEFAULT 0,
    resolved_at DATETIME,
    resolution_notes TEXT,
    FOREIGN KEY (detection_id) REFERENCES detections(id)
);

-- =====================================================
-- 3. SYSTEM_METRICS TABLE - Performance monitoring
-- =====================================================

CREATE TABLE system_metrics (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    
    -- Detection metrics
    total_detections INTEGER DEFAULT 0,
    true_positives INTEGER DEFAULT 0,
    false_positives INTEGER DEFAULT 0,
    false_negatives INTEGER DEFAULT 0,
    
    -- Performance metrics
    cpu_usage REAL DEFAULT 0.0,
    memory_usage_mb REAL DEFAULT 0.0,
    avg_processing_time_ms REAL DEFAULT 0.0,
    max_processing_time_ms REAL DEFAULT 0.0,
    detection_rate REAL DEFAULT 0.0,  -- Detections per minute
    
    -- Sensor metrics
    rf_sensor_uptime REAL DEFAULT 0.0,
    lidar_sensor_uptime REAL DEFAULT 0.0,
    camera_sensor_uptime REAL DEFAULT 0.0,
    radar_sensor_uptime REAL DEFAULT 0.0,
    
    -- RF metrics
    noise_floor_dbm REAL DEFAULT -100.0,
    active_frequency_hz INTEGER,
    current_band TEXT,
    
    -- System info
    system_uptime REAL DEFAULT 0.0,
    temperature_c REAL DEFAULT 0.0
);

-- =====================================================
-- 4. CONFIG TABLE - System configuration
-- =====================================================

CREATE TABLE config (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    config_key TEXT UNIQUE NOT NULL,
    config_value TEXT NOT NULL,
    config_type TEXT DEFAULT 'string',
    description TEXT,
    updated_at DATETIME DEFAULT CURRENT_TIMESTAMP,
    updated_by TEXT DEFAULT 'system'
);

-- =====================================================
-- 5. DRONE_SIGNATURES TABLE - Known drone RF signatures
-- =====================================================

CREATE TABLE drone_signatures (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    drone_name TEXT UNIQUE NOT NULL,
    manufacturer TEXT,
    model TEXT,
    
    -- Frequency bands
    control_freq_min INTEGER,
    control_freq_max INTEGER,
    video_freq_min INTEGER,
    video_freq_max INTEGER,
    telemetry_freq_min INTEGER,
    telemetry_freq_max INTEGER,
    
    -- Signal characteristics
    modulation_type TEXT,
    bandwidth_hz INTEGER,
    hopping_pattern TEXT,
    channel_count INTEGER DEFAULT 0,
    
    -- Physical characteristics
    size_category TEXT,  -- small, medium, large
    max_speed_kmh REAL,
    max_altitude_m REAL,
    typical_range_m REAL,
    
    -- Threat assessment
    base_threat_score INTEGER DEFAULT 0,
    is_military BOOLEAN DEFAULT 0,
    detection_difficulty TEXT,  -- easy, medium, hard
    
    -- Additional data
    notes TEXT,
    active BOOLEAN DEFAULT 1
);

-- =====================================================
-- 6. RF_ANALYSIS TABLE - Detailed RF spectrum analysis
-- =====================================================

CREATE TABLE rf_analysis (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    detection_id INTEGER,
    
    -- Spectrum data
    fft_data BLOB,  -- Binary FFT data
    peak_frequency_hz INTEGER,
    peak_power_dbm REAL,
    noise_floor_dbm REAL,
    signal_to_noise_ratio REAL,
    
    -- Signal features
    bandwidth_hz INTEGER,
    occupied_bandwidth_hz INTEGER,
    spectral_centroid REAL,
    spectral_rolloff REAL,
    spectral_spread REAL,
    peak_to_average_ratio REAL,
    
    -- Modulation detection
    detected_modulation TEXT,
    modulation_confidence REAL,
    symbol_rate REAL,
    
    -- Drone identification
    matched_drone_id INTEGER,
    match_confidence REAL,
    
    analysis_duration_ms REAL,
    FOREIGN KEY (detection_id) REFERENCES detections(id),
    FOREIGN KEY (matched_drone_id) REFERENCES drone_signatures(id)
);

-- =====================================================
-- 7. SENSOR_HEALTH TABLE - Sensor status monitoring
-- =====================================================

CREATE TABLE sensor_health (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    sensor_name TEXT NOT NULL,  -- rf, lidar, camera, radar
    sensor_status TEXT,  -- OK, WARNING, ERROR, OFFLINE
    
    -- Performance metrics
    uptime_seconds REAL,
    samples_rate_hz REAL,
    error_rate REAL,
    buffer_usage_percent REAL,
    last_heartbeat DATETIME,
    
    -- Hardware metrics
    temperature_c REAL,
    voltage_v REAL,
    current_ma REAL,
    
    -- Calibration data
    calibration_date DATETIME,
    calibration_data TEXT,
    
    is_active BOOLEAN DEFAULT 1
);

-- =====================================================
-- 8. GEOLOCATION TABLE - GPS positioning data
-- =====================================================

CREATE TABLE geolocation (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    detection_id INTEGER,
    
    -- System position
    system_latitude REAL NOT NULL,
    system_longitude REAL NOT NULL,
    system_altitude_m REAL,
    system_accuracy_m REAL,
    
    -- Detected drone position (relative)
    drone_bearing_deg REAL,
    drone_distance_m REAL,
    drone_altitude_m REAL,
    drone_azimuth_deg REAL,
    
    -- GPS quality
    gps_fix_quality INTEGER,  -- 0=invalid, 1=GPS, 2=DGPS, 3=RTK
    gps_satellites INTEGER,
    gps_hdop REAL,
    
    -- Timestamps
    gps_timestamp DATETIME,
    
    FOREIGN KEY (detection_id) REFERENCES detections(id)
);

-- =====================================================
-- 9. THREAT_INTEL TABLE - External threat intelligence
-- =====================================================

CREATE TABLE threat_intel (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    source TEXT NOT NULL,  -- local, api, manual
    drone_type TEXT,
    threat_level TEXT,
    confidence REAL DEFAULT 0.5,
    
    -- Intelligence data
    location_lat REAL,
    location_lon REAL,
    location_radius_m REAL,
    incident_description TEXT,
    
    -- Validity
    valid_from DATETIME,
    valid_to DATETIME,
    is_active BOOLEAN DEFAULT 1,
    notes TEXT
);

-- =====================================================
-- CREATE INDEXES FOR PERFORMANCE
-- =====================================================

-- Detections indexes
CREATE INDEX idx_detections_timestamp ON detections(timestamp);
CREATE INDEX idx_detections_drone_type ON detections(drone_type);
CREATE INDEX idx_detections_threat_level ON detections(threat_level);
CREATE INDEX idx_detections_confidence ON detections(confidence);
CREATE INDEX idx_detections_frequency ON detections(frequency_hz);

-- Alerts indexes
CREATE INDEX idx_alerts_timestamp ON alerts(timestamp);
CREATE INDEX idx_alerts_severity ON alerts(severity);
CREATE INDEX idx_alerts_acknowledged ON alerts(acknowledged);
CREATE INDEX idx_alerts_resolved ON alerts(resolved);

-- System metrics indexes
CREATE INDEX idx_metrics_timestamp ON system_metrics(timestamp);

-- RF analysis indexes
CREATE INDEX idx_rf_analysis_timestamp ON rf_analysis(timestamp);
CREATE INDEX idx_rf_analysis_modulation ON rf_analysis(detected_modulation);

-- Sensor health indexes
CREATE INDEX idx_sensor_health_name ON sensor_health(sensor_name);
CREATE INDEX idx_sensor_health_timestamp ON sensor_health(timestamp);

-- Geolocation indexes
CREATE INDEX idx_geolocation_timestamp ON geolocation(timestamp);

-- Threat intel indexes
CREATE INDEX idx_threat_intel_timestamp ON threat_intel(timestamp);
CREATE INDEX idx_threat_intel_drone_type ON threat_intel(drone_type);
CREATE INDEX idx_threat_intel_active ON threat_intel(is_active);

-- =====================================================
-- INSERT DEFAULT CONFIGURATION
-- =====================================================

INSERT OR IGNORE INTO config (config_key, config_value, config_type, description) VALUES
    ('system_name', 'HackRF Drone Detection System', 'string', 'System identifier'),
    ('system_version', '2.0.0', 'string', 'Software version'),
    ('detection_threshold', '0.625', 'float', 'Minimum confidence for detection'),
    ('alert_threshold', '0.75', 'float', 'Minimum confidence for alerts'),
    ('scan_interval_ms', '1000', 'integer', 'Scan interval in milliseconds'),
    ('frequency_bands', '2.4GHz,5.8GHz,915MHz,433MHz', 'string', 'Frequency bands to scan'),
    ('active_band', '2.4GHz', 'string', 'Currently active band'),
    ('rf_gain_lna', '32', 'integer', 'LNA gain setting (0-40)'),
    ('rf_gain_vga', '20', 'integer', 'VGA gain setting (0-62)'),
    ('sample_rate_hz', '20000000', 'integer', 'Sample rate in Hz'),
    ('fft_size', '4096', 'integer', 'FFT size'),
    ('websocket_port', '8082', 'integer', 'WebSocket server port'),
    ('webui_port', '8080', 'integer', 'Web UI HTTP port'),
    ('database_retention_days', '30', 'integer', 'Keep records for X days'),
    ('enable_sensor_fusion', '1', 'boolean', 'Enable sensor fusion'),
    ('enable_classification', '1', 'boolean', 'Enable drone classification'),
    ('enable_gps', '0', 'boolean', 'Enable GPS geolocation'),
    ('debug_mode', '0', 'boolean', 'Enable debug logging');

-- =====================================================
-- INSERT KNOWN DRONE SIGNATURES
-- =====================================================

INSERT OR IGNORE INTO drone_signatures (
    drone_name, manufacturer, model,
    control_freq_min, control_freq_max,
    video_freq_min, video_freq_max,
    modulation_type, bandwidth_hz, channel_count,
    size_category, max_speed_kmh, max_altitude_m, typical_range_m,
    base_threat_score, is_military, detection_difficulty
) VALUES
    -- DJI Drones
    ('DJI Phantom 4', 'DJI', 'Phantom 4',
     2400000000, 2483500000, 5725000000, 5850000000,
     'OFDM', 40000000, 32, 'medium', 72, 120, 2000, 15, 0, 'easy'),
    
    ('DJI Mavic 3', 'DJI', 'Mavic 3',
     2400000000, 2483500000, 5725000000, 5850000000,
     'OFDM', 80000000, 64, 'small', 75, 100, 1500, 10, 0, 'easy'),
    
    ('DJI Avata', 'DJI', 'Avata',
     2400000000, 2483500000, 5725000000, 5850000000,
     'OFDM', 40000000, 48, 'small', 80, 80, 1000, 10, 0, 'easy'),
    
    ('DJI Inspire 3', 'DJI', 'Inspire 3',
     2400000000, 2483500000, 5725000000, 5850000000,
     'OFDM', 80000000, 64, 'medium', 90, 200, 3000, 25, 0, 'medium'),
    
    -- FPV/DIY Drones
    ('ExpressLRS', 'ExpressLRS', 'Generic',
     2400000000, 2483500000, 0, 0,
     'FHSS', 1000000, 83, 'small', 120, 80, 1500, 30, 0, 'hard'),
    
    ('TBS Crossfire', 'TBS', 'Crossfire',
     868000000, 915000000, 0, 0,
     'FHSS', 4000000, 16, 'small', 150, 100, 2000, 40, 0, 'medium'),
    
    ('FrSky D16', 'FrSky', 'D16',
     2400000000, 2483500000, 0, 0,
     'FHSS', 1500000, 16, 'small', 100, 80, 1200, 25, 0, 'easy'),
    
    -- Analog FPV
    ('Analog FPV VTX', 'Various', 'Analog',
     0, 0, 5725000000, 5850000000,
     'ANALOG_FM', 25000000, 8, 'small', 120, 80, 1000, 35, 0, 'medium'),
    
    -- Commercial/Industrial
    ('Matrice 300', 'DJI', 'Matrice 300',
     2400000000, 2483500000, 5725000000, 5850000000,
     'OFDM', 40000000, 32, 'large', 80, 200, 5000, 50, 0, 'medium'),
    
    ('eBee X', 'senseFly', 'eBee X',
     868000000, 928000000, 0, 0,
     'QPSK', 2000000, 8, 'medium', 110, 500, 5000, 40, 0, 'hard'),
    
    -- Military/Grade
    ('Military Drone', 'Classified', 'Generic',
     1200000000, 1300000000, 3400000000, 3600000000,
     'SPREAD_SPECTRUM', 120000000, 128, 'large', 150, 500, 10000, 100, 1, 'hard'),
    
    ('Switchblade 300', 'AeroVironment', 'Switchblade',
     1200000000, 1300000000, 0, 0,
     'FHSS', 20000000, 64, 'small', 160, 500, 10000, 95, 1, 'hard');

-- =====================================================
-- INSERT SAMPLE DATA (For testing/demo purposes)
-- =====================================================

-- Sample detections (last 24 hours)
INSERT INTO detections (
    timestamp, drone_type, confidence, threat_level,
    position_x, position_y, position_z,
    frequency_hz, signal_strength_dbm, snr_db, bandwidth_hz, modulation,
    sensor_count, detection_method, event_number, is_confirmed
) VALUES
    (datetime('now', '-2 hours'), 'DJI Mavic 3', 0.85, 'HIGH',
     125.5, -45.2, 35.8, 2445000000, -65.3, 28.5, 40200000, 'OFDM', 3, 'multi-sensor', 1, 1),
    
    (datetime('now', '-4 hours'), 'ExpressLRS', 0.72, 'MEDIUM',
     85.3, -22.1, 45.2, 2420000000, -72.1, 22.1, 1000000, 'FHSS', 2, 'rf_only', 2, 1),
    
    (datetime('now', '-6 hours'), 'DJI Phantom 4', 0.91, 'HIGH',
     200.1, -85.6, 52.3, 2450000000, -58.4, 32.5, 38000000, 'OFDM', 4, 'multi-sensor', 3, 1),
    
    (datetime('now', '-8 hours'), 'Analog FPV VTX', 0.63, 'MEDIUM',
     15.2, -12.8, 22.1, 5800000000, -75.2, 18.5, 25000000, 'FM', 1, 'rf_only', 4, 0),
    
    (datetime('now', '-10 hours'), 'Military Drone', 0.88, 'CRITICAL',
     450.5, -220.3, 120.5, 1250000000, -62.1, 30.2, 115000000, 'DSSS', 3, 'multi-sensor', 5, 1),
    
    (datetime('now', '-12 hours'), 'TBS Crossfire', 0.58, 'LOW',
     75.8, -35.6, 15.2, 915000000, -78.5, 15.5, 3800000, 'FHSS', 2, 'rf_only', 6, 0),
    
    (datetime('now', '-14 hours'), 'DJI Avata', 0.79, 'MEDIUM',
     150.2, -65.8, 28.5, 2440000000, -68.2, 25.5, 41000000, 'OFDM', 3, 'multi-sensor', 7, 1);

-- Sample alerts
INSERT INTO alerts (
    timestamp, alert_type, severity, message, detection_id,
    drone_type, threat_level, position_x, position_y, position_z,
    acknowledged, resolved
) VALUES
    (datetime('now', '-2 hours'), 'DRONE_DETECTED', 'HIGH', 
     'High confidence detection of DJI Mavic 3 at 125.5, -45.2, 35.8',
     1, 'DJI Mavic 3', 'HIGH', 125.5, -45.2, 35.8, 1, 1),
    
    (datetime('now', '-10 hours'), 'DRONE_DETECTED', 'CRITICAL',
     'CRITICAL: Military Drone detected in restricted airspace!',
     5, 'Military Drone', 'CRITICAL', 450.5, -220.3, 120.5, 0, 0),
    
    (datetime('now', '-6 hours'), 'DRONE_DETECTED', 'HIGH',
     'DJI Phantom 4 detected within 200m radius',
     3, 'DJI Phantom 4', 'HIGH', 200.1, -85.6, 52.3, 1, 1);

-- Sample system metrics (hourly for last 24 hours)
INSERT INTO system_metrics (
    timestamp, total_detections, true_positives, false_positives,
    cpu_usage, memory_usage_mb, avg_processing_time_ms,
    rf_sensor_uptime, noise_floor_dbm, current_band
)
SELECT 
    datetime('now', '-' || value || ' hours'),
    42 + (value % 23),
    38 + (value % 18),
    4 + (value % 5),
    25.5 + (value % 15),
    145.2 + (value % 20),
    23.5 + (value % 10),
    3600.0 - (value * 60),
    -95.0 + (value % 10),
    CASE (value % 4)
        WHEN 0 THEN '2.4 GHz'
        WHEN 1 THEN '5.8 GHz'
        WHEN 2 THEN '915 MHz'
        ELSE '433 MHz'
    END
FROM (SELECT 0 as value UNION SELECT 1 UNION SELECT 2 UNION SELECT 3 UNION SELECT 4 
      UNION SELECT 5 UNION SELECT 6 UNION SELECT 7 UNION SELECT 8 UNION SELECT 9
      UNION SELECT 10 UNION SELECT 11 UNION SELECT 12 UNION SELECT 13 UNION SELECT 14
      UNION SELECT 15 UNION SELECT 16 UNION SELECT 17 UNION SELECT 18 UNION SELECT 19
      UNION SELECT 20 UNION SELECT 21 UNION SELECT 22 UNION SELECT 23);

-- Sample RF analysis data
INSERT INTO rf_analysis (
    timestamp, detection_id, peak_frequency_hz, peak_power_dbm,
    noise_floor_dbm, signal_to_noise_ratio, bandwidth_hz,
    detected_modulation, modulation_confidence, match_confidence
)
SELECT 
    timestamp, id, frequency_hz, signal_strength_dbm,
    signal_strength_dbm - snr_db, snr_db, bandwidth_hz,
    modulation, confidence, confidence
FROM detections
WHERE modulation IS NOT NULL;

-- Sample sensor health data
INSERT INTO sensor_health (sensor_name, sensor_status, uptime_seconds, is_active) VALUES
    ('rf', 'OK', 86400, 1),
    ('lidar', 'OK', 86350, 1),
    ('camera', 'WARNING', 86200, 1),
    ('radar', 'OK', 86400, 1);

-- =====================================================
-- CREATE VIEWS FOR COMMON QUERIES
-- =====================================================

-- Recent high-threat detections view
CREATE VIEW IF NOT EXISTS recent_threats AS
SELECT 
    timestamp,
    drone_type,
    confidence,
    threat_level,
    position_x,
    position_y,
    position_z
FROM detections
WHERE threat_level IN ('CRITICAL', 'HIGH')
    AND timestamp > datetime('now', '-1 hour')
ORDER BY timestamp DESC;

-- Detection statistics by hour
CREATE VIEW IF NOT EXISTS hourly_stats AS
SELECT 
    strftime('%Y-%m-%d %H:00:00', timestamp) as hour,
    COUNT(*) as detection_count,
    AVG(confidence) as avg_confidence,
    SUM(CASE WHEN threat_level = 'CRITICAL' THEN 1 ELSE 0 END) as critical_count,
    SUM(CASE WHEN threat_level = 'HIGH' THEN 1 ELSE 0 END) as high_count
FROM detections
WHERE timestamp > datetime('now', '-24 hours')
GROUP BY hour
ORDER BY hour DESC;

-- Active threats view
CREATE VIEW IF NOT EXISTS active_threats AS
SELECT 
    d.timestamp,
    d.drone_type,
    d.confidence,
    d.threat_level,
    d.position_x,
    d.position_y,
    d.position_z,
    a.acknowledged,
    a.resolved
FROM detections d
LEFT JOIN alerts a ON d.id = a.detection_id
WHERE d.threat_level IN ('CRITICAL', 'HIGH', 'MEDIUM')
    AND d.timestamp > datetime('now', '-30 minutes')
ORDER BY d.confidence DESC;

-- =====================================================
-- CREATE TRIGGERS
-- =====================================================

-- Auto-update system uptime when metrics are inserted
CREATE TRIGGER update_system_uptime
AFTER INSERT ON system_metrics
BEGIN
    UPDATE system_metrics
    SET system_uptime = (
        SELECT (julianday('now') - julianday(min(timestamp))) * 86400
        FROM system_metrics
    )
    WHERE id = NEW.id;
END;

-- Auto-create alert when high threat detection is recorded
CREATE TRIGGER auto_alert_on_critical
AFTER INSERT ON detections
WHEN NEW.threat_level IN ('CRITICAL', 'HIGH')
BEGIN
    INSERT INTO alerts (
        timestamp, alert_type, severity, message, detection_id,
        drone_type, threat_level, position_x, position_y, position_z
    ) VALUES (
        NEW.timestamp, 'DRONE_DETECTED', NEW.threat_level,
        CASE NEW.threat_level
            WHEN 'CRITICAL' THEN 'CRITICAL: ' || NEW.drone_type || ' detected in restricted area!'
            WHEN 'HIGH' THEN 'High: ' || NEW.drone_type || ' detected within perimeter'
        END,
        NEW.id, NEW.drone_type, NEW.threat_level,
        NEW.position_x, NEW.position_y, NEW.position_z
    );
END;

-- =====================================================
-- MAINTENANCE FUNCTIONS (as comments)
-- =====================================================

-- Clean old records (run daily)
-- DELETE FROM detections WHERE timestamp < datetime('now', '-' || (SELECT config_value FROM config WHERE config_key='database_retention_days') || ' days');

-- Vacuum database to reclaim space
-- VACUUM;

-- Analyze tables for query optimization
-- ANALYZE;

-- =====================================================
-- QUERY EXAMPLES
-- =====================================================

-- Example 1: Get detection count by drone type
-- SELECT drone_type, COUNT(*) as count 
-- FROM detections 
-- WHERE timestamp > datetime('now', '-7 days') 
-- GROUP BY drone_type 
-- ORDER BY count DESC;

-- Example 2: Average confidence by threat level
-- SELECT threat_level, AVG(confidence) as avg_conf 
-- FROM detections 
-- GROUP BY threat_level;

-- Example 3: Unacknowledged critical alerts
-- SELECT * FROM alerts 
-- WHERE severity = 'CRITICAL' 
--     AND acknowledged = 0 
--     AND resolved = 0;

-- Example 4: System performance trend
-- SELECT timestamp, cpu_usage, memory_usage_mb, avg_processing_time_ms 
-- FROM system_metrics 
-- WHERE timestamp > datetime('now', '-1 hour') 
-- ORDER BY timestamp;

-- Example 5: Most active detection times
-- SELECT strftime('%H', timestamp) as hour, COUNT(*) as detections
-- FROM detections
-- GROUP BY hour
-- ORDER BY detections DESC
-- LIMIT 5;

-- =====================================================
-- DATABASE MAINTENANCE NOTES
-- =====================================================

-- Backup database:
-- sqlite3 drone_detections.db ".backup drone_detections_backup.db"

-- Export to CSV:
-- sqlite3 drone_detections.db -header -csv "SELECT * FROM detections" > detections.csv

-- Check database integrity:
-- sqlite3 drone_detections.db "PRAGMA integrity_check;"

-- =====================================================
-- END OF SCHEMA
-- =====================================================
🚀 How to Create the Database
Method 1: Using SQLite3 Command Line
bash
# Create empty database and run schema
sqlite3 drone_detections.db < setup_database.sql

# Verify tables
sqlite3 drone_detections.db ".tables"

# Check schema
sqlite3 drone_detections.db ".schema detections"

# Run test query
sqlite3 drone_detections.db "SELECT COUNT(*) FROM detections;"
Method 2: Using Python
python
import sqlite3

# Read and execute schema
with open('setup_database.sql', 'r') as f:
    schema = f.read()

conn = sqlite3.connect('drone_detections.db')
conn.executescript(schema)
conn.close()

print("Database created successfully!")
Method 3: Within C Code
c
#include <sqlite3.h>

void initialize_database() {
    sqlite3 *db;
    char *err_msg = 0;
    
    sqlite3_open("drone_detections.db", &db);
    
    const char* sql = 
        "CREATE TABLE IF NOT EXISTS detections ("
        "id INTEGER PRIMARY KEY AUTOINCREMENT,"
        "timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,"
        "drone_type TEXT NOT NULL,"
        "confidence REAL DEFAULT 0.0,"
        "threat_level TEXT DEFAULT 'LOW'"
        ");";
    
    sqlite3_exec(db, sql, 0, 0, &err_msg);
    sqlite3_close(db);
}
📊 Database Statistics (After Setup)
text
Table: detections          ~7 rows (sample data)
Table: alerts              ~3 rows
Table: system_metrics      ~24 rows
Table: config              ~19 rows
Table: drone_signatures    ~13 rows
Table: rf_analysis         ~7 rows
Table: sensor_health       ~4 rows
Total size: ~40-60 KB (empty), ~200 KB (with sample data)
🔍 Useful SQL Queries
sql
-- Quick status check
SELECT 
    (SELECT COUNT(*) FROM detections) as total_detections,
    (SELECT COUNT(*) FROM alerts WHERE resolved=0) as active_alerts,
    (SELECT COUNT(*) FROM drone_signatures WHERE active=1) as known_drones;

-- Last 10 detections
SELECT timestamp, drone_type, confidence, threat_level 
FROM detections 
ORDER BY timestamp DESC 
LIMIT 10;

-- Detections by hour today
SELECT strftime('%H', timestamp) as hour, COUNT(*) as count
FROM detections 
WHERE date(timestamp) = date('now')
GROUP BY hour;

-- Sensor health summary
SELECT sensor_name, sensor_status, uptime_seconds/3600.0 as uptime_hours
FROM sensor_health;
📁 File Location
Place the database file in:

text
hackrf_drone_detector/
├── data/
│   └── drone_detections.db    ← Create this file
├── docs/
├── web_ui/
└── backend.c
The backend will automatically create the database if it doesn't exist using the schema from the code. This SQL file is for reference and manual setup.
