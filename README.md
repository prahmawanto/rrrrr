drone-detector/data/exports/README.md - Exports Directory Documentation

markdown
# Exports Directory

This directory contains exported data from the Drone Detection System, including detection records, spectrum data, reports, and ML training features. Exports are used for analysis, reporting, backup, and sharing with external systems.

## Directory Structure
data/exports/
├── README.md # This file
├── detections/ # Detection data exports
│ ├── detections_20240115.csv
│ ├── detections_20240115.json
│ ├── detections_20240116.csv
│ ├── detections_20240116.json
│ ├── detections_20240117.xlsx
│ └── README.md
├── spectrum/ # Spectrum analysis exports
│ ├── spectrum_snapshot_20240115_143022.png
│ ├── spectrum_snapshot_20240115_143022.json
│ ├── waterfall_snapshot_20240115_143022.png
│ ├── spectrum_data_20240115.csv
│ └── README.md
├── reports/ # Generated reports
│ ├── daily_report_20240115.md
│ ├── daily_report_20240115.pdf
│ ├── weekly_report_2024_W03.md
│ ├── weekly_report_2024_W03.pdf
│ ├── monthly_report_2024_01.md
│ ├── monthly_report_2024_01.pdf
│ ├── incident_report_20240115.md
│ ├── incident_report_20240115.pdf
│ └── README.md
├── ml/ # ML training data exports
│ ├── features_20240115.csv
│ ├── features_20240115.npy
│ ├── evaluation_20240115.json
│ ├── training_set.json
│ ├── validation_set.json
│ ├── test_set.json
│ └── README.md
├── archived/ # Compressed old exports
│ └── 2026-01/
│ ├── exports_2024_Q4.tar.gz
│ ├── exports_2025_Q1.tar.gz
│ └── ...
└── index.json # Global exports index

text

## Export Formats

### CSV Format (detections/)

CSV files contain tabular detection data for spreadsheet analysis.

