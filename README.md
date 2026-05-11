drone-detector/data/iq/replay/README.md - IQ Replay Dataset Documentation
Here's the complete README documentation for the IQ replay dataset directory.

markdown
# IQ Replay Dataset Directory

This directory contains pre-recorded IQ datasets for replay testing of the Drone Detection System. These datasets enable reproducible testing, algorithm development, and system validation without requiring live drone flights or hardware.

## Directory Structure
data/iq/replay/
├── README.md # This file
├── dji_mavic_2.4g/ # DJI Mavic 2.4 GHz recordings
│ ├── recording_001.iq
│ ├── recording_001.json
│ ├── recording_002.iq
│ ├── recording_002.json
│ ├── ...
│ └── dataset_info.json
├── dji_mavic_5.8g/ # DJI Mavic 5.8 GHz recordings
│ ├── recording_001.iq
│ ├── ...
│ └── dataset_info.json
├── dji_mini_2.4g/ # DJI Mini 2.4 GHz recordings
│ ├── recording_001.iq
│ ├── ...
│ └── dataset_info.json
├── fpv_analog_5.8g/ # FPV Analog 5.8 GHz recordings
│ ├── recording_001.iq
│ ├── ...
│ └── dataset_info.json
├── fpv_digital_5.8g/ # FPV Digital 5.8 GHz recordings
│ ├── recording_001.iq
│ ├── ...
│ └── dataset_info.json
├── autel_evo_2.4g/ # Autel EVO 2.4 GHz recordings
│ ├── recording_001.iq
│ ├── ...
│ └── dataset_info.json
├── skydio_2_2.4g/ # Skydio 2 2.4 GHz recordings
│ ├── recording_001.iq
│ ├── ...
│ └── dataset_info.json
├── noise_only/ # Background noise recordings
│ ├── urban_noise.iq
│ ├── suburban_noise.iq
│ ├── rural_noise.iq
│ ├── industrial_noise.iq
│ ├── office_noise.iq
│ └── dataset_info.json
├── interference/ # Interference recordings
│ ├── wifi_2.4g.iq
│ ├── wifi_5g.iq
│ ├── bluetooth.iq
│ ├── microwave.iq
│ ├── radar.iq
│ └── dataset_info.json
├── mixed_scenarios/ # Combined scenarios
│ ├── drone_with_wifi.iq
│ ├── multiple_drones.iq
│ ├── fading_environment.iq
│ └── dataset_info.json
└── index.json # Global dataset index

text

## Dataset Overview

### Drone Type Datasets

| Dataset | Drone Type | Frequency | Duration | Files | Total Size |
|---------|------------|-----------|----------|-------|------------|
| `dji_mavic_2.4g` | DJI Mavic 3 | 2.4 GHz | 600s | 20 | 4.8 GB |
| `dji_mavic_5.8g` | DJI Mavic 3 | 5.8 GHz | 600s | 20 | 9.6 GB |
| `dji_mini_2.4g` | DJI Mini 3 | 2.4 GHz | 300s | 10 | 2.4 GB |
| `fpv_analog_5.8g` | FPV Analog | 5.8 GHz | 300s | 10 | 2.4 GB |
| `fpv_digital_5.8g` | FPV Digital | 5.8 GHz | 300s | 10 | 4.8 GB |
| `autel_evo_2.4g` | Autel EVO II | 2.4 GHz | 300s | 10 | 2.4 GB |
| `skydio_2_2.4g` | Skydio 2 | 2.4 GHz | 300s | 10 | 2.4 GB |

### Environment Datasets

| Dataset | Environment | Noise Floor | Duration | Files |
|---------|-------------|-------------|----------|-------|
| `noise_only/urban` | Urban | -85 dBm | 300s | 5 |
| `noise_only/suburban` | Suburban | -95 dBm | 300s | 5 |
| `noise_only/rural` | Rural | -105 dBm | 300s | 5 |
| `noise_only/industrial` | Industrial | -80 dBm | 300s | 5 |
| `noise_only/office` | Office | -90 dBm | 300s | 5 |

