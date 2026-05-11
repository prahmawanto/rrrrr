drone-detector/data/exports/reports/README.md - Reports Exports Documentation

markdown
# Reports Exports Directory

This directory contains generated reports from the Drone Detection System, including daily summaries, weekly trends, monthly analytics, incident reports, and custom analysis reports. These reports provide comprehensive insights into drone detection activities, threat patterns, and system performance.

## Directory Structure
data/exports/reports/
├── README.md # This file
├── daily/ # Daily reports
│ ├── daily_report_20240115.md
│ ├── daily_report_20240115.pdf
│ ├── daily_report_20240115.html
│ ├── daily_report_20240116.md
│ ├── daily_report_20240116.pdf
│ └── daily_report_20240116.html
├── weekly/ # Weekly reports
│ ├── weekly_report_2024_W03.md
│ ├── weekly_report_2024_W03.pdf
│ ├── weekly_report_2024_W03.html
│ ├── weekly_report_2024_W04.md
│ └── weekly_report_2024_W04.pdf
├── monthly/ # Monthly reports
│ ├── monthly_report_2024_01.md
│ ├── monthly_report_2024_01.pdf
│ ├── monthly_report_2024_01.html
│ ├── monthly_report_2024_01.xlsx
│ ├── monthly_report_2024_02.md
│ └── monthly_report_2024_02.pdf
├── quarterly/ # Quarterly reports
│ ├── quarterly_report_2024_Q1.md
│ ├── quarterly_report_2024_Q1.pdf
│ └── quarterly_report_2024_Q1.pptx
├── annual/ # Annual reports
│ ├── annual_report_2023.md
│ ├── annual_report_2023.pdf
│ └── annual_report_2023.pptx
├── incident/ # Incident-specific reports
│ ├── incident_report_20240115.md
│ ├── incident_report_20240115.pdf
│ ├── incident_report_20240115_evidence.zip
│ ├── incident_report_20240120.md
│ └── incident_report_20240120.pdf
├── custom/ # Custom user-generated reports
│ ├── custom_report_20240115_143022.pdf
│ ├── custom_report_20240115_143022.json
│ ├── threat_analysis_20240115.pdf
│ └── hotspot_analysis_20240115.pdf
├── templates/ # Report templates
│ ├── daily_template.md
│ ├── weekly_template.md
│ ├── monthly_template.md
│ ├── incident_template.md
│ └── custom_template.html
├── attachments/ # Report attachments
│ ├── charts/
│ │ ├── trend_chart_20240115.png
│ │ ├── distribution_chart_20240115.png
│ │ └── heatmap_20240115.png
│ ├── data/
│ │ ├── detection_data_20240115.csv
│ │ └── alert_data_20240115.json
│ └── images/
│ ├── drone_icon.png
│ └── logo.png
└── index.json # Report index and metadata

text

## Naming Convention

Report files follow a consistent naming pattern:

| Report Type | Pattern | Example |
|-------------|---------|---------|
| Daily | `daily_report_YYYYMMDD.format` | `daily_report_20240115.pdf` |
| Weekly | `weekly_report_YYYY_WWW.format` | `weekly_report_2024_W03.pdf` |
| Monthly | `monthly_report_YYYY_MM.format` | `monthly_report_2024_01.pdf` |
| Quarterly | `quarterly_report_YYYY_QX.format` | `quarterly_report_2024_Q1.pdf` |
| Annual | `annual_report_YYYY.format` | `annual_report_2023.pdf` |
| Incident | `incident_report_YYYYMMDD.format` | `incident_report_20240115.pdf` |
| Custom | `custom_report_YYYYMMDD_HHMMSS.format` | `custom_report_20240115_143022.pdf` |

## Report Formats

### Markdown Format (.md)

Human-readable text format suitable for version control and editing.

