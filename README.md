drone-detector/data/exports/spectrum/README.md - Spectrum Exports Documentation

markdown
# Spectrum Exports Directory

This directory contains exported spectrum analysis data from the Drone Detection System. Exports include spectrum snapshots, waterfall plots, PSD data, and signal analysis results in various formats for visualization, analysis, and forensic investigation.

## Directory Structure
data/exports/spectrum/
├── README.md # This file
├── spectrum_snapshot_20240115_143022.png # Spectrum plot (PNG)
├── spectrum_snapshot_20240115_143022.svg # Spectrum plot (SVG)
├── spectrum_snapshot_20240115_143022.json # Spectrum data (JSON)
├── spectrum_snapshot_20240115_143022.csv # Spectrum data (CSV)
├── waterfall_snapshot_20240115_143022.png # Waterfall plot
├── waterfall_snapshot_20240115_143022.json # Waterfall data
├── psd_measurement_20240115_143022.npy # PSD data (NumPy)
├── peak_analysis_20240115_143022.json # Peak detection results
├── signal_analysis_20240115_143022.json # Signal parameters
├── interference_20240115_143022.json # Interference detection
├── modulation_20240115_143022.json # Modulation analysis
├── spectrum_animation_20240115.gif # Time-lapse animation
├── band_occupancy_20240115.json # Band occupancy report
├── index.json # Export index and metadata
└── thumbnails/ # Thumbnail images
├── spectrum_snapshot_20240115_143022_thumb.png
└── waterfall_snapshot_20240115_143022_thumb.png

text

## Naming Convention

Export files follow a consistent naming pattern:

| Export Type | Pattern | Example |
|-------------|---------|---------|
| Spectrum Snapshot | `spectrum_snapshot_YYYYMMDD_HHMMSS.format` | `spectrum_snapshot_20240115_143022.png` |
| Waterfall | `waterfall_snapshot_YYYYMMDD_HHMMSS.format` | `waterfall_snapshot_20240115_143022.png` |
| PSD Data | `psd_measurement_YYYYMMDD_HHMMSS.npy` | `psd_measurement_20240115_143022.npy` |
| Peak Analysis | `peak_analysis_YYYYMMDD_HHMMSS.json` | `peak_analysis_20240115_143022.json` |
| Signal Analysis | `signal_analysis_YYYYMMDD_HHMMSS.json` | `signal_analysis_20240115_143022.json` |
| Interference | `interference_YYYYMMDD_HHMMSS.json` | `interference_20240115_143022.json` |
| Modulation | `modulation_YYYYMMDD_HHMMSS.json` | `modulation_20240115_143022.json` |
| Animation | `spectrum_animation_YYYYMMDD.gif` | `spectrum_animation_20240115.gif` |
| Band Occupancy | `band_occupancy_YYYYMMDD.json` | `band_occupancy_20240115.json` |

## File Formats

### PNG Image Format (.png)

High-resolution spectrum plots suitable for reports and presentations.

**Specifications:**
| Property | Value |
|----------|-------|
| Resolution | 1920x1080 pixels (customizable) |
| Color Depth | 24-bit RGB |
| DPI | 150 (print quality) |
| Compression | Lossless PNG |
| Background | Dark theme (configurable) |

**Features:**
- Frequency vs. Power plot
- Detected peaks highlighted
- Noise floor indication
- Frequency band labels
- Grid lines and axis labels
- Title with timestamp

### SVG Image Format (.svg)

Vector graphics format for scalable, editable spectrum plots.

**Features:**
- Resolution independent
- Editable in vector graphics software
- Small file size
- Text as text (searchable)
- Layer support

### JSON Data Format (.json)

Structured spectrum data for programmatic analysis.