### Interference Datasets

| Dataset | Interference Type | Frequency | Duration | Files |
|---------|------------------|-----------|----------|-------|
| `interference/wifi_2.4g` | 802.11n | 2.4 GHz | 300s | 5 |
| `interference/wifi_5g` | 802.11ac | 5 GHz | 300s | 5 |
| `interference/bluetooth` | BLE | 2.4 GHz | 300s | 5 |
| `interference/microwave` | Microwave Oven | 2.4 GHz | 300s | 5 |
| `interference/radar` | Weather Radar | 5.6 GHz | 300s | 5 |

### Mixed Scenarios

| Dataset | Description | Duration | Files |
|---------|-------------|----------|-------|
| `mixed_scenarios/drone_with_wifi` | Drone + WiFi interference | 300s | 10 |
| `mixed_scenarios/multiple_drones` | Multiple drones simultaneous | 300s | 10 |
| `mixed_scenarios/fading_environment` | Multipath fading simulation | 300s | 10 |

## File Formats

### Recording File (.iq)

Standard IQ binary format:

| Property | Value |
|----------|-------|
| Format | Raw binary |
| Data Type | `np.complex64` |
| Sample Size | 8 bytes |
| Endianness | Little-endian |

### Recording Metadata (.json)

```json
{
  "recording_id": "recording_001",
  "dataset": "dji_mavic_2.4g",
  "drone_type": "DJI Mavic 3",
  "manufacturer": "DJI",
  "frequency_hz": 2412000000,
  "sample_rate": 10000000,
  "duration_seconds": 30.0,
  "num_samples": 300000000,
  "snr_db": 15.0,
  "modulation": "OFDM",
  "bandwidth_hz": 20000000,
  "recording_date": "2024-01-15T10:30:00Z",
  "source": "field_recording",
  "location": {
    "latitude": 37.7749,
    "longitude": -122.4194
  },
  "equipment": {
    "sdr": "HackRF One",
    "antenna": "2.4 GHz Yagi",
    "gain_db": 20
  },
  "weather": {
    "temperature_c": 22,
    "humidity_pct": 45,
    "wind_speed_ms": 3.5
  },
  "validated": true,
  "validation_confidence": 0.95
}
Dataset Info (dataset_info.json)
json
{
  "dataset_name": "dji_mavic_2.4g",
  "version": "2.0.0",
  "description": "DJI Mavic 3 OcuSync 4.0 recordings at 2.4 GHz",
  "drone_type": "DJI Mavic 3",
  "manufacturer": "DJI",
  "frequency_band": "2.4 GHz ISM",
  "center_frequency": 2412000000,
  "sample_rate": 10000000,
  "total_duration_seconds": 600,
  "num_recordings": 20,
  "avg_snr_db": 15.0,
  "recording_conditions": [
    "clear line of sight",
    "various distances (50-500m)",
    "various altitudes (10-120m)",
    "different speeds (hover to 15m/s)"
  ],
  "ground_truth": {
    "available": true,
    "format": "json",
    "includes_position": true,
    "includes_telemetry": true
  },
  "usage": {
    "training": 0.7,
    "validation": 0.15,
    "test": 0.15
  }
}
Global Index (index.json)
json
{
  "version": "2.0.0",
  "last_updated": "2024-01-15T10:30:00Z",
  "total_datasets": 12,
  "total_recordings": 115,
  "total_duration_seconds": 3900,
  "total_size_bytes": 31200000000,
  "datasets": [
    {
      "name": "dji_mavic_2.4g",
      "drone_type": "DJI Mavic 3",
      "frequency": "2.4 GHz",
      "num_recordings": 20,
      "duration_seconds": 600,
      "size_bytes": 4800000000
    },
    {
      "name": "dji_mavic_5.8g",
      "drone_type": "DJI Mavic 3",
      "frequency": "5.8 GHz",
      "num_recordings": 20,
      "duration_seconds": 600,
      "size_bytes": 9600000000
    }
  ],
  "statistics": {
    "total_by_drone_type": {
      "DJI Mavic 3": 40,
      "DJI Mini 3": 10,
      "FPV Analog": 10,
      "FPV Digital": 10,
      "Autel EVO II": 10,
      "Skydio 2": 10
    },
    "total_by_environment": {
      "urban": 5,
      "suburban": 5,
      "rural": 5,
      "industrial": 5,
      "office": 5
    }
  }
}
Loading and Playback
Basic Loading
python
import numpy as np
import json
from pathlib import Path

def load_replay_recording(dataset, recording_id):
    """Load a replay recording"""
    file_path = Path(f"data/iq/replay/{dataset}/{recording_id}.iq")
    meta_path = file_path.with_suffix('.json')
    
    # Load IQ data
    iq_data = np.fromfile(file_path, dtype=np.complex64)
    
    # Load metadata
    with open(meta_path, 'r') as f:
        metadata = json.load(f)
    
    return iq_data, metadata

# Usage
iq_data, meta = load_replay_recording("dji_mavic_2.4g", "recording_001")
print(f"Loaded {meta['drone_type']} recording")
print(f"Duration: {meta['duration_seconds']:.2f}s")
print(f"Sample rate: {meta['sample_rate']/1e6:.1f} MHz")
Batch Loading
python
def load_dataset(dataset_name):
    """Load entire dataset"""
    dataset_path = Path(f"data/iq/replay/{dataset_name}")
    
    recordings = []
    for iq_file in sorted(dataset_path.glob("*.iq")):
        iq_data = np.fromfile(iq_file, dtype=np.complex64)
        
        with open(iq_file.with_suffix('.json'), 'r') as f:
            metadata = json.load(f)
        
        recordings.append({
            'data': iq_data,
            'metadata': metadata
        })
    
    return recordings

# Load all DJI Mavic recordings
recordings = load_dataset("dji_mavic_2.4g")
print(f"Loaded {len(recordings)} recordings")
Playback with Engine
python
from infrastructure.signal_io.playback import IQPlaybackEngine

async def replay_dataset(dataset_name, speed=1.0):
    """Replay a dataset through the detection pipeline"""
    
    engine = IQPlaybackEngine()
    
    # Add all recordings from dataset
    dataset_path = Path(f"data/iq/replay/{dataset_name}")
    for iq_file in dataset_path.glob("*.iq"):
        engine.add_file(iq_file)
    
    # Register detection callback
    def on_detection(detection):
        print(f"Detection: {detection['drone_type']} (confidence: {detection['confidence']:.2f})")
    
    engine.on_detection(on_detection)
    
    # Start playback
    await engine.play(speed=speed)
    
    # Process frames
    async for chunk in engine:
        # Run detection on chunk
        result = detection_pipeline.process(chunk)
        if result:
            print(f"Detected: {result}")
    
    await engine.stop()
Playback Modes
1. Normal Playback
python
await engine.play(speed=1.0)  # Real-time playback
2. Speed Control
python
await engine.play(speed=0.5)   # Half speed
await engine.play(speed=2.0)   # Double speed
await engine.play(speed=0.0)   # Pause
3. Loop Playback
python
from infrastructure.signal_io.playback import PlaybackMode

engine.config.mode = PlaybackMode.LOOP
await engine.play()  # Infinite loop
4. Random Access
python
await engine.seek(15.0)  # Jump to 15 seconds
await engine.seek(0)     # Restart
Testing Scenarios
Scenario 1: Single Drone Detection
python
async def test_single_drone():
    """Test detection on a single drone recording"""
    
    iq_data, meta = load_replay_recording("dji_mavic_2.4g", "recording_001")
    
    # Run detection
    detections = detection_engine.process(iq_data, meta['sample_rate'])
    
    # Verify
    assert len(detections) > 0
    assert detections[0]['drone_type'] == meta['drone_type']
    assert detections[0]['confidence'] > 0.8
    
    print(f"✓ Detection successful: {detections[0]['drone_type']}")
Scenario 2: Interference Rejection
python
async def test_interference_rejection():
    """Test detection in presence of interference"""
    
    # Load drone signal
    drone, drone_meta = load_replay_recording("dji_mavic_2.4g", "recording_001")
    
    # Load interference
    interference, int_meta = load_replay_recording("interference", "wifi_2.4g")
    
    # Mix signals (dB scale)
    drone_power = np.mean(np.abs(drone)**2)
    int_power = np.mean(np.abs(interference)**2)
    mix = drone + np.sqrt(int_power/drone_power) * interference[:len(drone)]
    
    # Test detection
    detections = detection_engine.process(mix, drone_meta['sample_rate'])
    
    assert len(detections) > 0
    print(f"✓ Detection successful with {int_meta['interference_type']} interference")
Scenario 3: Multiple Drones
python
async def test_multiple_drones():
    """Test detection of multiple simultaneous drones"""
    
    # Load different drone signals
    dji, dji_meta = load_replay_recording("dji_mavic_2.4g", "recording_001")
    fpv, fpv_meta = load_replay_recording("fpv_analog_5.8g", "recording_001")
    
    # Combine signals (different frequency bands)
    mixed = dji + fpv[:len(dji)]
    
    # Test detection
    detections = detection_engine.process(mixed, dji_meta['sample_rate'])
    
    # Should detect both drones
    drone_types = [d['drone_type'] for d in detections]
    assert "DJI Mavic 3" in drone_types
    assert "FPV Analog" in drone_types
    
    print(f"✓ Detected {len(detections)} drones")
Scenario 4: Low SNR Performance
python
async def test_low_snr():
    """Test detection at various SNR levels"""
    
    iq_data, meta = load_replay_recording("dji_mavic_2.4g", "recording_001")
    
    snr_levels = [20, 15, 10, 6, 3, 0]  # dB
    results = {}
    
    for snr in snr_levels:
        # Add noise to achieve target SNR
        signal_power = np.mean(np.abs(iq_data)**2)
        noise_power = signal_power / (10 ** (snr / 10))
        noise = np.sqrt(noise_power/2) * (np.random.randn(len(iq_data)) + 1j * np.random.randn(len(iq_data)))
        noisy = iq_data + noise
        
        # Test detection
        detections = detection_engine.process(noisy, meta['sample_rate'])
        results[snr] = len(detections) > 0 and detections[0]['confidence']
    
    print("SNR Performance:")
    for snr, conf in results.items():
        print(f"  {snr} dB: {conf:.2%}" if conf else f"  {snr} dB: Failed")
Performance Benchmarking
Benchmark Script
python
import time
import numpy as np

def benchmark_processing(dataset_name, num_iterations=10):
    """Benchmark processing performance"""
    
    recordings = load_dataset(dataset_name)
    times = []
    
    for i in range(num_iterations):
        start = time.time()
        
        for recording in recordings:
            # Process recording
            detection_engine.process(recording['data'], recording['metadata']['sample_rate'])
        
        elapsed = time.time() - start
        times.append(elapsed)
    
    avg_time = np.mean(times)
    std_time = np.std(times)
    
    print(f"Dataset: {dataset_name}")
    print(f"  Recordings: {len(recordings)}")
    print(f"  Total data: {sum(len(r['data']) for r in recordings) / 1e6:.1f}M samples")
    print(f"  Avg processing: {avg_time:.2f}s")
    print(f"  Std dev: {std_time:.2f}s")
    print(f"  Throughput: {len(recordings) * 30 / avg_time:.1f}x real-time")

# Run benchmark
benchmark_processing("dji_mavic_2.4g")
Dataset Validation
Validate Dataset Integrity
python
def validate_dataset(dataset_name):
    """Validate dataset files and metadata"""
    
    dataset_path = Path(f"data/iq/replay/{dataset_name}")
    
    issues = []
    
    # Check all IQ files have matching JSON
    for iq_file in dataset_path.glob("*.iq"):
        json_file = iq_file.with_suffix('.json')
        if not json_file.exists():
            issues.append(f"Missing metadata: {json_file.name}")
        
        # Verify IQ file size is multiple of 8 bytes
        if iq_file.stat().st_size % 8 != 0:
            issues.append(f"Invalid IQ file size: {iq_file.name}")
        
        # Verify data can be loaded
        try:
            data = np.fromfile(iq_file, dtype=np.complex64)
            if len(data) == 0:
                issues.append(f"Empty IQ file: {iq_file.name}")
        except Exception as e:
            issues.append(f"Cannot load {iq_file.name}: {e}")
    
    # Check dataset info
    info_file = dataset_path / "dataset_info.json"
    if not info_file.exists():
        issues.append("Missing dataset_info.json")
    
    if issues:
        print(f"Dataset {dataset_name} has {len(issues)} issues:")
        for issue in issues[:10]:
            print(f"  - {issue}")
        return False
    
    print(f"✓ Dataset {dataset_name} is valid")
    return True
Export for Training
python
def export_for_training(dataset_name, output_dir="training_data"):
    """Export dataset for ML training"""
    
    import shutil
    
    output_path = Path(output_dir) / dataset_name
    output_path.mkdir(parents=True, exist_ok=True)
    
    recordings = load_dataset(dataset_name)
    
    # Create feature extraction
    from models.training.features.feature_extractor import FeatureExtractor
    extractor = FeatureExtractor()
    
    features = []
    labels = []
    
    for rec in recordings:
        # Extract features
        feature_dict = extractor.extract_all_features(rec['data'])
        feature_vector = np.array([feature_dict[name] for name in FEATURE_NAMES])
        features.append(feature_vector)
        labels.append(rec['metadata']['drone_type'])
        
        # Export IQ data
        iq_file = output_path / f"{rec['metadata']['recording_id']}.iq"
        rec['data'].tofile(iq_file)
    
    # Save features
    np.save(output_path / "features.npy", np.array(features))
    
    # Save labels
    with open(output_path / "labels.json", 'w') as f:
        json.dump(labels, f, indent=2)
    
    print(f"Exported {len(recordings)} recordings to {output_path}")
Command Line Interface
bash
# List all available datasets
python -m infrastructure.signal_io.playback --list-datasets

# Play a specific recording
python -m infrastructure.signal_io.playback --dataset dji_mavic_2.4g --recording 001

# Run benchmark
python -m infrastructure.signal_io.playback --benchmark --dataset dji_mavic_2.4g

# Validate datasets
python -m infrastructure.signal_io.playback --validate

# Export for training
python -m infrastructure.signal_io.playback --export --dataset dji_mavic_2.4g
Adding New Datasets
Dataset Creation Guidelines
Recording Duration: 30 seconds minimum

Sample Rate: 10 MHz for 2.4 GHz, 20 MHz for 5.8 GHz

SNR: Include SNR in metadata

Ground Truth: Provide position and telemetry if available

Documentation: Update README and index.json

Dataset Submission Checklist
IQ files in correct format

Metadata JSON files for each recording

Dataset info JSON file

Updated index.json

Updated README

Validation passes

Ground truth data (if available)

Troubleshooting
Issue	Solution
File not found	Verify dataset name and recording ID
Memory error	Use chunked loading for large files
Playback stutters	Reduce playback speed or use smaller chunks
Detection fails	Check SNR and signal presence
Metadata mismatch	Regenerate JSON files from IQ analysis
