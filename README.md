# HackRF Drone Detection System - API Reference

**Version:** 2.0.0  
**Base URL:** `ws://localhost:8082` (WebSocket)  
**Protocol:** WebSocket (JSON messages)

---

## 📡 WebSocket API

The system uses WebSocket for real-time bidirectional communication. Connect to `ws://localhost:8082` to start receiving data.

### Connection

```javascript
const ws = new WebSocket('ws://localhost:8082');

ws.onopen = () => {
    console.log('Connected to drone detection system');
    ws.send('start'); // Start scanning
};

ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('Received:', data);
};
📨 Message Types
1. Server → Client Messages
1.1 Detection Event
Type: detection

Sent when a drone is detected.

json
{
    "type": "detection",
    "data": {
        "timestamp": "2024-01-15 14:30:22",
        "drone_type": "DJI Mavic",
        "confidence": 0.85,
        "threat_level": "HIGH",
        "position": [45.2, -120.1, 50.3],
        "velocity": [12.5, -3.2, 0],
        "bandwidth": 40200000,
        "snr": 28.5,
        "signal_strength": -65.3,
        "modulation": "OFDM",
        "frequency": 2445000000,
        "sensor_count": 3
    }
}
Fields:

Field	Type	Unit	Description
timestamp	string	ISO datetime	Detection time
drone_type	string	-	Identified drone model
confidence	float	0-1	Detection confidence
threat_level	string	-	CRITICAL/HIGH/MEDIUM/LOW/NEGLIGIBLE
position[3]	array	meters	[x, y, z] coordinates
velocity[3]	array	m/s	[vx, vy, vz] velocity
bandwidth	integer	Hz	Signal bandwidth
snr	float	dB	Signal-to-noise ratio
signal_strength	float	dBm	Received signal power
modulation	string	-	OFDM/FHSS/DSSS/ANALOG_FM
frequency	integer	Hz	Center frequency
sensor_count	integer	-	Number of sensors contributing
1.2 Metrics Update
Type: metrics

System performance metrics sent periodically.

json
{
    "type": "metrics",
    "data": {
        "total_detections": 47,
        "true_positives": 42,
        "false_positives": 5,
        "avg_processing_time": 23.5,
        "sensor_uptime": [3600.5, 3598.2, 3600.0, 3595.8],
        "system_uptime": 3602.5,
        "active_sensors": 4,
        "cpu_usage": 32.5,
        "memory_usage": 156.8,
        "detection_rate": 0.35
    }
}
Fields:

Field	Type	Unit	Description
total_detections	integer	-	Total detections since start
true_positives	integer	-	Correct detections
false_positives	integer	-	False alarms
avg_processing_time	float	ms	Average processing latency
sensor_uptime[4]	array	seconds	Uptime per sensor [RF, LIDAR, Camera, Radar]
system_uptime	float	seconds	System runtime
active_sensors	integer	-	Number of active sensors
cpu_usage	float	%	CPU utilization
memory_usage	float	MB	RAM usage
detection_rate	float	detections/sec	Current detection frequency
1.3 Alert
Type: alert

Critical or high-threat detections trigger alerts.

json
{
    "type": "alert",
    "data": {
        "message": "CRITICAL: Military Drone detected within 100m",
        "drone_type": "Military Drone",
        "threat_level": "CRITICAL",
        "timestamp": "2024-01-15 14:30:22",
        "position": [120.5, -45.2, 35.8],
        "velocity": [25.3, -5.1, 2.0],
        "recommended_action": "EVACUATE_AREA"
    }
}
Threat Levels & Recommended Actions:

Level	Score	Color	Recommended Action
CRITICAL	80-100	🔴 Red	EVACUATE_AREA, NOTIFY_AUTHORITIES
HIGH	60-79	🟠 Orange	INCREASE_ALERT, PREPARE_COUNTERMEASURES
MEDIUM	40-59	🟡 Yellow	MONITOR_CLOSELY, LOG_DETECTION
LOW	20-39	🔵 Blue	ROUTINE_MONITORING
NEGLIGIBLE	0-19	⚪ Gray	IGNORE
1.4 Plot Data
Type: plot_data

Confidence trend data for visualization.

json
{
    "type": "plot_data",
    "data": {
        "event_numbers": [1, 2, 3, 4, 5],
        "confidences": [0.45, 0.62, 0.78, 0.85, 0.92],
        "timestamps": ["14:30:22", "14:30:25", "14:30:28", "14:30:31", "14:30:34"]
    }
}
1.5 Spectrum Data
Type: spectrum

Real-time FFT data for spectrum analyzer.

json
{
    "type": "spectrum",
    "data": {
        "frequencies": [2400000000, 2401000000, ..., 2483500000],
        "amplitudes": [-85.2, -82.1, -78.5, ..., -92.3],
        "center_freq": 2441750000,
        "span": 83500000,
        "peak_freq": 2445000000,
        "peak_amplitude": -65.3,
        "timestamp": 1705325422
    }
}
1.6 Status
Type: status

System status updates.

json
{
    "type": "status",
    "data": {
        "state": "RUNNING",
        "mode": "AUTO_SCAN",
        "current_band": "2.4 GHz",
        "current_freq": 2445000000,
        "scan_progress": 65,
        "message": "Scanning 2.4 GHz band"
    }
}
States:

State	Description
RUNNING	Normal operation
PAUSED	Scanning paused
ERROR	System error
CALIBRATING	Performing calibration
SCANNING	Actively scanning bands
2. Client → Server Messages
2.1 Start Scanning
Start or resume drone detection.

json
"start"
Response: None (status update via status message)

2.2 Stop Scanning
Pause drone detection.

json
"stop"
Response: None (status update via status message)

2.3 Clear Detections
Clear detection history and reset plots.

json
"clear_detections"
Response: None

2.4 Set Frequency
Change center frequency.

json
"set_freq:2450000000"
Format: set_freq:<frequency_hz>

Valid Frequencies:

Band	Frequency Range
433 MHz	433000000 - 435000000
915 MHz	915000000 - 928000000
2.4 GHz	2400000000 - 2483500000
5.8 GHz	5725000000 - 5850000000
2.5 Set Band
Switch to a predefined band.

json
"set_band:2.4"
Valid Bands:

set_band:433 - 433 MHz band

set_band:915 - 915 MHz band

set_band:2.4 - 2.4 GHz band

set_band:5.8 - 5.8 GHz band

2.6 Set Gain
Adjust RF gain settings.

json
"set_gain:32:20"
Format: set_gain:<lna_gain>:<vga_gain>

Parameter	Range	Default	Description
lna_gain	0-40 dB	32	Low Noise Amplifier
vga_gain	0-62 dB	20	Variable Gain Amplifier
2.7 Set Threshold
Adjust alert confidence threshold.

json
"set_threshold:0.75"
Format: set_threshold:<value>

Range: 0.0 - 1.0 (default: 0.625)

2.8 Request Metrics
Request immediate metrics update.

json
"get_metrics"
Response: metrics message

2.9 Request Spectrum
Request current spectrum data.

json
"get_spectrum"
Response: spectrum message

2.10 Calibrate
Perform system calibration.

json
"calibrate"
Response: status message with calibration progress

2.11 Export Data
Export detection data to file.

json
"export:csv"
Formats:

export:csv - CSV format

export:json - JSON format

export:sqlite - SQLite database

Response: File download via separate HTTP endpoint

🔌 HTTP REST API (Optional)
For non-realtime operations, HTTP endpoints are available on port 8081.

GET /api/detections
Get recent detections.

http
GET /api/detections?limit=10&offset=0&threat=HIGH
Parameters:

Parameter	Type	Default	Description
limit	int	50	Number of records
offset	int	0	Pagination offset
threat	string	ALL	Filter by threat level
from	timestamp	-	Start date
to	timestamp	-	End date
Response:

json
{
    "total": 47,
    "detections": [
        {
            "id": 1,
            "timestamp": "2024-01-15 14:30:22",
            "drone_type": "DJI Mavic",
            "confidence": 0.85,
            "threat_level": "HIGH"
        }
    ]
}
GET /api/stats
Get system statistics.

http
GET /api/stats
Response:

json
{
    "total_detections_24h": 124,
    "by_drone_type": {
        "DJI Phantom": 45,
        "DJI Mavic": 38,
        "FPV Racing": 22,
        "Military Drone": 12,
        "Other": 7
    },
    "by_threat": {
        "CRITICAL": 8,
        "HIGH": 23,
        "MEDIUM": 45,
        "LOW": 38,
        "NEGLIGIBLE": 10
    },
    "avg_confidence": 0.72,
    "peak_detection_hour": 14
}
GET /api/bands
Get available frequency bands.

http
GET /api/bands
Response:

json
{
    "bands": [
        {
            "name": "2.4 GHz Control",
            "min_freq": 2400000000,
            "max_freq": 2483500000,
            "active": true,
            "detected_drones": ["DJI", "FrSky", "ELRS"]
        },
        {
            "name": "5.8 GHz Video",
            "min_freq": 5725000000,
            "max_freq": 5850000000,
            "active": true,
            "detected_drones": ["Analog", "DJI", "WalkSnail"]
        }
    ]
}
POST /api/alert/acknowledge
Acknowledge an alert.

http
POST /api/alert/acknowledge
Content-Type: application/json

{
    "alert_id": "alert_1705325422",
    "action_taken": "NOTIFIED_SECURITY",
    "operator": "admin"
}
Response:

json
{
    "success": true,
    "message": "Alert acknowledged"
}
📊 WebSocket Event Flow Diagram
text
Client                          Server
  |                               |
  |--- WS Connect --------------->|
  |<-- Connection Established ----|
  |                               |
  |--- "start" ------------------>|
  |                               |
  |<-- status (RUNNING) ----------|
  |<-- spectrum (update) ---------|
  |<-- detection (drone found) ---|
  |<-- alert (if critical) -------|
  |<-- metrics (periodic) --------|
  |                               |
  |--- "set_band:2.4" ----------->|
  |<-- status (SCANNING) ---------|
  |                               |
  |--- "stop" ------------------->|
  |<-- status (PAUSED) -----------|
  |                               |
  |--- "clear_detections" ------->|
  |<-- plot_data (reset) ---------|
  |                               |
  |--- WS Disconnect -------------|
🛠 Error Handling
Error Response Format
json
{
    "type": "error",
    "data": {
        "code": 4001,
        "message": "Invalid frequency",
        "details": "Frequency must be between 2400 MHz and 2483.5 MHz",
        "timestamp": "2024-01-15 14:30:22"
    }
}
Error Codes
Code	Name	Description
1000	AUTH_FAILED	Authentication failed
1001	CONNECTION_LOST	WebSocket connection lost
2000	INVALID_COMMAND	Unknown command
2001	INVALID_PARAMETER	Invalid parameter value
2002	INVALID_FREQUENCY	Frequency out of range
3000	HARDWARE_ERROR	HackRF device error
3001	USB_ERROR	USB communication error
3002	RF_OVERRANGE	RF input out of range
4000	DATABASE_ERROR	SQLite error
4001	QUERY_FAILED	Database query failed
5000	INTERNAL_ERROR	Internal system error
🔒 Authentication (If Enabled)
For production deployments, include authentication token:

javascript
// Connect with authentication
const ws = new WebSocket('ws://localhost:8082?token=your_api_token');

// Or send after connection
ws.send('auth:your_api_token');
API Keys
Generate API key:

bash
curl -X POST http://localhost:8081/api/auth/generate \
    -H "Content-Type: application/json" \
    -d '{"role": "admin", "expires": "2024-12-31"}'
Response:

json
{
    "api_key": "hkdf_1234567890abcdef",
    "expires": "2024-12-31 23:59:59"
}
📈 Rate Limiting
Endpoint	Limit	Window
WebSocket messages	100/sec	1 second
HTTP GET	60/min	1 minute
HTTP POST	30/min	1 minute
Export requests	10/hour	1 hour
Rate limit exceeded response:

json
{
    "error": "Rate limit exceeded",
    "retry_after": 60,
    "limit": 60,
    "remaining": 0
}
🧪 Example Client Implementations
JavaScript (Browser)
javascript
class DroneDetectionClient {
    constructor(url) {
        this.ws = new WebSocket(url);
        this.setupEventHandlers();
    }
    
    setupEventHandlers() {
        this.ws.onopen = () => {
            console.log('Connected');
            this.start();
        };
        
        this.ws.onmessage = (event) => {
            const msg = JSON.parse(event.data);
            this.handleMessage(msg);
        };
        
        this.ws.onerror = (error) => {
            console.error('WebSocket error:', error);
        };
    }
    
    handleMessage(msg) {
        switch(msg.type) {
            case 'detection':
                this.onDetection(msg.data);
                break;
            case 'alert':
                this.onAlert(msg.data);
                break;
            case 'metrics':
                this.onMetrics(msg.data);
                break;
        }
    }
    
    start() { this.ws.send('start'); }
    stop() { this.ws.send('stop'); }
    setBand(band) { this.ws.send(`set_band:${band}`); }
    
    onDetection(detection) {
        console.log(`Drone detected: ${detection.drone_type}`);
        // Update UI
    }
    
    onAlert(alert) {
        console.warn(`ALERT: ${alert.message}`);
        // Show notification
    }
    
    onMetrics(metrics) {
        console.log(`Detections: ${metrics.total_detections}`);
        // Update dashboard
    }
}

// Usage
const client = new DroneDetectionClient('ws://localhost:8082');
Python Client
python
import asyncio
import websockets
import json

class DroneDetectionClient:
    def __init__(self, uri="ws://localhost:8082"):
        self.uri = uri
        self.websocket = None
        
    async def connect(self):
        self.websocket = await websockets.connect(self.uri)
        print("Connected to drone detection system")
        
    async def start(self):
        await self.websocket.send("start")
        
    async def stop(self):
        await self.websocket.send("stop")
        
    async def set_band(self, band):
        await self.websocket.send(f"set_band:{band}")
        
    async def listen(self):
        async for message in self.websocket:
            data = json.loads(message)
            if data['type'] == 'detection':
                print(f"🚁 Drone: {data['data']['drone_type']} "
                      f"({data['data']['confidence']*100:.0f}% confidence)")
            elif data['type'] == 'alert':
                print(f"🚨 ALERT: {data['data']['message']}")
                
    async def run(self):
        await self.connect()
        await self.start()
        await self.listen()

# Usage
async def main():
    client = DroneDetectionClient()
    await client.run()

asyncio.run(main())
C++ Client (Qt)
cpp
#include <QtWebSockets/QWebSocket>
#include <QJsonDocument>
#include <QJsonObject>

class DroneDetectionClient : public QObject {
    Q_OBJECT
private:
    QWebSocket m_webSocket;
    
public:
    DroneDetectionClient() {
        connect(&m_webSocket, &QWebSocket::connected, 
                this, &DroneDetectionClient::onConnected);
        connect(&m_webSocket, &QWebSocket::textMessageReceived,
                this, &DroneDetectionClient::onMessageReceived);
    }
    
    void connectToServer() {
        m_webSocket.open(QUrl("ws://localhost:8082"));
    }
    
private slots:
    void onConnected() {
        qDebug() << "Connected to drone detection system";
        m_webSocket.sendTextMessage("start");
    }
    
    void onMessageReceived(QString message) {
        QJsonDocument doc = QJsonDocument::fromJson(message.toUtf8());
        QJsonObject obj = doc.object();
        
        if (obj["type"].toString() == "detection") {
            QJsonObject data = obj["data"].toObject();
            qDebug() << "Drone detected:" << data["drone_type"].toString();
        }
    }
};