```json
{
  "export_info": {
    "export_id": "spec_exp_20240115_143022",
    "export_date": "2024-01-15T14:30:22.123456Z",
    "export_format": "json",
    "version": "2.0.0",
    "source": "spectrum_analyzer",
    "device": {
      "type": "hackrf",
      "sample_rate": 10000000,
      "center_frequency": 2440000000
    }
  },
  "spectrum": {
    "frequencies_hz": [2400000000, 2401000000, ...],
    "psd_dbm": [-95.2, -94.8, -45.2, ...],
    "sample_rate": 10000000,
    "fft_size": 2048,
    "resolution_bandwidth_hz": 4882.81,
    "number_of_points": 2048
  },
  "analysis": {
    "noise_floor_dbm": -98.5,
    "peak_frequency_hz": 2440000000,
    "peak_power_dbm": -45.2,
    "snr_db": 53.3,
    "total_power_dbm": -52.1,
    "occupied_bandwidth_hz": 20000000,
    "peak_to_average_ratio_db": 6.8
  },
  "peaks": [
    {
      "index": 512,
      "frequency_hz": 2440000000,
      "power_dbm": -45.2,
      "prominence_db": 35.6,
      "width_hz": 125000,
      "snr_db": 53.3
    },
    {
      "index": 768,
      "frequency_hz": 2450000000,
      "power_dbm": -62.3,
      "prominence_db": 18.2,
      "width_hz": 89000,
      "snr_db": 36.2
    }
  ],
  "statistics": {
    "mean_power_dbm": -82.3,
    "std_power_dbm": 12.4,
    "min_power_dbm": -102.3,
    "max_power_dbm": -45.2,
    "power_variance": 153.8,
    "spectral_flatness": 0.234,
    "spectral_centroid_hz": 2445000000,
    "spectral_spread_hz": 15000000
  }
}
CSV Data Format (.csv)
Tabular spectrum data for spreadsheet analysis.

csv
Frequency (Hz),Power (dBm),Frequency (MHz),Power (Linear)
2400000000,-95.2,2400.0,3.02e-10
2401000000,-94.8,2401.0,3.31e-10
2402000000,-93.5,2402.0,4.47e-10
...
2440000000,-45.2,2440.0,3.02e-05
2441000000,-46.1,2441.0,2.45e-05
...
2483000000,-96.2,2483.0,2.40e-10
2483500000,-96.8,2483.5,2.09e-10
NumPy Format (.npy)
Binary format for fast loading in Python.

python
import numpy as np

# Load PSD data
psd_data = np.load('psd_measurement_20240115_143022.npy')

# Data contains: [frequencies, psd_values, metadata]
frequencies = psd_data[0]
psd_values = psd_data[1]
metadata = psd_data[2].item()
Waterfall Format
PNG Visualization:

Time vs Frequency heatmap

Color intensity represents power

Scrollable history (up to 100 lines)

Animated transitions

JSON Data:

json
{
  "waterfall": {
    "time_axis": ["14:30:22", "14:30:23", ...],
    "frequency_axis_hz": [2400000000, 2401000000, ...],
    "power_matrix": [[-95.2, -94.8, ...], [...]],
    "max_lines": 100,
    "time_resolution_ms": 100
  }
}
Export Operations
Creating Spectrum Snapshot
python
async def create_spectrum_snapshot(iq_data, sample_rate, center_freq, output_dir="data/exports/spectrum"):
    """Create spectrum snapshot export"""
    
    from datetime import datetime
    import matplotlib.pyplot as plt
    import numpy as np
    
    timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
    base_filename = f"spectrum_snapshot_{timestamp}"
    
    # Compute PSD
    frequencies, psd = compute_psd(iq_data, sample_rate)
    psd_db = 10 * np.log10(psd + 1e-12)
    
    # Find peaks
    peaks = detect_peaks(psd_db, height=np.max(psd_db) - 20)
    
    # Create plot
    fig, ax = plt.subplots(figsize=(12, 6))
    
    # Plot spectrum
    ax.plot(frequencies / 1e6, psd_db, 'b-', linewidth=1, alpha=0.8)
    
    # Highlight peaks
    for peak in peaks:
        ax.plot(peak['frequency'] / 1e6, peak['power'], 'ro', markersize=8)
        ax.annotate(f"{peak['frequency']/1e6:.1f} MHz", 
                   xy=(peak['frequency']/1e6, peak['power']),
                   xytext=(10, 10), textcoords='offset points')
    
    # Formatting
    ax.set_xlabel('Frequency (MHz)')
    ax.set_ylabel('Power (dBm)')
    ax.set_title(f'Spectrum Snapshot - {datetime.now().strftime("%Y-%m-%d %H:%M:%S")}')
    ax.grid(True, alpha=0.3)
    ax.set_xlim([center_freq/1e6 - sample_rate/2e6, center_freq/1e6 + sample_rate/2e6])
    
    # Save PNG
    png_path = Path(output_dir) / f"{base_filename}.png"
    plt.savefig(png_path, dpi=150, bbox_inches='tight', facecolor='white')
    
    # Save SVG
    svg_path = Path(output_dir) / f"{base_filename}.svg"
    plt.savefig(svg_path, format='svg', bbox_inches='tight')
    
    plt.close()
    
    # Save JSON data
    json_path = Path(output_dir) / f"{base_filename}.json"
    export_data = {
        'export_info': {
            'export_id': base_filename,
            'export_date': datetime.now().isoformat(),
            'export_format': 'json',
            'version': '2.0.0'
        },
        'spectrum': {
            'frequencies_hz': frequencies.tolist(),
            'psd_dbm': psd_db.tolist(),
            'sample_rate': sample_rate,
            'center_frequency': center_freq
        },
        'peaks': peaks,
        'statistics': compute_spectrum_statistics(psd_db, frequencies)
    }
    
    with open(json_path, 'w') as f:
        json.dump(export_data, f, indent=2)
    
    # Save CSV
    csv_path = Path(output_dir) / f"{base_filename}.csv"
    np.savetxt(csv_path, 
               np.column_stack([frequencies, psd_db]),
               delimiter=',',
               header='Frequency (Hz),Power (dBm)',
               comments='')
    
    return {
        'png': str(png_path),
        'svg': str(svg_path),
        'json': str(json_path),
        'csv': str(csv_path)
    }
Creating Waterfall Export
python
async def create_waterfall_export(spectrum_history, output_dir="data/exports/spectrum"):
    """Create waterfall visualization export"""
    
    from datetime import datetime
    import matplotlib.pyplot as plt
    import numpy as np
    
    timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
    base_filename = f"waterfall_snapshot_{timestamp}"
    
    # Convert history to matrix
    frequencies = spectrum_history[0]['frequencies']
    time_labels = [s['timestamp'] for s in spectrum_history]
    power_matrix = np.array([s['psd'] for s in spectrum_history])
    
    # Create waterfall plot
    fig, ax = plt.subplots(figsize=(14, 8))
    
    # Normalize power for colormap
    power_norm = (power_matrix - power_matrix.min()) / (power_matrix.max() - power_matrix.min())
    
    # Create heatmap
    im = ax.imshow(power_norm, aspect='auto', cmap='viridis',
                   extent=[frequencies[0]/1e6, frequencies[-1]/1e6, 
                           len(spectrum_history), 0])
    
    # Formatting
    ax.set_xlabel('Frequency (MHz)')
    ax.set_ylabel('Time (seconds ago)')
    ax.set_title(f'Waterfall Spectrogram - {datetime.now().strftime("%Y-%m-%d %H:%M:%S")}')
    
    # Add colorbar
    cbar = plt.colorbar(im, ax=ax)
    cbar.set_label('Relative Power')
    
    # Add time labels
    y_ticks = np.arange(0, len(spectrum_history), max(1, len(spectrum_history) // 10))
    ax.set_yticks(y_ticks)
    ax.set_yticklabels([f"-{len(spectrum_history) - tick}s" for tick in y_ticks])
    
    # Save
    png_path = Path(output_dir) / f"{base_filename}.png"
    plt.savefig(png_path, dpi=150, bbox_inches='tight')
    plt.close()
    
    # Save data
    json_path = Path(output_dir) / f"{base_filename}.json"
    export_data = {
        'export_info': {
            'export_id': base_filename,
            'export_date': datetime.now().isoformat()
        },
        'waterfall': {
            'frequencies_hz': frequencies.tolist(),
            'time_stamps': time_labels,
            'power_matrix': power_matrix.tolist(),
            'max_lines': len(spectrum_history)
        }
    }
    
    with open(json_path, 'w') as f:
        json.dump(export_data, f, indent=2)
    
    return {'png': str(png_path), 'json': str(json_path)}
Exporting Peak Analysis
python
async def export_peak_analysis(peaks, frequencies, psd, output_dir="data/exports/spectrum"):
    """Export peak detection analysis"""
    
    from datetime import datetime
    
    timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
    filename = f"peak_analysis_{timestamp}.json"
    
    # Analyze peaks
    peak_analysis = []
    for peak in peaks:
        peak_analysis.append({
            'index': peak['index'],
            'frequency_hz': frequencies[peak['index']],
            'frequency_mhz': frequencies[peak['index']] / 1e6,
            'power_dbm': psd[peak['index']],
            'prominence_db': peak['prominence'],
            'width_hz': peak['width'],
            'snr_db': peak['power'] - get_noise_floor(psd),
            'is_drone_candidate': is_potential_drone(peak, frequencies)
        })
    
    # Group by frequency band
    bands = {
        '2.4ghz': [p for p in peak_analysis if 2.4e9 <= p['frequency_hz'] <= 2.5e9],
        '5.2ghz': [p for p in peak_analysis if 5.15e9 <= p['frequency_hz'] <= 5.35e9],
        '5.8ghz': [p for p in peak_analysis if 5.725e9 <= p['frequency_hz'] <= 5.875e9]
    }
    
    export_data = {
        'export_info': {
            'export_id': f"peak_analysis_{timestamp}",
            'export_date': datetime.now().isoformat(),
            'total_peaks': len(peaks)
        },
        'peaks': peak_analysis,
        'bands': bands,
        'statistics': {
            'strongest_peak': max(peak_analysis, key=lambda x: x['power_dbm']),
            'average_power': np.mean([p['power_dbm'] for p in peak_analysis]),
            'peak_density': len(peaks) / ((frequencies[-1] - frequencies[0]) / 1e6)
        }
    }
    
    file_path = Path(output_dir) / filename
    with open(file_path, 'w') as f:
        json.dump(export_data, f, indent=2)
    
    return file_path
Spectrum Analysis Tools
Loading Spectrum Data
python
import numpy as np
import json
import matplotlib.pyplot as plt

def load_spectrum_export(file_path):
    """Load spectrum export data"""
    
    file_path = Path(file_path)
    
    if file_path.suffix == '.json':
        with open(file_path, 'r') as f:
            data = json.load(f)
        
        if 'spectrum' in data:
            frequencies = np.array(data['spectrum']['frequencies_hz'])
            psd = np.array(data['spectrum']['psd_dbm'])
        else:
            frequencies = np.array(data['frequencies_hz'])
            psd = np.array(data['psd_dbm'])
        
        return frequencies, psd
    
    elif file_path.suffix == '.csv':
        data = np.loadtxt(file_path, delimiter=',', skiprows=1)
        frequencies = data[:, 0]
        psd = data[:, 1]
        return frequencies, psd
    
    elif file_path.suffix == '.npy':
        data = np.load(file_path)
        frequencies = data[0]
        psd = data[1]
        return frequencies, psd
    
    else:
        raise ValueError(f"Unsupported format: {file_path.suffix}")
Comparing Spectrum Exports
python
def compare_spectrum_exports(export1_path, export2_path):
    """Compare two spectrum exports"""
    
    # Load data
    f1, p1 = load_spectrum_export(export1_path)
    f2, p2 = load_spectrum_export(export2_path)
    
    # Interpolate to common frequency grid
    common_freq = np.linspace(max(f1[0], f2[0]), min(f1[-1], f2[-1]), 2048)
    p1_interp = np.interp(common_freq, f1, p1)
    p2_interp = np.interp(common_freq, f2, p2)
    
    # Calculate difference
    diff = p2_interp - p1_interp
    
    # Statistics
    comparison = {
        'mean_difference_db': np.mean(diff),
        'max_difference_db': np.max(diff),
        'min_difference_db': np.min(diff),
        'std_difference_db': np.std(diff),
        'correlation': np.corrcoef(p1_interp, p2_interp)[0, 1],
        'frequencies_hz': common_freq.tolist(),
        'differences_db': diff.tolist()
    }
    
    # Plot comparison
    fig, (ax1, ax2) = plt.subplots(2, 1, figsize=(12, 10))
    
    # Overlay plots
    ax1.plot(common_freq / 1e6, p1_interp, 'b-', label='Export 1', alpha=0.7)
    ax1.plot(common_freq / 1e6, p2_interp, 'r-', label='Export 2', alpha=0.7)
    ax1.set_xlabel('Frequency (MHz)')
    ax1.set_ylabel('Power (dBm)')
    ax1.set_title('Spectrum Comparison')
    ax1.legend()
    ax1.grid(True, alpha=0.3)
    
    # Difference plot
    ax2.plot(common_freq / 1e6, diff, 'g-', linewidth=1)
    ax2.axhline(y=0, color='k', linestyle='--', alpha=0.5)
    ax2.fill_between(common_freq / 1e6, diff, 0, where=(diff > 0), color='r', alpha=0.3)
    ax2.fill_between(common_freq / 1e6, diff, 0, where=(diff < 0), color='b', alpha=0.3)
    ax2.set_xlabel('Frequency (MHz)')
    ax2.set_ylabel('Power Difference (dB)')
    ax2.set_title('Spectrum Difference')
    ax2.grid(True, alpha=0.3)
    
    plt.tight_layout()
    plt.show()
    
    return comparison
Generating Band Occupancy Report
python
def generate_band_occupancy_report(spectrum_exports, output_dir="data/exports/spectrum"):
    """Generate band occupancy report from multiple exports"""
    
    from datetime import datetime
    
    bands = {
        '2.4 GHz ISM': (2.400e9, 2.4835e9),
        '5.2 GHz': (5.150e9, 5.350e9),
        '5.8 GHz ISM': (5.725e9, 5.875e9),
        '900 MHz': (902e6, 928e6),
        '1.2 GHz': (1.240e9, 1.300e9)
    }
    
    occupancy = {}
    
    for band_name, (start, end) in bands.items():
        band_powers = []
        
        for export_path in spectrum_exports:
            frequencies, psd = load_spectrum_export(export_path)
            
            # Get indices within band
            indices = np.where((frequencies >= start) & (frequencies <= end))[0]
            
            if len(indices) > 0:
                band_power = np.mean(psd[indices])
                band_powers.append(band_power)
        
        if band_powers:
            occupancy[band_name] = {
                'avg_power_dbm': np.mean(band_powers),
                'max_power_dbm': np.max(band_powers),
                'min_power_dbm': np.min(band_powers),
                'std_power_dbm': np.std(band_powers),
                'sample_count': len(band_powers)
            }
        else:
            occupancy[band_name] = {'error': 'No data available'}
    
    report = {
        'report_date': datetime.now().isoformat(),
        'exports_analyzed': len(spectrum_exports),
        'band_occupancy': occupancy,
        'recommendations': generate_band_recommendations(occupancy)
    }
    
    report_path = Path(output_dir) / f"band_occupancy_{datetime.now().strftime('%Y%m%d')}.json"
    
    with open(report_path, 'w') as f:
        json.dump(report, f, indent=2)
    
    return report_path
Visualization Tools
Interactive Spectrum Viewer
python
import plotly.graph_objects as go
from plotly.subplots import make_subplots

def create_interactive_spectrum_viewer(export_path):
    """Create interactive HTML spectrum viewer"""
    
    frequencies, psd = load_spectrum_export(export_path)
    
    # Create interactive plot
    fig = make_subplots(rows=2, cols=1, 
                        subplot_titles=('Spectrum', 'Waterfall'),
                        vertical_spacing=0.1)
    
    # Spectrum plot
    fig.add_trace(
        go.Scatter(x=frequencies/1e6, y=psd, mode='lines', name='Spectrum',
                   line=dict(color='blue', width=1)),
        row=1, col=1
    )
    
    # Add peak markers
    peaks = detect_peaks(psd, height=np.max(psd) - 20)
    for peak in peaks:
        fig.add_trace(
            go.Scatter(x=[peak['frequency']/1e6], y=[peak['power']], 
                      mode='markers', name='Peak',
                      marker=dict(color='red', size=10, symbol='circle')),
            row=1, col=1
        )
    
    # Add threshold line
    noise_floor = np.percentile(psd, 10)
    fig.add_hline(y=noise_floor, line_dash="dash", line_color="gray",
                  annotation_text="Noise Floor", row=1, col=1)
    
    # Update layout
    fig.update_layout(
        title='Spectrum Analysis',
        xaxis_title='Frequency (MHz)',
        yaxis_title='Power (dBm)',
        template='plotly_dark',
        hovermode='closest'
    )
    
    # Save as HTML
    html_path = export_path.with_suffix('.html')
    fig.write_html(str(html_path))
    
    return html_path
Generating Spectrum Animation
python
def create_spectrum_animation(export_paths, output_path):
    """Create animated GIF from multiple spectrum exports"""
    
    import imageio
    import tempfile
    
    frames = []
    
    for export_path in sorted(export_paths):
        # Load spectrum
        frequencies, psd = load_spectrum_export(export_path)
        
        # Create frame
        fig, ax = plt.subplots(figsize=(10, 6))
        ax.plot(frequencies / 1e6, psd, 'b-', linewidth=1)
        ax.set_xlabel('Frequency (MHz)')
        ax.set_ylabel('Power (dBm)')
        ax.set_title(f'Spectrum - {export_path.stem}')
        ax.grid(True, alpha=0.3)
        ax.set_ylim([-120, -30])
        
        # Save to temporary file
        with tempfile.NamedTemporaryFile(suffix='.png', delete=False) as tmp:
            plt.savefig(tmp.name, dpi=100, bbox_inches='tight')
            frames.append(imageio.imread(tmp.name))
        
        plt.close()
    
    # Create GIF
    imageio.mimsave(output_path, frames, duration=0.5, loop=0)
    
    return output_path
Integration Examples
Import to MATLAB
matlab
% Load spectrum CSV export
data = readtable('spectrum_snapshot_20240115_143022.csv');

% Extract data
freq_mhz = data.Frequency_Hz / 1e6;
power_dbm = data.Power_dBm;

% Plot
figure;
plot(freq_mhz, power_dbm, 'b-', 'LineWidth', 1);
xlabel('Frequency (MHz)');
ylabel('Power (dBm)');
title('Spectrum Analysis');
grid on;

% Find peaks
[pks, locs] = findpeaks(power_dbm, 'MinPeakHeight', -60);
hold on;
plot(freq_mhz(locs), pks, 'ro', 'MarkerSize', 8);
Import to GNU Octave
octave
# Load JSON export
data = jsondecode(fileread('spectrum_snapshot_20240115_143022.json'));

# Extract data
freq = data.spectrum.frequencies_hz / 1e6;
power = data.spectrum.psd_dbm;

# Plot
plot(freq, power, 'b-');
xlabel('Frequency (MHz)');
ylabel('Power (dBm)');
title('Spectrum Analysis');
grid on;
Import to Python (SciPy)
python
from scipy import signal
import numpy as np
import json

# Load spectrum data
with open('spectrum_snapshot_20240115_143022.json', 'r') as f:
    data = json.load(f)

frequencies = np.array(data['spectrum']['frequencies_hz'])
psd = np.array(data['spectrum']['psd_dbm'])

# Find peaks using scipy
from scipy.signal import find_peaks
peaks, properties = find_peaks(psd, height=-60, prominence=5)

# Calculate spectral entropy
def spectral_entropy(psd):
    psd_norm = psd / np.sum(psd)
    return -np.sum(psd_norm * np.log2(psd_norm + 1e-12))

entropy = spectral_entropy(10 ** (psd / 10))
print(f"Spectral Entropy: {entropy:.3f}")
Storage Guidelines
Retention Policy
Export Type	Retention	Compression	Archive
Spectrum PNG	30 days	None	Monthly
Spectrum JSON	90 days	gzip	Quarterly
Waterfall PNG	14 days	None	Monthly
Waterfall JSON	30 days	gzip	Quarterly
Peak Analysis	90 days	None	Quarterly
Animations	7 days	None	As needed
Band Occupancy	365 days	None	Annual
Storage Limits
python
def check_spectrum_storage():
    """Check spectrum storage usage"""
    
    exports_dir = Path("data/exports/spectrum")
    total_size = sum(f.stat().st_size for f in exports_dir.rglob("*") if f.is_file())
    size_gb = total_size / (1024 ** 3)
    
    limits = {
        'warning': 2,    # 2 GB warning
        'critical': 5,   # 5 GB critical
        'max': 10        # 10 GB maximum
    }
    
    return {
        'size_gb': size_gb,
        'file_count': len(list(exports_dir.rglob("*"))),
        'status': 'ok' if size_gb < limits['warning'] else 'warning' if size_gb < limits['critical'] else 'critical'
    }
Troubleshooting
Common Issues
Issue	Cause	Solution
Missing peaks	Threshold too high	Adjust peak detection parameters
Blurry image	Low DPI	Increase DPI in export settings
Slow export	Large FFT size	Reduce FFT size or frequency range
Memory error	Too many waterfall lines	Limit history length
Corrupted JSON	Incomplete write	Re-export or restore from backup
Export Recovery
python
async def recover_spectrum_export(export_id):
    """Recover missing spectrum export"""
    
    export_path = Path(f"data/exports/spectrum/spectrum_snapshot_{export_id}.json")
    
    if export_path.exists():
        return {'status': 'exists', 'path': str(export_path)}
    
    # Try to find in archive
    archive_path = Path(f"data/exports/archived/spectrum_snapshot_{export_id}.json.gz")
    
    if archive_path.exists():
        import gzip
        with gzip.open(archive_path, 'rb') as f_in:
            with open(export_path, 'wb') as f_out:
                f_out.write(f_in.read())
        return {'status': 'restored', 'path': str(export_path)}
    
    return {'status': 'not_found'}
Best Practices
Export Configuration
python
# Recommended export settings
SPECTRUM_EXPORT_CONFIG = {
    'fft_size': 2048,
    'overlap': 0.5,
    'window': 'hann',
    'frequency_range': [2.4e9, 2.5e9],  # 2.4 GHz band
    'resolution': 'high',  # high, medium, low
    'formats': ['png', 'json'],
    'include_waterfall': True,
    'waterfall_lines': 50,
    'peak_detection': {
        'enabled': True,
        'threshold_db': 6,
        'min_prominence': 10
    }
}
Quality Assurance
python
def validate_spectrum_export(file_path):
    """Validate spectrum export quality"""
    
    try:
        frequencies, psd = load_spectrum_export(file_path)
        
        checks = {
            'has_data': len(frequencies) > 0,
            'valid_range': np.all(np.isfinite(frequencies)) and np.all(np.isfinite(psd)),
            'frequency_monotonic': np.all(np.diff(frequencies) > 0),
            'power_range': np.min(psd) > -150 and np.max(psd) < 50,
            'no_clipping': np.max(psd) < 0
        }
        
        quality_score = sum(checks.values()) / len(checks) * 100
        
        return {
            'valid': quality_score == 100,
            'checks': checks,
            'quality_score': quality_score,
            'issues': [k for k, v in checks.items() if not v]
        }
        
    except Exception as e:
        return {'valid': False, 'error': str(e)}