**Structure:**
```markdown
# Daily Drone Detection Report
**Date:** 2024-01-15
**Generated:** 2024-01-15T23:59:59Z
**Period:** 2024-01-15 00:00:00 - 2024-01-15 23:59:59

## Executive Summary

During the reporting period, the Drone Detection System recorded **1,247 detections** across **89 unique drones**. 

### Key Metrics
- **Total Detections:** 1,247
- **Active Threats:** 342 (27.4%)
- **High Confidence Detections:** 456
- **Geofence Violations:** 12

## Detection Statistics

### By Threat Level
| Threat Level | Count | Percentage |
|--------------|-------|------------|
| HIGH | 342 | 27.4% |
| MEDIUM | 567 | 45.5% |
| LOW | 338 | 27.1% |

### By Drone Type
| Drone Type | Count | Percentage |
|------------|-------|------------|
| DJI Mavic 3 | 456 | 36.6% |
| FPV Analog | 234 | 18.8% |
| DJI Mini 3 | 189 | 15.2% |
| Autel EVO II | 123 | 9.9% |
| Skydio 2 | 78 | 6.3% |
| Unknown | 167 | 13.4% |

## Temporal Analysis

### Peak Detection Hours
- **16:00 - 17:00:** 234 detections
- **15:00 - 16:00:** 201 detections
- **17:00 - 18:00:** 189 detections

### Detections by Day of Week (Weekly Report)
| Day | Count |
|-----|-------|
| Monday | 1,234 |
| Tuesday | 1,189 |
| Wednesday | 1,345 |
| Thursday | 1,456 |
| Friday | 1,567 |
| Saturday | 1,234 |
| Sunday | 1,089 |

## Geographic Distribution

### Top 5 Detection Locations
| Location | Count | Threat Level |
|----------|-------|--------------|
| Downtown Area | 234 | HIGH |
| Airport Buffer Zone | 156 | CRITICAL |
| Industrial Park | 145 | MEDIUM |
| Residential Area | 123 | LOW |
| Sports Stadium | 98 | HIGH |

### Geofence Violations
| Zone | Violations | Action Taken |
|------|------------|--------------|
| Airport No-Fly Zone | 8 | Alerted Authorities |
| Military Base Buffer | 3 | Escalated to Security |
| Power Plant | 1 | Investigated |

## Alert Summary

- **Total Alerts Generated:** 45
- **Critical Alerts:** 3
- **High Alerts:** 12
- **Medium Alerts:** 18
- **Low Alerts:** 12

### Response Metrics
- **Average Response Time:** 2.3 minutes
- **Alerts Acknowledged:** 42 (93.3%)
- **Alerts Resolved:** 38 (84.4%)

## System Performance

| Metric | Value |
|--------|-------|
| System Uptime | 99.98% |
| Detection Latency (Avg) | 45 ms |
| False Positive Rate | 3.2% |
| Processing Throughput | 1,234 detections/hour |

## Recommendations

1. **Increase monitoring during peak hours (15:00-18:00)**
2. **Review airport buffer zone security measures**
3. **Update drone signature database for unknown types**
4. **Schedule maintenance for antenna array**

## Appendix

- Full detection data available in attached CSV
- Spectrum snapshots available in attachments
- Alert details available on request
PDF Format (.pdf)
Professionally formatted reports suitable for distribution and printing.

Features:

Page numbering

Table of contents

Cover page with logo

Professional typography

Embedded charts and graphs

Hyperlinks for navigation

Digital signatures (optional)

Watermark for confidential reports

HTML Format (.html)
Web-friendly reports with interactive elements.

Features:

Responsive design

Interactive charts (Chart.js)

Filterable tables

Collapsible sections

Print-friendly CSS

Embedded JavaScript for interactivity

Mobile-optimized viewing

Excel Format (.xlsx)
Data-rich reports for further analysis.

Sheets:

Summary - Key metrics and KPIs

Detections - Full detection data

Statistics - Aggregated statistics

Timeline - Time-series data

Locations - Geographic distribution

Charts - Embedded visualizations

PowerPoint Format (.pptx)
Presentation-ready reports for meetings.

Slides:

Cover slide

Executive summary

Key metrics dashboard

Detection trends

Threat distribution

Geographic heatmap

Alert summary

Performance metrics

Recommendations

Appendix

Report Generation
Daily Report Generation
python
async def generate_daily_report(date=None):
    """Generate daily report for specified date"""
    
    from datetime import datetime, timedelta
    
    if date is None:
        date = datetime.now() - timedelta(days=1)
    
    start_date = datetime(date.year, date.month, date.day, 0, 0, 0)
    end_date = start_date + timedelta(days=1)
    
    # Collect data
    detections = await get_detections_by_date_range(start_date, end_date)
    alerts = await get_alerts_by_date_range(start_date, end_date)
    metrics = await get_metrics_by_date_range(start_date, end_date)
    
    # Generate report content
    report_data = {
        'report_type': 'daily',
        'date': date.strftime('%Y-%m-%d'),
        'period_start': start_date.isoformat(),
        'period_end': end_date.isoformat(),
        'detections': detections,
        'alerts': alerts,
        'metrics': metrics,
        'statistics': calculate_statistics(detections, alerts),
        'charts': await generate_report_charts(detections)
    }
    
    # Generate in multiple formats
    reports = {}
    
    # Markdown
    md_path = f"data/exports/reports/daily/daily_report_{date.strftime('%Y%m%d')}.md"
    await generate_markdown_report(report_data, md_path)
    reports['markdown'] = md_path
    
    # PDF
    pdf_path = f"data/exports/reports/daily/daily_report_{date.strftime('%Y%m%d')}.pdf"
    await convert_markdown_to_pdf(md_path, pdf_path)
    reports['pdf'] = pdf_path
    
    # HTML
    html_path = f"data/exports/reports/daily/daily_report_{date.strftime('%Y%m%d')}.html"
    await generate_html_report(report_data, html_path)
    reports['html'] = html_path
    
    # Update index
    await update_report_index(report_data, reports)
    
    return reports
Weekly Report Generation
python
async def generate_weekly_report(year, week):
    """Generate weekly report for specified week"""
    
    from datetime import datetime, timedelta
    
    # Calculate week dates
    start_date = datetime.strptime(f'{year}-W{week-1}-1', '%Y-W%W-%w')
    end_date = start_date + timedelta(days=7)
    
    # Collect weekly data
    detections = await get_detections_by_date_range(start_date, end_date)
    
    # Calculate week-over-week changes
    prev_week_start = start_date - timedelta(days=7)
    prev_week_end = start_date
    prev_detections = await get_detections_by_date_range(prev_week_start, prev_week_end)
    
    # Generate report
    report_data = {
        'report_type': 'weekly',
        'year': year,
        'week': week,
        'period_start': start_date.isoformat(),
        'period_end': end_date.isoformat(),
        'detections': detections,
        'previous_week': {
            'detections': prev_detections,
            'count': len(prev_detections)
        },
        'statistics': calculate_weekly_statistics(detections, prev_detections),
        'trends': calculate_weekly_trends(detections),
        'highlights': generate_weekly_highlights(detections)
    }
    
    # Generate report files
    reports = {}
    
    for fmt in ['md', 'pdf', 'html', 'xlsx']:
        output_path = f"data/exports/reports/weekly/weekly_report_{year}_W{week:02d}.{fmt}"
        await generate_report(report_data, output_path, format=fmt)
        reports[fmt] = output_path
    
    return reports
Incident Report Generation
python
async def generate_incident_report(incident_id, detection_ids, alert_ids):
    """Generate incident-specific report"""
    
    from datetime import datetime
    
    # Fetch incident data
    detections = await get_detections_by_ids(detection_ids)
    alerts = await get_alerts_by_ids(alert_ids)
    incident_details = await get_incident_details(incident_id)
    
    # Generate evidence package
    evidence_files = await package_evidence(detections, alerts, incident_id)
    
    report_data = {
        'report_type': 'incident',
        'incident_id': incident_id,
        'report_date': datetime.now().isoformat(),
        'incident_details': incident_details,
        'detections': detections,
        'alerts': alerts,
        'timeline': build_incident_timeline(detections, alerts),
        'evidence': evidence_files,
        'analysis': analyze_incident(detections, alerts),
        'recommendations': generate_recommendations(incident_details)
    }
    
    # Generate report
    md_path = f"data/exports/reports/incident/incident_report_{incident_id}.md"
    await generate_incident_markdown(report_data, md_path)
    
    pdf_path = f"data/exports/reports/incident/incident_report_{incident_id}.pdf"
    await convert_markdown_to_pdf(md_path, pdf_path)
    
    # Create evidence archive
    zip_path = f"data/exports/reports/incident/incident_report_{incident_id}_evidence.zip"
    await create_evidence_archive(evidence_files, zip_path)
    
    return {
        'report': pdf_path,
        'markdown': md_path,
        'evidence': zip_path
    }
Custom Report Generation
python
async def generate_custom_report(filters, date_range, metrics, formats=['pdf']):
    """Generate custom report with user-specified parameters"""
    
    from datetime import datetime
    
    # Apply filters and get data
    detections = await get_detections_with_filters(filters, date_range)
    alerts = await get_alerts_with_filters(filters, date_range)
    performance = await get_performance_metrics(date_range)
    
    report_data = {
        'report_type': 'custom',
        'export_id': datetime.now().strftime('%Y%m%d_%H%M%S'),
        'export_date': datetime.now().isoformat(),
        'filters': filters,
        'date_range': {
            'start': date_range['start'].isoformat(),
            'end': date_range['end'].isoformat()
        },
        'metrics': metrics,
        'detections': detections,
        'alerts': alerts,
        'performance': performance,
        'statistics': calculate_custom_statistics(detections, alerts, metrics)
    }
    
    reports = {}
    
    for fmt in formats:
        output_path = f"data/exports/reports/custom/custom_report_{report_data['export_id']}.{fmt}"
        await generate_report(report_data, output_path, format=fmt)
        reports[fmt] = output_path
    
    return reports
Report Templates
Daily Report Template (Markdown)
markdown
# Daily Drone Detection Report
**Date:** {{ date }}
**Generated:** {{ generated_at }}
**Period:** {{ period_start }} - {{ period_end }}

## Executive Summary
{{ executive_summary }}

## Key Metrics
| Metric | Value | Change |
|--------|-------|--------|
| Total Detections | {{ total_detections }} | {{ detection_change }} |
| Active Threats | {{ active_threats }} | {{ threat_change }} |
| High Confidence | {{ high_confidence }} | {{ confidence_change }} |
| Geofence Violations | {{ geofence_violations }} | {{ geofence_change }} |

## Detection Statistics
### By Threat Level
{{ threat_level_table }}

### By Drone Type
{{ drone_type_table }}

## Temporal Analysis
### Hourly Distribution
{{ hourly_chart }}

### Peak Hours
{{ peak_hours }}

## Geographic Distribution
### Top Locations
{{ location_table }}

### Geofence Violations
{{ violation_table }}

## Alert Summary
{{ alert_summary }}

### Response Metrics
{{ response_metrics }}

## System Performance
{{ performance_table }}

## Recommendations
{{ recommendations }}

## Appendix
- Full data: [detections_{{ date }}.csv](attachments/detections_{{ date }}.csv)
- Spectrum data: [spectrum_{{ date }}.json](attachments/spectrum_{{ date }}.json)
Incident Report Template
markdown
# Incident Report: {{ incident_id }}
**Date:** {{ report_date }}
**Classification:** {{ classification }}
**Severity:** {{ severity }}

## Incident Overview
- **Time of Incident:** {{ incident_time }}
- **Duration:** {{ duration }}
- **Location:** {{ location }}
- **Drone Type:** {{ drone_type }}
- **Threat Level:** {{ threat_level }}

## Timeline of Events
{{ timeline }}

## Detection Details
{{ detection_table }}

## Alert Details
{{ alert_table }}

## Evidence Summary
{{ evidence_list }}

## Analysis
### Root Cause Analysis
{{ root_cause }}

### Impact Assessment
{{ impact_assessment }}

### Contributing Factors
{{ contributing_factors }}

## Response Actions
| Time | Action | Actor | Result |
|------|--------|-------|--------|
{{ response_actions }}

## Recommendations
{{ recommendations }}

## Lessons Learned
{{ lessons_learned }}

## Sign-off
- **Prepared by:** {{ prepared_by }}
- **Reviewed by:** {{ reviewed_by }}
- **Approved by:** {{ approved_by }}
- **Date:** {{ signoff_date }}
Report API
REST Endpoints
python
from fastapi import APIRouter, Query, Body, Depends
from datetime import datetime

router = APIRouter(prefix="/api/reports", tags=["reports"])

@router.get("/daily/{date}")
async def get_daily_report(
    date: str = Path(..., description="Date in YYYYMMDD format"),
    format: str = Query("pdf", regex="^(md|pdf|html)$"),
    user = Depends(get_current_user)
):
    """Download daily report"""
    
    report_path = Path(f"data/exports/reports/daily/daily_report_{date}.{format}")
    
    if not report_path.exists():
        raise HTTPException(404, "Report not found")
    
    return FileResponse(report_path, filename=report_path.name)

@router.post("/generate")
async def generate_report_endpoint(
    report_type: str = Body(..., regex="^(daily|weekly|monthly|incident|custom)$"),
    parameters: dict = Body(...),
    formats: list = Body(["pdf"]),
    user = Depends(require_permission("reports:generate"))
):
    """Generate new report"""
    
    if report_type == 'daily':
        result = await generate_daily_report(**parameters)
    elif report_type == 'weekly':
        result = await generate_weekly_report(**parameters)
    elif report_type == 'monthly':
        result = await generate_monthly_report(**parameters)
    elif report_type == 'incident':
        result = await generate_incident_report(**parameters)
    else:
        result = await generate_custom_report(**parameters, formats=formats)
    
    return {
        "message": "Report generated successfully",
        "report_id": result.get('report_id'),
        "download_urls": result
    }

@router.get("/list")
async def list_reports(
    report_type: Optional[str] = Query(None, regex="^(daily|weekly|monthly|incident|custom)$"),
    start_date: Optional[datetime] = Query(None),
    end_date: Optional[datetime] = Query(None),
    limit: int = Query(50, le=100),
    user = Depends(get_current_user)
):
    """List available reports"""
    
    reports = await scan_reports_directory(
        report_type=report_type,
        start_date=start_date,
        end_date=end_date,
        limit=limit
    )
    
    return {"reports": reports, "total": len(reports)}
Report Automation
Scheduled Report Generation
python
import schedule
import asyncio

def schedule_reports():
    """Schedule automated report generation"""
    
    # Daily report at 00:30
    schedule.every().day.at("00:30").do(
        lambda: asyncio.run(generate_daily_report())
    )
    
    # Weekly report on Monday at 01:00
    schedule.every().monday.at("01:00").do(
        lambda: asyncio.run(generate_weekly_report())
    )
    
    # Monthly report on 1st at 02:00
    schedule.every().month.at("02:00").do(
        lambda: asyncio.run(generate_monthly_report())
    )
    
    # Quarterly report on Jan 1, Apr 1, Jul 1, Oct 1 at 03:00
    schedule.every().quarter.at("03:00").do(
        lambda: asyncio.run(generate_quarterly_report())
    )
    
    # Annual report on Jan 1 at 04:00
    schedule.every().year.at("04:00").do(
        lambda: asyncio.run(generate_annual_report())
    )
Report Distribution
python
async def distribute_report(report_path, recipients, channels=['email']):
    """Distribute report to recipients"""
    
    from email.mime.multipart import MIMEMultipart
    from email.mime.text import MIMEText
    from email.mime.base import MIMEBase
    
    results = []
    
    for channel in channels:
        if channel == 'email':
            for recipient in recipients:
                result = await send_report_email(report_path, recipient)
                results.append(result)
        
        elif channel == 'slack':
            result = await post_report_to_slack(report_path, recipients)
            results.append(result)
        
        elif channel == 'webhook':
            result = await send_report_webhook(report_path, recipients)
            results.append(result)
    
    return {
        'report': str(report_path),
        'recipients': recipients,
        'channels': channels,
        'results': results
    }
Report Analysis Tools
Compare Reports
python
def compare_reports(report1_path, report2_path):
    """Compare two reports"""
    
    import json
    
    with open(report1_path, 'r') as f:
        report1 = json.load(f)
    
    with open(report2_path, 'r') as f:
        report2 = json.load(f)
    
    comparison = {
        'detection_change': report2['statistics']['total_detections'] - report1['statistics']['total_detections'],
        'threat_level_changes': {},
        'drone_type_changes': {},
        'performance_changes': {}
    }
    
    # Compare threat levels
    for level in ['HIGH', 'MEDIUM', 'LOW', 'CRITICAL']:
        comparison['threat_level_changes'][level] = {
            'previous': report1['statistics']['by_threat_level'].get(level, 0),
            'current': report2['statistics']['by_threat_level'].get(level, 0),
            'change': report2['statistics']['by_threat_level'].get(level, 0) - report1['statistics']['by_threat_level'].get(level, 0)
        }
    
    return comparison
Extract Report Data
python
def extract_report_data(report_path):
    """Extract structured data from report"""
    
    import re
    import json
    
    with open(report_path, 'r') as f:
        content = f.read()
    
    # Extract key metrics using regex
    metrics = {}
    
    patterns = {
        'total_detections': r'Total Detections[:\s]+([0-9,]+)',
        'active_threats': r'Active Threats[:\s]+([0-9,]+)',
        'avg_confidence': r'Average Confidence[:\s]+([0-9.]+)%',
        'system_uptime': r'System Uptime[:\s]+([0-9.]+)%'
    }
    
    for key, pattern in patterns.items():
        match = re.search(pattern, content)
        if match:
            metrics[key] = match.group(1).replace(',', '')
    
    # Extract table data
    tables = extract_tables_from_markdown(content)
    
    return {
        'metrics': metrics,
        'tables': tables,
        'raw_content': content
    }
Report Storage
Retention Policy
Report Type	Retention	Archive	Format
Daily	90 days	Monthly	PDF + MD
Weekly	180 days	Quarterly	PDF + MD
Monthly	3 years	Annually	PDF + XLSX
Quarterly	5 years	Permanent	PDF + PPTX
Annual	Permanent	Permanent	PDF + XLSX
Incident	Permanent	Permanent	PDF + ZIP
Custom	User-defined	User-defined	Configurable
Storage Limits
python
def check_report_storage():
    """Check report storage usage"""
    
    reports_dir = Path("data/exports/reports")
    total_size = sum(f.stat().st_size for f in reports_dir.rglob("*") if f.is_file())
    size_gb = total_size / (1024 ** 3)
    
    limits = {
        'warning': 2,     # 2 GB warning
        'critical': 5,    # 5 GB critical
        'max': 10         # 10 GB maximum
    }
    
    return {
        'size_gb': size_gb,
        'file_count': len(list(reports_dir.rglob("*"))),
        'status': 'ok' if size_gb < limits['warning'] else 'warning' if size_gb < limits['critical'] else 'critical'
    }
Troubleshooting
Common Issues
Issue	Cause	Solution
Missing data	Date range incorrect	Verify report parameters
Generation timeout	Too much data	Reduce date range or add filters
PDF conversion failed	Missing dependencies	Install required packages
Chart missing	Data format error	Check data structure
Large file size	Embedded images	Compress images or use references
Report Regeneration
python
async def regenerate_report(report_id, report_type):
    """Regenerate a report"""
    
    # Find original report parameters
    params = await get_report_parameters(report_id, report_type)
    
    if not params:
        return {'error': 'Report parameters not found'}
    
    # Regenerate report
    if report_type == 'daily':
        result = await generate_daily_report(**params)
    elif report_type == 'weekly':
        result = await generate_weekly_report(**params)
    elif report_type == 'monthly':
        result = await generate_monthly_report(**params)
    else:
        result = await generate_custom_report(**params)
    
    return {
        'message': 'Report regenerated successfully',
        'new_report': result
    }
Best Practices
Report Configuration
python
# Recommended report settings
REPORT_CONFIG = {
    'daily': {
        'time': '00:30',
        'formats': ['md', 'pdf', 'html'],
        'include_attachments': True,
        'compression': False,
        'retention_days': 90
    },
    'weekly': {
        'day': 'Monday',
        'time': '01:00',
        'formats': ['md', 'pdf', 'xlsx'],
        'include_attachments': True,
        'compression': True,
        'retention_days': 180
    },
    'monthly': {
        'day': 1,
        'time': '02:00',
        'formats': ['pdf', 'xlsx', 'pptx'],
        'include_attachments': True,
        'compression': True,
        'retention_years': 3
    }
}
Quality Assurance
python
def validate_report(report_path):
    """Validate report quality"""
    
    checks = {
        'file_exists': report_path.exists(),
        'file_not_empty': report_path.stat().st_size > 0,
        'contains_data': check_report_has_data(report_path),
        'valid_format': check_report_format(report_path),
        'no_placeholders': not check_for_placeholders(report_path)
    }
    
    quality_score = sum(checks.values()) / len(checks) * 100
    
    return {
        'valid': quality_score == 100,
        'checks': checks,
        'quality_score': quality_score,
        'issues': [k for k, v in checks.items() if not v]
    }