```csv
id,timestamp,drone_type,confidence,threat_level,latitude,longitude,altitude,frequency,signal_strength
det_001,2024-01-15T14:30:22Z,DJI Mavic 3,0.95,HIGH,37.7749,-122.4194,100.0,2.44e9,-45.2
det_002,2024-01-15T14:31:15Z,FPV Analog,0.87,MEDIUM,37.7750,-122.4185,50.0,5.80e9,-55.1
JSON Format (detections/)
JSON files contain structured detection data with metadata.

json
{
  "export_info": {
    "export_date": "2024-01-15T14:35:00Z",
    "export_format": "json",
    "version": "2.0.0",
    "source": "Drone Detection System",
    "date_range": {
      "start": "2024-01-01T00:00:00Z",
      "end": "2024-01-15T23:59:59Z"
    }
  },
  "statistics": {
    "total_detections": 1247,
    "by_threat_level": {
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
    }
  },
  "data": [
    {
      "id": "det_001",
      "timestamp": "2024-01-15T14:30:22Z",
      "drone_type": "DJI Mavic 3",
      "confidence": 0.95,
      "threat_level": "HIGH",
      "latitude": 37.7749,
      "longitude": -122.4194,
      "altitude": 100.0,
      "frequency": 2440000000,
      "signal_strength": -45.2
    }
  ]
}
Excel Format (detections/)
Excel files provide multi-sheet exports with formatted data:

Sheet	Content
Detections	Raw detection data
Summary	Aggregated statistics
Charts	Visualizations
Metadata	Export information
Image Formats (spectrum/)
Format	Use Case	Resolution
PNG	Spectrum plots, watermarks	1920x1080
SVG	Vector graphics for reports	Scalable
PDF	High-quality printing	Vector
Report Formats (reports/)
Format	Use Case	Features
Markdown	Readable text, version control	Lightweight, editable
PDF	Distribution, printing	Paginated, formatted
HTML	Web viewing	Interactive, linked
DOCX	Word processing	Editable, compatible
ML Data Formats (ml/)
Format	Use Case	Description
CSV	Feature analysis	Human-readable features
NPY	Fast loading	NumPy binary format
JSON	Metadata	Configuration and labels
PKL	Python models	Pickled classifiers
Export Operations
Exporting Detections
python
from infrastructure.storage import DetectionRepository
from datetime import datetime, timedelta

async def export_detections():
    """Export detections to CSV and JSON"""
    
    repo = DetectionRepository()
    
    # Get detections from last 7 days
    end_date = datetime.now()
    start_date = end_date - timedelta(days=7)
    
    detections = await repo.get_by_date_range(start_date, end_date)
    
    # Export to CSV
    csv_path = f"data/exports/detections/detections_{end_date.strftime('%Y%m%d')}.csv"
    await export_to_csv(detections, csv_path)
    
    # Export to JSON
    json_path = f"data/exports/detections/detections_{end_date.strftime('%Y%m%d')}.json"
    await export_to_json(detections, json_path)
    
    return {'csv': csv_path, 'json': json_path}
Exporting Spectrum Data
python
async def export_spectrum_snapshot(spectrum_data, timestamp):
    """Export spectrum snapshot as image and data"""
    
    import matplotlib.pyplot as plt
    
    # Generate plot
    fig, ax = plt.subplots(figsize=(12, 6))
    ax.plot(spectrum_data.frequencies, spectrum_data.powers)
    ax.set_xlabel('Frequency (MHz)')
    ax.set_ylabel('Power (dBm)')
    ax.set_title(f'Spectrum Snapshot - {timestamp}')
    ax.grid(True, alpha=0.3)
    
    # Save image
    image_path = f"data/exports/spectrum/spectrum_snapshot_{timestamp}.png"
    plt.savefig(image_path, dpi=150, bbox_inches='tight')
    
    # Save data
    data_path = f"data/exports/spectrum/spectrum_data_{timestamp}.csv"
    np.savetxt(data_path, 
               np.column_stack([spectrum_data.frequencies, spectrum_data.powers]),
               delimiter=',',
               header='Frequency(Hz),Power(dBm)')
    
    plt.close()
    
    return {'image': image_path, 'data': data_path}
Generating Reports
python
async def generate_daily_report(date=None):
    """Generate daily report in multiple formats"""
    
    if date is None:
        date = datetime.now()
    
    # Collect data
    detections = await get_detections_for_date(date)
    alerts = await get_alerts_for_date(date)
    metrics = await get_metrics_for_date(date)
    
    # Generate Markdown
    md_content = generate_markdown_report(detections, alerts, metrics)
    md_path = f"data/exports/reports/daily_report_{date.strftime('%Y%m%d')}.md"
    with open(md_path, 'w') as f:
        f.write(md_content)
    
    # Generate PDF
    pdf_path = f"data/exports/reports/daily_report_{date.strftime('%Y%m%d')}.pdf"
    await convert_markdown_to_pdf(md_path, pdf_path)
    
    return {'markdown': md_path, 'pdf': pdf_path}
Export Scheduling
Automated Daily Exports
python
import schedule
import asyncio

def schedule_daily_exports():
    """Schedule automated daily exports"""
    
    # Daily detection export at 00:30
    schedule.every().day.at("00:30").do(
        lambda: asyncio.run(export_detections())
    )
    
    # Weekly report every Monday at 08:00
    schedule.every().monday.at("08:00").do(
        lambda: asyncio.run(generate_weekly_report())
    )
    
    # Monthly report on 1st at 09:00
    schedule.every().month.at("09:00").do(
        lambda: asyncio.run(generate_monthly_report())
    )
    
    # Clean old exports every Sunday at 02:00
    schedule.every().sunday.at("02:00").do(
        lambda: asyncio.run(cleanup_old_exports(days=90))
    )
Export Configuration
yaml
# config/exports.yaml
exports:
  detections:
    enabled: true
    schedule: "0 1 * * *"  # Daily at 01:00
    formats: ["csv", "json"]
    retention_days: 90
    filters:
      min_confidence: 0.5
      date_range: "last_7_days"
  
  spectrum:
    enabled: true
    schedule: "*/30 * * * *"  # Every 30 minutes
    formats: ["png", "csv"]
    retention_days: 30
    resolution: "1920x1080"
  
  reports:
    daily:
      enabled: true
      schedule: "0 2 * * *"  # Daily at 02:00
      formats: ["md", "pdf"]
      retention_days: 30
    weekly:
      enabled: true
      schedule: "0 3 * * 1"  # Monday at 03:00
      formats: ["md", "pdf"]
      retention_days: 90
    monthly:
      enabled: true
      schedule: "0 4 1 * *"  # 1st at 04:00
      formats: ["md", "pdf"]
      retention_days: 365
Export API
REST API Endpoints
python
from fastapi import APIRouter, Query, Response
from datetime import datetime

router = APIRouter(prefix="/api/exports", tags=["exports"])

@router.get("/detections")
async def export_detections(
    start_date: datetime = Query(...),
    end_date: datetime = Query(...),
    format: str = Query("csv", regex="^(csv|json|excel)$")
):
    """Export detections within date range"""
    
    exporter = DetectionExporter()
    file_path = await exporter.export(
        start_date=start_date,
        end_date=end_date,
        format=format
    )
    
    return FileResponse(
        file_path,
        filename=file_path.name,
        media_type=exporter.get_mime_type(format)
    )

@router.get("/spectrum/{snapshot_id}")
async def export_spectrum(
    snapshot_id: str,
    format: str = Query("png", regex="^(png|svg|csv)$")
):
    """Export spectrum snapshot"""
    
    exporter = SpectrumExporter()
    file_path = await exporter.export_snapshot(snapshot_id, format)
    
    return FileResponse(file_path)

@router.post("/reports/generate")
async def generate_report(
    report_type: str = Query(..., regex="^(daily|weekly|monthly|custom)$"),
    start_date: Optional[datetime] = None,
    end_date: Optional[datetime] = None
):
    """Generate and download report"""
    
    generator = ReportGenerator()
    report_path = await generator.generate(
        report_type=report_type,
        start_date=start_date,
        end_date=end_date
    )
    
    return FileResponse(report_path)
Export Management
Listing Exports
python
async def list_exports(category=None, days=30):
    """List available exports"""
    
    base_path = Path("data/exports")
    cutoff = datetime.now() - timedelta(days=days)
    exports = []
    
    if category:
        search_paths = [base_path / category]
    else:
        search_paths = [base_path / d for d in ['detections', 'spectrum', 'reports', 'ml']]
    
    for search_path in search_paths:
        if not search_path.exists():
            continue
        
        for file_path in search_path.iterdir():
            if file_path.is_file():
                mtime = datetime.fromtimestamp(file_path.stat().st_mtime)
                if mtime > cutoff:
                    exports.append({
                        'name': file_path.name,
                        'path': str(file_path),
                        'size_mb': file_path.stat().st_size / (1024 * 1024),
                        'modified': mtime.isoformat(),
                        'category': search_path.name
                    })
    
    return sorted(exports, key=lambda x: x['modified'], reverse=True)
Download Export
python
async def download_export(export_path, request):
    """Download export file"""
    
    from fastapi.responses import FileResponse
    
    export_path = Path(export_path)
    
    if not export_path.exists():
        raise HTTPException(404, "Export not found")
    
    # Determine MIME type
    mime_types = {
        '.csv': 'text/csv',
        '.json': 'application/json',
        '.xlsx': 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet',
        '.png': 'image/png',
        '.pdf': 'application/pdf',
        '.md': 'text/markdown'
    }
    
    media_type = mime_types.get(export_path.suffix, 'application/octet-stream')
    
    return FileResponse(
        export_path,
        filename=export_path.name,
        media_type=media_type
    )
Deleting Exports
python
async def delete_export(export_path):
    """Delete export file"""
    
    export_path = Path(export_path)
    
    if not export_path.exists():
        raise HTTPException(404, "Export not found")
    
    # Optional: move to archive instead of deleting
    archive_path = Path("data/exports/archived") / export_path.name
    export_path.rename(archive_path)
    
    return {'message': f'Export moved to archive: {archive_path}'}
Storage Management
Automatic Cleanup
python
async def cleanup_old_exports(days=90):
    """Delete exports older than specified days"""
    
    base_path = Path("data/exports")
    cutoff = datetime.now() - timedelta(days=days)
    deleted = []
    
    for category in ['detections', 'spectrum', 'reports', 'ml']:
        category_path = base_path / category
        if not category_path.exists():
            continue
        
        for file_path in category_path.iterdir():
            if file_path.is_file():
                mtime = datetime.fromtimestamp(file_path.stat().st_mtime)
                if mtime < cutoff:
                    # Archive before deletion
                    archive_path = base_path / "archived" / f"{datetime.now().strftime('%Y-%m')}" / file_path.name
                    archive_path.parent.mkdir(parents=True, exist_ok=True)
                    file_path.rename(archive_path)
                    deleted.append(str(archive_path))
    
    return {'deleted_count': len(deleted), 'deleted_files': deleted}
Storage Quotas
python
def get_storage_usage():
    """Get storage usage statistics"""
    
    base_path = Path("data/exports")
    usage = {}
    
    for category in ['detections', 'spectrum', 'reports', 'ml', 'archived']:
        category_path = base_path / category
        if category_path.exists():
            total_size = sum(f.stat().st_size for f in category_path.rglob('*') if f.is_file())
            file_count = len(list(category_path.rglob('*')))
            usage[category] = {
                'size_mb': total_size / (1024 * 1024),
                'file_count': file_count
            }
    
    total_size = sum(u['size_mb'] for u in usage.values())
    total_files = sum(u['file_count'] for u in usage.values())
    
    return {
        'categories': usage,
        'total_size_mb': total_size,
        'total_files': total_files,
        'quota_mb': 10240,  # 10 GB quota
        'usage_percent': (total_size / 10240) * 100
    }
Export Formats Details
CSV Export Options
python
def export_to_csv(data, output_path, options=None):
    """Export data to CSV with options"""
    
    import csv
    
    default_options = {
        'delimiter': ',',
        'encoding': 'utf-8',
        'include_header': True,
        'date_format': '%Y-%m-%d %H:%M:%S',
        'float_format': '%.6f'
    }
    
    options = {**default_options, **(options or {})}
    
    with open(output_path, 'w', newline='', encoding=options['encoding']) as f:
        writer = csv.writer(f, delimiter=options['delimiter'])
        
        if options['include_header']:
            writer.writerow(data[0].keys())
        
        for row in data:
            # Format values
            formatted_row = []
            for key, value in row.items():
                if isinstance(value, datetime):
                    formatted_row.append(value.strftime(options['date_format']))
                elif isinstance(value, float):
                    formatted_row.append(f"{value:{options['float_format']}}")
                else:
                    formatted_row.append(value)
            writer.writerow(formatted_row)
JSON Export Options
python
def export_to_json(data, output_path, options=None):
    """Export data to JSON with options"""
    
    import json
    
    default_options = {
        'indent': 2,
        'ensure_ascii': False,
        'sort_keys': False,
        'include_metadata': True
    }
    
    options = {**default_options, **(options or {})}
    
    export_data = data
    
    if options['include_metadata']:
        export_data = {
            'metadata': {
                'export_date': datetime.now().isoformat(),
                'export_version': '2.0.0',
                'record_count': len(data)
            },
            'data': data
        }
    
    with open(output_path, 'w', encoding='utf-8') as f:
        json.dump(export_data, f, **{k: v for k, v in options.items() 
                                      if k in ['indent', 'ensure_ascii', 'sort_keys']})
Excel Export Options
python
def export_to_excel(data_sheets, output_path):
    """Export multiple sheets to Excel"""
    
    import pandas as pd
    
    with pd.ExcelWriter(output_path, engine='openpyxl') as writer:
        for sheet_name, sheet_data in data_sheets.items():
            df = pd.DataFrame(sheet_data)
            df.to_excel(writer, sheet_name=sheet_name, index=False)
            
            # Auto-adjust column widths
            worksheet = writer.sheets[sheet_name]
            for column in df:
                column_width = max(df[column].astype(str).map(len).max(), len(column))
                column_idx = df.columns.get_loc(column)
                worksheet.column_dimensions[chr(65 + column_idx)].width = min(column_width + 2, 50)
Security
Export Access Control
python
from functools import wraps
from fastapi import HTTPException, Depends

def require_export_permission(export_type: str):
    """Decorator to check export permissions"""
    
    def decorator(func):
        @wraps(func)
        async def wrapper(user=Depends(get_current_user), *args, **kwargs):
            permissions = {
                'detections': ['admin', 'analyst', 'operator'],
                'spectrum': ['admin', 'analyst'],
                'reports': ['admin', 'analyst', 'operator'],
                'ml': ['admin', 'data_scientist']
            }
            
            required_roles = permissions.get(export_type, ['admin'])
            
            if user.role not in required_roles:
                raise HTTPException(403, f"Not authorized to export {export_type}")
            
            return await func(*args, **kwargs)
        
        return wrapper
    
    return decorator

# Usage
@router.get("/detections")
@require_export_permission("detections")
async def export_detections_endpoint():
    """Export detections (admin/analyst/operator only)"""
    pass
Encryption at Rest
python
from cryptography.fernet import Fernet
import base64

class EncryptedExport:
    """Handle encrypted exports"""
    
    def __init__(self, key=None):
        if key is None:
            key = Fernet.generate_key()
        self.cipher = Fernet(key)
        self.key = key
    
    def encrypt_file(self, input_path, output_path=None):
        """Encrypt export file"""
        
        if output_path is None:
            output_path = input_path.with_suffix(input_path.suffix + '.enc')
        
        with open(input_path, 'rb') as f:
            data = f.read()
        
        encrypted = self.cipher.encrypt(data)
        
        with open(output_path, 'wb') as f:
            f.write(encrypted)
        
        return output_path
    
    def decrypt_file(self, encrypted_path, output_path=None):
        """Decrypt export file"""
        
        if output_path is None:
            output_path = encrypted_path.with_suffix('')
        
        with open(encrypted_path, 'rb') as f:
            encrypted = f.read()
        
        decrypted = self.cipher.decrypt(encrypted)
        
        with open(output_path, 'wb') as f:
            f.write(decrypted)
        
        return output_path
Monitoring
Export Metrics
python
from prometheus_client import Counter, Histogram, Gauge

# Export metrics
exports_total = Counter('exports_total', 'Total exports created', ['format', 'category'])
export_size_bytes = Histogram('export_size_bytes', 'Export file sizes', buckets=[1e3, 1e4, 1e5, 1e6, 1e7, 1e8])
export_duration_seconds = Histogram('export_duration_seconds', 'Export generation time')
export_errors_total = Counter('export_errors_total', 'Export errors', ['error_type'])

# Track exports
def track_export(category, format, size_bytes, duration):
    exports_total.labels(format=format, category=category).inc()
    export_size_bytes.observe(size_bytes)
    export_duration_seconds.observe(duration)
Troubleshooting
Common Issues
Issue	Cause	Solution
Export failed	Disk full	Free up space or reduce export size
Corrupted export	Interrupted write	Re-export with verification
Wrong format	Incorrect parameters	Check format compatibility
Missing data	Date range error	Verify date parameters
Slow export	Large dataset	Use pagination or compression
Export Verification
python
def verify_export(file_path, expected_records=None):
    """Verify export file integrity"""
    
    file_path = Path(file_path)
    
    if not file_path.exists():
        return {'valid': False, 'error': 'File not found'}
    
    if file_path.stat().st_size == 0:
        return {'valid': False, 'error': 'Empty file'}
    
    # Verify based on extension
    if file_path.suffix == '.csv':
        import csv
        with open(file_path, 'r') as f:
            reader = csv.reader(f)
            rows = list(reader)
            record_count = len(rows) - 1  # Subtract header
            
    elif file_path.suffix == '.json':
        import json
        with open(file_path, 'r') as f:
            data = json.load(f)
            if 'data' in data:
                record_count = len(data['data'])
            else:
                record_count = len(data)
    
    result = {'valid': True, 'record_count': record_count}
    
    if expected_records and record_count != expected_records:
        result['valid'] = False
        result['error'] = f'Expected {expected_records} records, got {record_count}'
    
    return result
