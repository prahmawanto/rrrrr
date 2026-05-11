drone-detector/data/exports/detections/README.md - Detections Exports Documentation

markdown
# Detections Exports Directory

This directory contains exported detection data from the Drone Detection System. Exports include detection records, statistics, and metadata in various formats for analysis, reporting, and integration with external systems.

## Directory Structure
data/exports/detections/
├── README.md # This file
├── detections_20240115.csv # Daily detection export (CSV)
├── detections_20240115.json # Daily detection export (JSON)
├── detections_20240115.xlsx # Daily detection export (Excel)
├── detections_20240116.csv
├── detections_20240116.json
├── detections_20240116.xlsx
├── detections_20240117.csv
├── detections_week_2024_W03.csv # Weekly export
├── detections_month_2024_01.csv # Monthly export
├── detections_custom_20240115_143022.csv # Custom range export
├── summary_20240115.json # Summary statistics only
├── incident_20240115_detections.json # Incident-specific export
└── index.json # Export index and metadata

text

## Naming Convention

Export files follow a consistent naming pattern:

| Export Type | Pattern | Example |
|-------------|---------|---------|
| Daily | `detections_YYYYMMDD.format` | `detections_20240115.csv` |
| Weekly | `detections_week_YYYY_WWW.format` | `detections_week_2024_W03.csv` |
| Monthly | `detections_month_YYYY_MM.format` | `detections_month_2024_01.csv` |
| Custom | `detections_custom_YYYYMMDD_HHMMSS.format` | `detections_custom_20240115_143022.json` |
| Summary | `summary_YYYYMMDD.json` | `summary_20240115.json` |
| Incident | `incident_YYYYMMDD_detections.format` | `incident_20240115_detections.json` |

## File Formats

### CSV Format (.csv)

CSV files are optimized for spreadsheet applications and data analysis tools.

