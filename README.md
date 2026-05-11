drone-detector/data/iq/live/README.md - Live IQ Recordings Documentation

markdown
# Live IQ Recordings Directory

This directory stores live IQ recordings captured by the Drone Detection System during real-time operation. These recordings are used for forensic analysis, training data collection, and incident documentation.

## Directory Structure
data/iq/live/
├── README.md # This file
├── session_20240115_143022/ # Session-based recordings
│ ├── frame_000000.iq # Raw IQ data frame
│ ├── frame_000000.json # Frame metadata
│ ├── frame_000001.iq
│ ├── frame_000001.json
│ ├── ...
│ ├── session_metadata.json # Session information
│ └── detection_events.json # Detections during session
├── session_20240116_091533/
│ └── ...
├── session_20240117_162248/
│ └── ...
└── index.json # Global recording index

text

## Session Naming Convention

Sessions are named using the following format:
session_YYYYMMDD_HHMMSS

text

Where:
- `YYYY`: 4-digit year
- `MM`: 2-digit month (01-12)
- `DD`: 2-digit day (01-31)
- `HH`: 2-digit hour (00-23)
- `MM`: 2-digit minute (00-59)
- `SS`: 2-digit second (00-59)

Example: `session_20240115_143022` = January 15, 2024 at 14:30:22

## File Formats

### IQ Data Files (.iq)

| Property | Value |
|----------|-------|
| Format | Raw binary |
| Data Type | `np.complex64` |
| Sample Size | 8 bytes (4 bytes real + 4 bytes imag) |
| Endianness | Little-endian |
| No Header | Direct sample data only |

### Frame Metadata (.json)

Each IQ frame has a corresponding metadata file:

```json
{
  "frame_id": 0,
  "timestamp": "2024-01-15T14:30:22.123456Z",
  "sample_rate": 10000000,
  "center_frequency": 2440000000,
  "num_samples": 16384000,
  "duration_seconds": 1.6384,
  "gain_settings": {
    "lna_gain_db": 16,
    "vga_gain_db": 20,
    "amp_enabled": false
  },
  "antenna": {
    "port": 1,
    "type": "omnidirectional",
    "gain_dbi": 3.0
  },
  "trigger_source": "manual",
  "metadata": {
    "operator": "admin",
    "notes": "DJI Mavic 3 detected"
  }
}
Session Metadata (session_metadata.json)
json
{
  "session_id": "session_20240115_143022",
  "created_at": "2024-01-15T14:30:22.123456Z",
  "closed_at": "2024-01-15T14:35:45.678901Z",
  "duration_seconds": 323.555445,
  "num_frames": 198,
  "total_samples": 3244032000,
  "total_size_bytes": 25952256000,
  "sample_rate": 10000000,
  "center_frequency": 2440000000,
  "detection_count": 12,
  "hardware_config": {
    "device_type": "hackrf",
    "serial_number": "HACKRF001234",
    "firmware_version": "2024.02.1"
  },
  "operator": "admin",
  "description": "Drone detection incident - unauthorized DJI Mavic 3",
  "tags": ["incident", "unauthorized", "djia", "mavic_3"]
}
Detection Events (detection_events.json)
json
{
  "session_id": "session_20240115_143022",
  "detections": [
    {
      "detection_id": "det_20240115_143022_001",
      "timestamp": "2024-01-15T14:32:15.234567Z",
      "frame_id": 45,
      "sample_offset": 2345678,
      "drone_type": "DJI Mavic 3",
      "confidence": 0.95,
      "threat_level": "HIGH",
      "frequency": 2440000000,
      "signal_strength_dbm": -45.2,
      "snr_db": 28.5,
      "position": {
        "latitude": 37.7749,
        "longitude": -122.4194,
        "altitude_m": 100.0,
        "accuracy_m": 5.0
      },
      "remote_id": {
        "uas_id": "ABCD1234EFGH5678",
        "operator_id": "OP12345678",
        "valid": true
      }
    }
  ]
}
Global Index (index.json)
json
{
  "version": "2.0.0",
  "last_updated": "2024-01-15T14:35:45.678901Z",
  "total_sessions": 47,
  "total_recordings": 253,
  "total_size_bytes": 1234567890123,
  "total_duration_seconds": 12345.678,
  "sessions": [
    {
      "session_id": "session_20240115_143022",
      "created_at": "2024-01-15T14:30:22Z",
      "duration_seconds": 323.56,
      "num_frames": 198,
      "size_bytes": 25952256000,
      "detection_count": 12,
      "has_remote_id": true,
      "tags": ["incident", "unauthorized"]
    }
  ],
  "storage_stats": {
    "used_bytes": 1234567890123,
    "used_gb": 1234.57,
    "quota_gb": 5000,
    "free_gb": 3765.43,
    "oldest_session": "2023-12-01T08:00:00Z",
    "newest_session": "2024-01-15T14:35:45Z"
  }
}
Recording Sessions
Starting a Session
Sessions can be started in several ways:

1. Manual Recording
python
from infrastructure.signal_io.recorder import IQRecorder, RecordingConfig

recorder = IQRecorder(RecordingConfig(
    output_dir="data/iq/live",
    session_name="manual_recording"
))

recording_id = await recorder.start_recording(
    session_name="drone_incident_001",
    metadata={"operator": "admin", "reason": "suspicious drone"}
)
2. Trigger-Based Recording
python
# Automatic recording when drone detected
async def on_drone_detected(detection):
    if detection.confidence > 0.8:
        await recorder.start_recording(
            session_name=f"detection_{detection.id}",
            metadata={"trigger": "auto_detection", "confidence": detection.confidence}
        )
3. Scheduled Recording
python
# Schedule recording during high-risk hours
await recorder.schedule_recording(
    start_time=datetime.now().replace(hour=20, minute=0),
    duration_seconds=3600,  # 1 hour
    repeat_interval=86400,  # daily
    metadata={"purpose": "nighttime_monitoring"}
)
Stopping a Session
python
# Stop current recording
metadata = await recorder.stop_recording()

print(f"Session saved: {metadata.session_id}")
print(f"Duration: {metadata.duration_seconds:.2f}s")
print(f"File size: {metadata.file_size_bytes / 1024 / 1024:.2f} MB")
Loading Recorded Data
Load Full Session
python
import numpy as np
import json
from pathlib import Path

def load_session(session_path):
    """Load all frames from a session"""
    session_path = Path(session_path)
    
    # Load session metadata
    with open(session_path / "session_metadata.json", 'r') as f:
        session_meta = json.load(f)
    
    # Load all IQ frames
    frames = []
    frame_files = sorted(session_path.glob("frame_*.iq"))
    
    for iq_file in frame_files:
        # Load IQ data
        iq_data = np.fromfile(iq_file, dtype=np.complex64)
        
        # Load frame metadata
        json_file = iq_file.with_suffix('.json')
        with open(json_file, 'r') as f:
            frame_meta = json.load(f)
        
        frames.append({
            'data': iq_data,
            'metadata': frame_meta
        })
    
    return session_meta, frames

# Usage
session_meta, frames = load_session("data/iq/live/session_20240115_143022")
print(f"Loaded {len(frames)} frames, {session_meta['duration_seconds']:.2f}s")
Load Specific Time Range
python
def load_time_range(session_path, start_time, end_time):
    """Load frames within a specific time range"""
    session_path = Path(session_path)
    
    # Load all frame metadata first
    frames_data = []
    
    for json_file in session_path.glob("frame_*.json"):
        with open(json_file, 'r') as f:
            frame_meta = json.load(f)
        
        timestamp = datetime.fromisoformat(frame_meta['timestamp'])
        
        if start_time <= timestamp <= end_time:
            iq_file = json_file.with_suffix('.iq')
            iq_data = np.fromfile(iq_file, dtype=np.complex64)
            
            frames_data.append({
                'data': iq_data,
                'metadata': frame_meta
            })
    
    return frames_data
Load Detection Events
python
def get_detections_in_session(session_path):
    """Get all detection events from a session"""
    session_path = Path(session_path)
    
    with open(session_path / "detection_events.json", 'r') as f:
        events = json.load(f)
    
    return events['detections']

# Usage
detections = get_detections_in_session("data/iq/live/session_20240115_143022")
for det in detections:
    print(f"Drone: {det['drone_type']} at {det['timestamp']}")
Storage Management
Automatic Rotation
The system automatically manages storage with the following policies:

Policy	Value
Max File Size	1 GB per frame
Max Session Duration	1 hour
Max Total Storage	100 GB (configurable)
Retention Period	30 days
Auto-cleanup	Enabled
Manual Cleanup
python
from infrastructure.signal_io.recorder import IQRecorder

recorder = IQRecorder()

# Delete old sessions (older than 30 days)
await recorder.cleanup_old_sessions(days=30)

# Delete specific session
await recorder.delete_session("session_20240115_143022")

# Export session for archiving
await recorder.export_session("session_20240115_143022", format="zip")
Storage Monitoring
python
def get_storage_stats():
    """Get storage statistics"""
    import shutil
    
    iq_dir = Path("data/iq/live")
    total_size = sum(f.stat().st_size for f in iq_dir.rglob("*.iq"))
    total_gb = total_size / (1024**3)
    
    # Get disk usage
    disk_usage = shutil.disk_usage(iq_dir)
    
    return {
        'total_size_gb': total_gb,
        'disk_free_gb': disk_usage.free / (1024**3),
        'disk_used_gb': disk_usage.used / (1024**3),
        'disk_total_gb': disk_usage.total / (1024**3),
        'session_count': len(list(iq_dir.glob("session_*")))
    }
Export and Conversion
Export to Different Formats
python
from infrastructure.signal_io.file_reader import IQFileReaderFactory

async def export_session(session_path, output_format='npy'):
    """Export session to different format"""
    session_path = Path(session_path)
    
    for iq_file in session_path.glob("*.iq"):
        # Read IQ data
        reader = IQFileReaderFactory.get_reader(iq_file)
        async with reader:
            iq_data = await reader.read_all()
            sample_rate = reader.file_info.sample_rate
        
        # Export as NumPy
        if output_format == 'npy':
            output_file = iq_file.with_suffix('.npy')
            np.save(output_file, iq_data)
        
        # Export as CSV
        elif output_format == 'csv':
            output_file = iq_file.with_suffix('.csv')
            np.savetxt(output_file, 
                      np.column_stack((np.real(iq_data), np.imag(iq_data))),
                      delimiter=',',
                      header='I,Q')
        
        # Export as HDF5
        elif output_format == 'h5':
            import h5py
            output_file = iq_file.with_suffix('.h5')
            with h5py.File(output_file, 'w') as f:
                f.create_dataset('iq_data', data=iq_data)
                f.attrs['sample_rate'] = sample_rate
Generate Spectrograms from Recordings
python
import matplotlib.pyplot as plt
from scipy import signal

def generate_spectrogram(iq_file, output_file=None):
    """Generate spectrogram from IQ recording"""
    import matplotlib.pyplot as plt
    from scipy import signal
    
    # Load IQ data
    iq_data = np.fromfile(iq_file, dtype=np.complex64)
    
    # Load metadata
    json_file = iq_file.with_suffix('.json')
    with open(json_file, 'r') as f:
        metadata = json.load(f)
    
    # Compute spectrogram
    f, t, Sxx = signal.spectrogram(
        iq_data,
        fs=metadata['sample_rate'],
        nperseg=1024,
        noverlap=512
    )
    
    # Plot
    plt.figure(figsize=(12, 6))
    plt.pcolormesh(t, f / 1e6, 10 * np.log10(Sxx + 1e-12), shading='gouraud')
    plt.colorbar(label='Power (dB)')
    plt.ylabel('Frequency (MHz)')
    plt.xlabel('Time (s)')
    plt.title(f"Spectrogram - {iq_file.name}")
    
    if output_file:
        plt.savefig(output_file, dpi=150, bbox_inches='tight')
    else:
        plt.show()
Playback Recorded Sessions
python
from infrastructure.signal_io.playback import IQPlaybackEngine

async def playback_session(session_path, speed=1.0):
    """Playback a recorded session"""
    engine = IQPlaybackEngine()
    
    # Add all IQ files from session
    for iq_file in Path(session_path).glob("*.iq"):
        engine.add_file(iq_file)
    
    # Set playback speed
    await engine.set_speed(speed)
    
    # Start playback
    await engine.play()
    
    # Process frames in real-time
    async for chunk in engine:
        # Process chunk (e.g., run detection)
        process_chunk(chunk)
    
    await engine.stop()
Data Retention Policies
Retention Category	Duration	Action
Daily Recordings	7 days	Auto-delete
Incident Recordings	90 days	Manual delete only
Training Data	180 days	Archive to cold storage
False Positives	30 days	Auto-delete
Calibration Data	365 days	Keep for reference
Security and Privacy
Data Sensitivity Levels
Level	Description	Access	Retention
Public	No sensitive data	All users	30 days
Internal	Operational data	Authorized users	90 days
Confidential	Incident data	Security team	365 days
Restricted	Remote ID data	Compliance required	90 days
Data Anonymization
python
def anonymize_session(session_path):
    """Remove personally identifiable information from session"""
    # Remove Remote ID data
    with open(session_path / "detection_events.json", 'r') as f:
        events = json.load(f)
    
    for detection in events['detections']:
        if 'remote_id' in detection:
            # Anonymize UAS ID
            detection['remote_id']['uas_id'] = hash(detection['remote_id']['uas_id'])
            detection['remote_id']['operator_id'] = hash(detection['remote_id']['operator_id'])
    
    # Save anonymized version
    with open(session_path / "detection_events_anonymized.json", 'w') as f:
        json.dump(events, f, indent=2)
Troubleshooting
Common Issues
Issue	Cause	Solution
Insufficient disk space	Too many recordings	Run cleanup or increase quota
Corrupted IQ file	Incomplete write	Re-record or restore from backup
Missing metadata	Recording interrupted	Check session metadata integrity
Slow playback	Large file size	Reduce sample rate or use chunking
Recovery Procedures
python
def repair_session(session_path):
    """Attempt to repair a corrupted session"""
    session_path = Path(session_path)
    
    # Check for missing frame files
    expected_frames = len(list(session_path.glob("frame_*.json")))
    actual_frames = len(list(session_path.glob("frame_*.iq")))
    
    if expected_frames != actual_frames:
        print(f"Missing {expected_frames - actual_frames} IQ files")
        
        # Regenerate missing metadata
        for json_file in session_path.glob("frame_*.json"):
            iq_file = json_file.with_suffix('.iq')
            if not iq_file.exists():
                print(f"Missing IQ file for {json_file.name}")
                # Create empty placeholder or skip
Performance Optimization
Memory-Mapped Reading
python
def load_large_session_mmap(session_path):
    """Load large session using memory mapping"""
    session_path = Path(session_path)
    
    frames = []
    for iq_file in sorted(session_path.glob("frame_*.iq")):
        # Use memory mapping for large files
        iq_data = np.memmap(iq_file, dtype=np.complex64, mode='r')
        frames.append(iq_data)
    
    return frames
Batch Processing
python
def process_session_batch(session_path, batch_size=10):
    """Process session in batches to manage memory"""
    session_path = Path(session_path)
    
    iq_files = sorted(session_path.glob("frame_*.iq"))
    
    for i in range(0, len(iq_files), batch_size):
        batch = iq_files[i:i+batch_size]
        
        # Load batch
        batch_data = []
        for iq_file in batch:
            data = np.fromfile(iq_file, dtype=np.complex64)
            batch_data.append(data)
        
        # Process batch
        for data in batch_data:
            process_chunk(data)
        
        # Clear memory
        del batch_data
Command Line Interface
bash
# List all sessions
python -m infrastructure.signal_io.recorder --list

# Show session info
python -m infrastructure.signal_io.recorder --info session_20240115_143022

# Export session
python -m infrastructure.signal_io.recorder --export session_20240115_143022 --format npy

# Playback session
python -m infrastructure.signal_io.playback --session session_20240115_143022 --speed 2.0

# Clean old sessions
python -m infrastructure.signal_io.recorder --cleanup --days 30