**Schema:**
```csv
id,timestamp,drone_type,manufacturer,confidence,threat_level,frequency,signal_strength,snr,bandwidth,modulation,latitude,longitude,altitude,speed,heading,remote_id,operator_id,source,verified
det_001,2024-01-15T14:30:22Z,DJI Mavic 3,DJI,0.95,HIGH,2.44e9,-45.2,28.5,20e6,OFDM,37.7749,-122.4194,100.0,12.5,180.0,ABCD1234,OP5678,sdr,true
Field Descriptions:

Field	Type	Description	Example
id	string	Unique detection identifier	det_001
timestamp	datetime	UTC detection time	2024-01-15T14:30:22Z
drone_type	string	Identified drone model	DJI Mavic 3
manufacturer	string	Drone manufacturer	DJI
confidence	float	Detection confidence (0-1)	0.95
threat_level	string	Threat assessment	HIGH
frequency	float	Center frequency (Hz)	2.44e9
signal_strength	float	Signal power (dBm)	-45.2
snr	float	Signal-to-noise ratio (dB)	28.5
bandwidth	float	Signal bandwidth (Hz)	20e6
modulation	string	Modulation type	OFDM
latitude	float	GPS latitude	37.7749
longitude	float	GPS longitude	-122.4194
altitude	float	Altitude (meters)	100.0
speed	float	Speed (m/s)	12.5
heading	float	Direction (degrees)	180.0
remote_id	string	Remote ID	ABCD1234
operator_id	string	Operator ID	OP5678
source	string	Detection source	sdr
verified	boolean	Ground truth verified	true
JSON Format (.json)
JSON files provide structured data with metadata and statistics.

json
{
  "export_info": {
    "export_id": "exp_20240115_001",
    "export_date": "2024-01-15T14:35:00Z",
    "export_format": "json",
    "version": "2.0.0",
    "source_system": "Drone Detection System",
    "export_type": "daily",
    "date_range": {
      "start": "2024-01-15T00:00:00Z",
      "end": "2024-01-15T23:59:59Z"
    },
    "filters_applied": {
      "min_confidence": 0.0,
      "threat_levels": ["LOW", "MEDIUM", "HIGH", "CRITICAL"],
      "drone_types": []
    }
  },
  "statistics": {
    "total_detections": 1247,
    "by_threat_level": {
      "CRITICAL": 0,
      "HIGH": 342,
      "MEDIUM": 567,
      "LOW": 338
    },
    "by_drone_type": {
      "DJI Mavic 3": 456,
      "FPV Analog": 234,
      "DJI Mini 3": 189,
      "Autel EVO II": 123,
      "Skydio 2": 78,
      "Unknown": 167
    },
    "by_hour": {
      "0": 12, "1": 8, "2": 5, "3": 3, "4": 2, "5": 4,
      "6": 15, "7": 45, "8": 89, "9": 120, "10": 145,
      "11": 156, "12": 167, "13": 178, "14": 189,
      "15": 201, "16": 234, "17": 256, "18": 234,
      "19": 198, "20": 167, "21": 134, "22": 98, "23": 45
    },
    "avg_confidence": 0.87,
    "unique_drones": 89,
    "total_incidents": 12
  },
  "data": [
    {
      "id": "det_001",
      "timestamp": "2024-01-15T14:30:22Z",
      "drone_type": "DJI Mavic 3",
      "confidence": 0.95,
      "threat_level": "HIGH",
      "position": {
        "latitude": 37.7749,
        "longitude": -122.4194,
        "altitude": 100.0
      },
      "signal": {
        "frequency": 2440000000,
        "strength": -45.2,
        "snr": 28.5,
        "bandwidth": 20000000,
        "modulation": "OFDM"
      },
      "remote_id": {
        "uas_id": "ABCD1234",
        "operator_id": "OP5678",
        "valid": true
      }
    }
  ]
}
Excel Format (.xlsx)
Excel files provide multi-sheet workbooks with formatted data:

Sheet 1: Detections

Raw detection data with formatting

Conditional formatting for threat levels

Filterable columns

Frozen header row

Sheet 2: Summary

Aggregated statistics

Pivot tables

Charts and visualizations

Key performance indicators

Sheet 3: Timeline

Hourly detection counts

Daily trends

Weekly patterns

Monthly overview

Sheet 4: Locations

Geographic distribution

Hotspot analysis

Geofence violations

Heatmap data

Sheet 5: Metadata

Export information

Data dictionary

Notes and disclaimers

Contact information

Export Operations
Creating Daily Export
python
async def create_daily_export(date=None):
    """Create daily detection export"""
    
    from datetime import datetime, timedelta
    
    if date is None:
        date = datetime.now() - timedelta(days=1)
    
    start_date = datetime(date.year, date.month, date.day, 0, 0, 0)
    end_date = start_date + timedelta(days=1)
    
    # Fetch detections
    detections = await get_detections_by_date_range(start_date, end_date)
    
    # Generate filename
    filename = f"detections_{start_date.strftime('%Y%m%d')}"
    
    # Export to multiple formats
    exports = {}
    
    # CSV export
    csv_path = f"data/exports/detections/{filename}.csv"
    await export_to_csv(detections, csv_path)
    exports['csv'] = csv_path
    
    # JSON export
    json_path = f"data/exports/detections/{filename}.json"
    await export_to_json(detections, json_path)
    exports['json'] = json_path
    
    # Excel export
    excel_path = f"data/exports/detections/{filename}.xlsx"
    await export_to_excel(detections, excel_path)
    exports['excel'] = excel_path
    
    # Update index
    await update_export_index(filename, exports, len(detections))
    
    return exports
Creating Custom Export
python
async def create_custom_export(filters, formats=['csv', 'json']):
    """Create custom detection export with filters"""
    
    from datetime import datetime
    
    # Apply filters
    detections = await get_detections_with_filters(filters)
    
    # Generate unique ID
    export_id = datetime.now().strftime('%Y%m%d_%H%M%S')
    filename = f"detections_custom_{export_id}"
    
    exports = {}
    
    for format in formats:
        if format == 'csv':
            path = f"data/exports/detections/{filename}.csv"
            await export_to_csv(detections, path)
            exports['csv'] = path
        
        elif format == 'json':
            path = f"data/exports/detections/{filename}.json"
            await export_to_json(detections, path, include_stats=True)
            exports['json'] = path
        
        elif format == 'excel':
            path = f"data/exports/detections/{filename}.xlsx"
            await export_to_excel(detections, path)
            exports['excel'] = path
    
    # Save export metadata
    metadata = {
        'export_id': export_id,
        'export_date': datetime.now().isoformat(),
        'filters': filters,
        'record_count': len(detections),
        'exports': exports
    }
    
    metadata_path = f"data/exports/detections/{filename}_metadata.json"
    with open(metadata_path, 'w') as f:
        json.dump(metadata, f, indent=2)
    
    return exports
Exporting Incident Detections
python
async def export_incident_detections(incident_id, detection_ids):
    """Export detections related to a specific incident"""
    
    from datetime import datetime
    
    # Fetch detections by IDs
    detections = await get_detections_by_ids(detection_ids)
    
    # Generate incident export
    filename = f"incident_{datetime.now().strftime('%Y%m%d')}_detections"
    
    # Create JSON export with incident context
    export_data = {
        'incident_id': incident_id,
        'export_date': datetime.now().isoformat(),
        'detection_count': len(detections),
        'detections': detections,
        'incident_details': await get_incident_details(incident_id),
        'related_alerts': await get_alerts_for_incident(incident_id),
        'evidence_files': await get_evidence_files(incident_id)
    }
    
    json_path = f"data/exports/detections/{filename}.json"
    with open(json_path, 'w') as f:
        json.dump(export_data, f, indent=2, default=str)
    
    # Also create PDF report for the incident
    pdf_path = f"data/exports/detections/{filename}.pdf"
    await generate_incident_report_pdf(export_data, pdf_path)
    
    return {'json': json_path, 'pdf': pdf_path}
Export API
REST Endpoints
python
from fastapi import APIRouter, Query, Body, Depends
from datetime import datetime

router = APIRouter(prefix="/api/exports/detections", tags=["detection-exports"])

@router.get("/daily/{date}")
async def get_daily_export(
    date: str = Path(..., description="Date in YYYYMMDD format"),
    format: str = Query("csv", regex="^(csv|json|excel)$"),
    user = Depends(get_current_user)
):
    """Download daily detection export"""
    
    export_path = Path(f"data/exports/detections/detections_{date}.{format}")
    
    if not export_path.exists():
        raise HTTPException(404, "Export not found for specified date")
    
    return FileResponse(
        export_path,
        filename=export_path.name,
        media_type=get_mime_type(format)
    )

@router.post("/custom")
async def create_custom_export_endpoint(
    filters: dict = Body(...),
    formats: list = Body(["csv", "json"]),
    user = Depends(require_permission("exports:create"))
):
    """Create custom detection export"""
    
    export_id = await create_custom_export(filters, formats)
    
    return {
        "message": "Export created successfully",
        "export_id": export_id,
        "download_urls": get_download_urls(export_id)
    }

@router.get("/list")
async def list_exports(
    start_date: Optional[datetime] = Query(None),
    end_date: Optional[datetime] = Query(None),
    limit: int = Query(50, le=100),
    user = Depends(get_current_user)
):
    """List available detection exports"""
    
    exports = await scan_exports_directory(
        start_date=start_date,
        end_date=end_date,
        limit=limit
    )
    
    return {"exports": exports, "total": len(exports)}
Data Processing
Loading Export for Analysis
python
import pandas as pd
import json

def load_detection_export(file_path):
    """Load detection export for analysis"""
    
    file_path = Path(file_path)
    
    if file_path.suffix == '.csv':
        # Load CSV with pandas
        df = pd.read_csv(file_path)
        df['timestamp'] = pd.to_datetime(df['timestamp'])
        return df
    
    elif file_path.suffix == '.json':
        # Load JSON
        with open(file_path, 'r') as f:
            data = json.load(f)
        
        if 'data' in data:
            return pd.DataFrame(data['data'])
        else:
            return pd.DataFrame(data)
    
    elif file_path.suffix == '.xlsx':
        # Load Excel
        return pd.read_excel(file_path, sheet_name='Detections')
    
    else:
        raise ValueError(f"Unsupported format: {file_path.suffix}")
Analyzing Exported Data
python
def analyze_detection_export(df):
    """Perform analysis on exported detection data"""
    
    analysis = {
        'total_detections': len(df),
        'date_range': {
            'start': df['timestamp'].min(),
            'end': df['timestamp'].max()
        },
        'threat_distribution': df['threat_level'].value_counts().to_dict(),
        'top_drone_types': df['drone_type'].value_counts().head(10).to_dict(),
        'avg_confidence': df['confidence'].mean(),
        'peak_hour': df['timestamp'].dt.hour.value_counts().idxmax(),
        'unique_drones': df['drone_id'].nunique() if 'drone_id' in df else None,
        'detections_by_hour': df['timestamp'].dt.hour.value_counts().sort_index().to_dict()
    }
    
    # Calculate hourly trend
    hourly = df.groupby(df['timestamp'].dt.hour).size()
    analysis['peak_hours'] = hourly.nlargest(3).to_dict()
    
    # Calculate daily trend
    daily = df.groupby(df['timestamp'].dt.date).size()
    analysis['busiest_day'] = daily.idxmax().isoformat()
    
    return analysis
Export Management
Automatic Cleanup
python
async def cleanup_old_exports(days=30):
    """Delete exports older than specified days"""
    
    from datetime import datetime, timedelta
    
    cutoff = datetime.now() - timedelta(days=days)
    exports_dir = Path("data/exports/detections")
    deleted = []
    
    for file_path in exports_dir.glob("*"):
        if file_path.is_file() and file_path.name != "README.md":
            mtime = datetime.fromtimestamp(file_path.stat().st_mtime)
            
            if mtime < cutoff:
                # Move to archive instead of delete
                archive_path = Path("data/exports/archived") / file_path.name
                archive_path.parent.mkdir(parents=True, exist_ok=True)
                file_path.rename(archive_path)
                deleted.append(str(archive_path))
    
    return {
        'deleted_count': len(deleted),
        'deleted_files': deleted,
        'cutoff_date': cutoff.isoformat()
    }
Export Verification
python
def verify_export_integrity(file_path):
    """Verify export file integrity"""
    
    file_path = Path(file_path)
    
    if not file_path.exists():
        return {'valid': False, 'error': 'File not found'}
    
    file_size = file_path.stat().st_size
    
    if file_size == 0:
        return {'valid': False, 'error': 'Empty file'}
    
    # Verify based on format
    if file_path.suffix == '.csv':
        try:
            df = pd.read_csv(file_path)
            required_columns = ['id', 'timestamp', 'drone_type', 'confidence', 'threat_level']
            missing = [col for col in required_columns if col not in df.columns]
            
            if missing:
                return {'valid': False, 'error': f'Missing columns: {missing}'}
            
            return {
                'valid': True,
                'rows': len(df),
                'columns': list(df.columns),
                'size_mb': file_size / (1024 * 1024)
            }
            
        except Exception as e:
            return {'valid': False, 'error': str(e)}
    
    elif file_path.suffix == '.json':
        try:
            with open(file_path, 'r') as f:
                data = json.load(f)
            
            if 'data' in data:
                records = len(data['data'])
            else:
                records = len(data)
            
            return {
                'valid': True,
                'records': records,
                'size_mb': file_size / (1024 * 1024),
                'has_metadata': 'export_info' in data
            }
            
        except Exception as e:
            return {'valid': False, 'error': str(e)}
    
    return {'valid': True, 'size_mb': file_size / (1024 * 1024)}
Integration Examples
Import to Python (Pandas)
python
import pandas as pd

# Load daily export
df = pd.read_csv('data/exports/detections/detections_20240115.csv')

# Convert timestamp
df['timestamp'] = pd.to_datetime(df['timestamp'])

# Filter high threat detections
high_threat = df[df['threat_level'] == 'HIGH']

# Group by hour
hourly = df.groupby(df['timestamp'].dt.hour).size()

# Create time series
ts = df.set_index('timestamp').resample('1H').size()
Import to R
r
library(readr)
library(dplyr)
library(lubridate)

# Load CSV export
detections <- read_csv('data/exports/detections/detections_20240115.csv')

# Convert timestamp
detections$timestamp <- ymd_hms(detections$timestamp)

# Filter by drone type
dji_mavic <- detections %>% filter(drone_type == "DJI Mavic 3")

# Summary by threat level
summary <- detections %>% 
  group_by(threat_level) %>% 
  summarise(count = n())
Import to SQL
sql
-- Create temporary table
CREATE TEMP TABLE temp_detections (
    id TEXT,
    timestamp TIMESTAMP,
    drone_type TEXT,
    confidence REAL,
    threat_level TEXT,
    latitude REAL,
    longitude REAL
);

-- Import CSV
COPY temp_detections(id, timestamp, drone_type, confidence, threat_level, latitude, longitude)
FROM '/path/to/detections_20240115.csv'
DELIMITER ','
CSV HEADER;

-- Query imported data
SELECT threat_level, COUNT(*) 
FROM temp_detections 
GROUP BY threat_level;
Storage Guidelines
Retention Policy
Export Type	Retention	Compression	Archive
Daily exports	30 days	gzip after 7 days	Monthly
Weekly exports	90 days	gzip after 30 days	Quarterly
Monthly exports	365 days	gzip after 90 days	Yearly
Custom exports	7 days	None	User discretion
Incident exports	365 days	None	Permanent
Summary exports	90 days	gzip after 30 days	Quarterly
Storage Limits
python
def check_storage_limit():
    """Check if exports are within storage limits"""
    
    exports_dir = Path("data/exports/detections")
    total_size = sum(f.stat().st_size for f in exports_dir.glob("*") if f.is_file())
    size_gb = total_size / (1024 ** 3)
    
    limits = {
        'warning': 5,   # 5 GB warning
        'critical': 10,  # 10 GB critical
        'max': 20        # 20 GB maximum
    }
    
    if size_gb > limits['critical']:
        return {'status': 'critical', 'size_gb': size_gb, 'action': 'Cleanup required'}
    elif size_gb > limits['warning']:
        return {'status': 'warning', 'size_gb': size_gb, 'action': 'Consider cleanup'}
    else:
        return {'status': 'ok', 'size_gb': size_gb}
Troubleshooting
Common Issues
Issue	Cause	Solution
Export missing	No data for date	Verify date range and data availability
Corrupted file	Incomplete write	Re-run export or restore from backup
Format errors	Schema mismatch	Check export version and compatibility
Large file size	Too many records	Use filtering or pagination
Slow generation	Complex queries	Optimize filters or use summary export
Export Recovery
python
async def recover_missing_export(date):
    """Recover missing daily export"""
    
    # Check if export exists
    export_path = Path(f"data/exports/detections/detections_{date}.csv")
    
    if export_path.exists():
        return {'status': 'exists', 'path': str(export_path)}
    
    # Try to find in archive
    archive_path = Path(f"data/exports/archived/detections_{date}.csv")
    
    if archive_path.exists():
        # Restore from archive
        archive_path.rename(export_path)
        return {'status': 'restored', 'path': str(export_path)}
    
    # Regenerate export
    await create_daily_export(datetime.strptime(date, '%Y%m%d'))
    
    return {'status': 'regenerated', 'path': str(export_path)}
Best Practices
Export Scheduling
python
# Recommended export schedule
EXPORT_SCHEDULE = {
    'daily': {
        'time': '01:00',
        'formats': ['csv', 'json'],
        'retention': 30
    },
    'weekly': {
        'day': 'Monday',
        'time': '02:00',
        'formats': ['csv', 'json', 'excel'],
        'retention': 90
    },
    'monthly': {
        'day': 1,
        'time': '03:00',
        'formats': ['json', 'excel'],
        'retention': 365
    },
    'summary': {
        'time': '04:00',
        'formats': ['json'],
        'retention': 90
    }
}
Data Quality Checks
python
def validate_export_quality(file_path):
    """Perform quality checks on export"""
    
    df = load_detection_export(file_path)
    
    checks = {
        'has_data': len(df) > 0,
        'no_null_ids': df['id'].notna().all(),
        'valid_timestamps': df['timestamp'].notna().all(),
        'confidence_range': df['confidence'].between(0, 1).all(),
        'valid_threats': df['threat_level'].isin(['LOW', 'MEDIUM', 'HIGH', 'CRITICAL']).all()
    }
    
    quality_score = sum(checks.values()) / len(checks) * 100
    
    return {
        'checks': checks,
        'quality_score': quality_score,
        'pass': quality_score == 100
    }
