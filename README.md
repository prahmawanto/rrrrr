drone-detector/data/exports/ml/README.md - ML Training Data Exports Documentation

markdown
# ML Training Data Exports Directory

This directory contains machine learning training data exports from the Drone Detection System. These exports include feature vectors, labeled datasets, model evaluation results, and training artifacts used for developing and improving drone classification models.

## Directory Structure
data/exports/ml/
├── README.md # This file
├── features/ # Extracted feature datasets
│ ├── features_20240115.csv # Feature vectors (CSV)
│ ├── features_20240115.npy # Feature vectors (NumPy)
│ ├── features_20240115_spectral.csv # Spectral features only
│ ├── features_20240115_temporal.csv # Temporal features only
│ ├── features_20240115_modulation.csv # Modulation features only
│ └── features_20240115_cyclostationary.csv # Cyclostationary features
├── labeled/ # Labeled datasets
│ ├── training_set.json # Training dataset
│ ├── training_set.npy # Training set (NumPy)
│ ├── validation_set.json # Validation dataset
│ ├── validation_set.npy # Validation set (NumPy)
│ ├── test_set.json # Test dataset
│ └── test_set.npy # Test set (NumPy)
├── evaluations/ # Model evaluation results
│ ├── evaluation_20240115.json # Evaluation metrics
│ ├── evaluation_20240115.html # Evaluation report
│ ├── confusion_matrix_20240115.png # Confusion matrix
│ ├── roc_curves_20240115.png # ROC curves
│ ├── precision_recall_20240115.png # Precision-Recall curves
│ ├── feature_importance_20240115.png # Feature importance plot
│ └── learning_curves_20240115.png # Learning curves
├── models/ # Exported models
│ ├── classifier_20240115.pkl # Pickled model
│ ├── classifier_20240115.onnx # ONNX model
│ ├── scaler_20240115.pkl # Feature scaler
│ ├── model_metadata_20240115.json # Model metadata
│ └── model_card_20240115.md # Model documentation
├── experiments/ # Experiment tracking
│ ├── experiment_001_baseline.json
│ ├── experiment_002_augmented.json
│ ├── experiment_003_feature_selection.json
│ └── experiment_log.csv
└── index.json # Export index and metadata

text

## Naming Convention

Export files follow a consistent naming pattern:

| Export Type | Pattern | Example |
|-------------|---------|---------|
| Feature Export | `features_YYYYMMDD.format` | `features_20240115.csv` |
| Training Set | `training_set.format` | `training_set.json` |
| Validation Set | `validation_set.format` | `validation_set.json` |
| Test Set | `test_set.format` | `test_set.json` |
| Evaluation | `evaluation_YYYYMMDD.format` | `evaluation_20240115.json` |
| Model Export | `classifier_YYYYMMDD.format` | `classifier_20240115.pkl` |
| Experiment | `experiment_XXX_name.json` | `experiment_001_baseline.json` |

## File Formats

### Feature CSV Format (.csv)

Tabular feature data for analysis and visualization.

```csv
sample_id,drone_type,peak_freq_hz,peak_magnitude_dbm,bandwidth_hz,snr_db,spectral_flatness,modulation_index,evm_rms,label
sample_001,DJI Mavic 3,2440000000,-45.2,20000000,28.5,0.234,0.85,0.12,1
sample_002,DJI Mini 3,2440000000,-52.3,10000000,22.1,0.312,0.72,0.15,2
sample_003,FPV Analog,5800000000,-55.1,8000000,18.5,0.456,1.24,0.08,3
sample_004,FPV Digital,5800000000,-48.7,20000000,25.3,0.287,0.91,0.11,4
sample_005,Noise,2440000000,-92.4,0,5.2,0.876,0.00,0.95,0
Feature NumPy Format (.npy)
Binary format for fast loading in Python.

python
import numpy as np

# Load feature data
features = np.load('features_20240115.npy')

# Structure: [num_samples, num_features]
# Shape: (12500, 46) - 46 features per sample
print(f"Features shape: {features.shape}")

# Load labels
labels = np.load('labels_20240115.npy')
print(f"Labels shape: {labels.shape}")
Labeled Dataset JSON Format (.json)
Structured labeled dataset with metadata.

json
{
  "dataset_info": {
    "name": "Drone Detection Training Set",
    "version": "2.0.0",
    "created_date": "2024-01-15T10:30:00Z",
    "num_samples": 8750,
    "num_features": 46,
    "num_classes": 14,
    "class_distribution": {
      "DJI Mavic 3": 1250,
      "DJI Mini 3": 950,
      "DJI Phantom": 1050,
      "FPV Analog": 900,
      "FPV Digital": 850,
      "Autel EVO II": 1000,
      "Skydio 2": 800,
      "Parrot Anafi": 750,
      "Noise": 1200
    },
    "feature_names": [
      "peak_freq_hz",
      "peak_magnitude_dbm",
      "bandwidth_hz",
      "snr_db",
      "spectral_flatness",
      "modulation_index",
      "evm_rms",
      "..."
    ],
    "source": "field_recordings",
    "augmentation_applied": true,
    "normalization": "z_score"
  },
  "data": [
    {
      "sample_id": "sample_001",
      "features": {
        "peak_freq_hz": 2440000000,
        "peak_magnitude_dbm": -45.2,
        "bandwidth_hz": 20000000,
        "snr_db": 28.5,
        "spectral_flatness": 0.234,
        "modulation_index": 0.85,
        "evm_rms": 0.12
      },
      "label": "DJI Mavic 3",
      "label_id": 1,
      "confidence": 0.95,
      "source_file": "recording_001.iq",
      "segment": 42
    }
  ]
}
Evaluation Results JSON Format (.json)
Comprehensive model evaluation metrics.

json
{
  "evaluation_info": {
    "evaluation_id": "eval_20240115_001",
    "evaluation_date": "2024-01-15T14:30:00Z",
    "model_name": "Drone Detection Classifier",
    "model_version": "2.0.0",
    "test_set_size": 1875
  },
  "overall_metrics": {
    "accuracy": 0.942,
    "precision_macro": 0.918,
    "recall_macro": 0.921,
    "f1_macro": 0.919,
    "precision_weighted": 0.941,
    "recall_weighted": 0.942,
    "f1_weighted": 0.941,
    "kappa": 0.935,
    "mcc": 0.928
  },
  "per_class_metrics": {
    "DJI Mavic 3": {
      "precision": 0.94,
      "recall": 0.92,
      "f1": 0.93,
      "support": 156,
      "auc": 0.98
    },
    "FPV Analog": {
      "precision": 0.91,
      "recall": 0.93,
      "f1": 0.92,
      "support": 135,
      "auc": 0.97
    }
  },
  "confusion_matrix": {
    "shape": [14, 14],
    "values": [[182, 3, 2, ...], [...]]
  },
  "roc_auc_scores": {
    "micro": 0.98,
    "macro": 0.97,
    "weighted": 0.98
  },
  "feature_importance": {
    "peak_magnitude_dbm": 0.1245,
    "snr_db": 0.1123,
    "peak_freq_hz": 0.0987,
    "bandwidth_hz": 0.0876,
    "spectral_flatness": 0.0765
  },
  "training_history": {
    "num_epochs": 100,
    "best_epoch": 87,
    "train_loss": [0.456, 0.234, ...],
    "val_loss": [0.523, 0.267, ...],
    "train_accuracy": [0.82, 0.89, ...],
    "val_accuracy": [0.79, 0.88, ...]
  }
}
Model Export Formats
Pickle Format (.pkl) - Python serialized model

python
import pickle

# Load model
with open('classifier_20240115.pkl', 'rb') as f:
    model = pickle.load(f)

# Load scaler
with open('scaler_20240115.pkl', 'rb') as f:
    scaler = pickle.load(f)
ONNX Format (.onnx) - Cross-platform model format

python
import onnxruntime as ort

# Load ONNX model
session = ort.InferenceSession('classifier_20240115.onnx')

# Run inference
inputs = {session.get_inputs()[0].name: features}
outputs = session.run(None, inputs)
Model Metadata (.json)

json
{
  "model_name": "Drone Detection Classifier",
  "version": "2.0.0",
  "algorithm": "RandomForest",
  "training_date": "2024-01-15T10:30:00Z",
  "num_features": 46,
  "feature_names": ["peak_freq_hz", "peak_magnitude_dbm", ...],
  "num_classes": 14,
  "class_names": ["Noise", "DJI Mavic 3", "FPV Analog", ...],
  "hyperparameters": {
    "n_estimators": 100,
    "max_depth": 20,
    "min_samples_split": 5,
    "min_samples_leaf": 2,
    "max_features": "sqrt"
  },
  "performance": {
    "accuracy": 0.942,
    "f1_macro": 0.919,
    "precision_macro": 0.918,
    "recall_macro": 0.921
  },
  "input_shape": [-1, 46],
  "output_shape": [-1, 14],
  "framework": "scikit-learn",
  "dependencies": {
    "scikit-learn": "1.2.2",
    "numpy": "1.24.3",
    "scipy": "1.10.1"
  }
}
Export Operations
Export Feature Dataset
python
async def export_feature_dataset(X, y, feature_names, output_dir="data/exports/ml"):
    """Export feature dataset to multiple formats"""
    
    from datetime import datetime
    import pandas as pd
    import numpy as np
    
    timestamp = datetime.now().strftime('%Y%m%d')
    base_filename = f"features_{timestamp}"
    
    exports = {}
    
    # CSV export
    df = pd.DataFrame(X, columns=feature_names)
    df['label'] = y
    csv_path = Path(output_dir) / "features" / f"{base_filename}.csv"
    df.to_csv(csv_path, index=False)
    exports['csv'] = str(csv_path)
    
    # NumPy export
    npy_path = Path(output_dir) / "features" / f"{base_filename}.npy"
    np.save(npy_path, X)
    exports['npy'] = str(npy_path)
    
    # Feature subsets
    spectral_indices = [i for i, name in enumerate(feature_names) if 'spectral' in name]
    if spectral_indices:
        spectral_path = Path(output_dir) / "features" / f"{base_filename}_spectral.csv"
        df_spectral = pd.DataFrame(X[:, spectral_indices], 
                                   columns=[feature_names[i] for i in spectral_indices])
        df_spectral.to_csv(spectral_path, index=False)
        exports['spectral'] = str(spectral_path)
    
    return exports
Create Labeled Dataset
python
async def create_labeled_dataset(features, labels, class_names, output_dir="data/exports/ml"):
    """Create labeled dataset for training"""
    
    from datetime import datetime
    import json
    import numpy as np
    from sklearn.model_selection import train_test_split
    
    # Split dataset
    X_train, X_temp, y_train, y_temp = train_test_split(
        features, labels, test_size=0.3, random_state=42, stratify=labels
    )
    X_val, X_test, y_val, y_test = train_test_split(
        X_temp, y_temp, test_size=0.5, random_state=42, stratify=y_temp
    )
    
    datasets = {
        'training_set': (X_train, y_train),
        'validation_set': (X_val, y_val),
        'test_set': (X_test, y_test)
    }
    
    exports = {}
    
    for name, (X, y) in datasets.items():
        # NumPy export
        npy_path = Path(output_dir) / "labeled" / f"{name}.npy"
        np.savez(npy_path, features=X, labels=y)
        exports[f'{name}_npy'] = str(npy_path)
        
        # JSON export
        json_path = Path(output_dir) / "labeled" / f"{name}.json"
        
        # Convert to list for JSON
        data_list = []
        for i, (sample_features, sample_label) in enumerate(zip(X, y)):
            data_list.append({
                'sample_id': f"{name}_{i:04d}",
                'features': {f"feat_{j}": float(val) for j, val in enumerate(sample_features)},
                'label': class_names[int(sample_label)],
                'label_id': int(sample_label)
            })
        
        dataset_info = {
            'dataset_info': {
                'name': name.replace('_', ' ').title(),
                'created_date': datetime.now().isoformat(),
                'num_samples': len(X),
                'num_features': X.shape[1],
                'num_classes': len(np.unique(y)),
                'class_distribution': {class_names[int(label)]: int(np.sum(y == label)) 
                                      for label in np.unique(y)}
            },
            'data': data_list
        }
        
        with open(json_path, 'w') as f:
            json.dump(dataset_info, f, indent=2)
        
        exports[f'{name}_json'] = str(json_path)
    
    return exports
Export Model Evaluation
python
async def export_model_evaluation(model, X_test, y_test, class_names, output_dir="data/exports/ml"):
    """Export comprehensive model evaluation"""
    
    from datetime import datetime
    import json
    import matplotlib.pyplot as plt
    import seaborn as sns
    from sklearn.metrics import (classification_report, confusion_matrix, 
                                 roc_curve, auc, precision_recall_curve)
    
    timestamp = datetime.now().strftime('%Y%m%d')
    eval_dir = Path(output_dir) / "evaluations"
    eval_dir.mkdir(parents=True, exist_ok=True)
    
    # Make predictions
    y_pred = model.predict(X_test)
    y_pred_proba = model.predict_proba(X_test)
    
    # Generate metrics
    report = classification_report(y_test, y_pred, target_names=class_names, output_dict=True)
    
    # Confusion matrix
    cm = confusion_matrix(y_test, y_pred)
    plt.figure(figsize=(12, 10))
    sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
                xticklabels=class_names, yticklabels=class_names)
    plt.xlabel('Predicted')
    plt.ylabel('Actual')
    plt.title('Confusion Matrix')
    plt.tight_layout()
    cm_path = eval_dir / f"confusion_matrix_{timestamp}.png"
    plt.savefig(cm_path, dpi=150)
    plt.close()
    
    # ROC Curves (for multi-class)
    if hasattr(model, 'predict_proba'):
        n_classes = len(class_names)
        fpr = dict()
        tpr = dict()
        roc_auc = dict()
        
        plt.figure(figsize=(10, 8))
        for i in range(n_classes):
            fpr[i], tpr[i], _ = roc_curve(y_test == i, y_pred_proba[:, i])
            roc_auc[i] = auc(fpr[i], tpr[i])
            plt.plot(fpr[i], tpr[i], lw=2, label=f'{class_names[i]} (AUC = {roc_auc[i]:.3f})')
        
        plt.plot([0, 1], [0, 1], 'k--', lw=2)
        plt.xlim([0.0, 1.0])
        plt.ylim([0.0, 1.05])
        plt.xlabel('False Positive Rate')
        plt.ylabel('True Positive Rate')
        plt.title('ROC Curves')
        plt.legend(loc="lower right")
        plt.tight_layout()
        roc_path = eval_dir / f"roc_curves_{timestamp}.png"
        plt.savefig(roc_path, dpi=150)
        plt.close()
    
    # Feature importance (if available)
    if hasattr(model, 'feature_importances_'):
        importances = model.feature_importances_
        indices = np.argsort(importances)[::-1][:20]
        
        plt.figure(figsize=(10, 8))
        plt.bar(range(len(indices)), importances[indices])
        plt.xticks(range(len(indices)), [f"F{i}" for i in indices], rotation=45)
        plt.xlabel('Feature Index')
        plt.ylabel('Importance')
        plt.title('Top 20 Feature Importances')
        plt.tight_layout()
        fi_path = eval_dir / f"feature_importance_{timestamp}.png"
        plt.savefig(fi_path, dpi=150)
        plt.close()
    
    # Save JSON results
    results = {
        'evaluation_info': {
            'evaluation_id': f"eval_{timestamp}_001",
            'evaluation_date': datetime.now().isoformat(),
            'model_name': model.__class__.__name__,
            'test_set_size': len(y_test)
        },
        'overall_metrics': {
            'accuracy': report['accuracy'],
            'precision_macro': report['macro avg']['precision'],
            'recall_macro': report['macro avg']['recall'],
            'f1_macro': report['macro avg']['f1-score']
        },
        'per_class_metrics': {
            class_names[i]: {
                'precision': report[class_names[i]]['precision'],
                'recall': report[class_names[i]]['recall'],
                'f1': report[class_names[i]]['f1-score'],
                'support': report[class_names[i]]['support']
            } for i in range(len(class_names))
        },
        'roc_auc_scores': roc_auc if 'roc_auc' in dir() else None,
        'confusion_matrix': cm.tolist()
    }
    
    json_path = eval_dir / f"evaluation_{timestamp}.json"
    with open(json_path, 'w') as f:
        json.dump(results, f, indent=2)
    
    # Generate HTML report
    html_path = eval_dir / f"evaluation_{timestamp}.html"
    await generate_evaluation_html(results, cm_path, roc_path, html_path)
    
    return {
        'json': str(json_path),
        'html': str(html_path),
        'confusion_matrix': str(cm_path),
        'roc_curves': str(roc_path) if 'roc_path' in dir() else None,
        'feature_importance': str(fi_path) if 'fi_path' in dir() else None
    }
Experiment Tracking
Experiment Configuration
json
{
  "experiment_id": "exp_001_baseline",
  "name": "Baseline Random Forest",
  "description": "Baseline model with default hyperparameters",
  "created_date": "2024-01-15T10:00:00Z",
  "status": "completed",
  "configuration": {
    "model_type": "RandomForestClassifier",
    "hyperparameters": {
      "n_estimators": 100,
      "max_depth": null,
      "min_samples_split": 2,
      "min_samples_leaf": 1,
      "max_features": "sqrt"
    },
    "feature_set": "all_46_features",
    "data_split": {
      "train": 0.7,
      "validation": 0.15,
      "test": 0.15
    },
    "random_seed": 42
  },
  "results": {
    "accuracy": 0.912,
    "f1_macro": 0.894,
    "training_time_seconds": 45.2,
    "inference_time_ms": 12.5
  },
  "artifacts": {
    "model": "models/classifier_exp001.pkl",
    "scaler": "models/scaler_exp001.pkl",
    "evaluation": "evaluations/evaluation_exp001.json"
  }
}
Run Experiment
python
async def run_experiment(config, output_dir="data/exports/ml/experiments"):
    """Run and track ML experiment"""
    
    from datetime import datetime
    import json
    import time
    
    experiment_id = f"exp_{datetime.now().strftime('%Y%m%d_%H%M%S')}"
    
    # Log experiment start
    experiment = {
        'experiment_id': experiment_id,
        'name': config['name'],
        'description': config.get('description', ''),
        'start_time': datetime.now().isoformat(),
        'status': 'running',
        'configuration': config
    }
    
    # Save experiment config
    config_path = Path(output_dir) / f"{experiment_id}_config.json"
    with open(config_path, 'w') as f:
        json.dump(experiment, f, indent=2)
    
    try:
        start_time = time.time()
        
        # Train model
        model = train_model(config)
        
        training_time = time.time() - start_time
        
        # Evaluate
        metrics = evaluate_model(model, config)
        
        # Save results
        results = {
            'experiment_id': experiment_id,
            'status': 'completed',
            'end_time': datetime.now().isoformat(),
            'training_time_seconds': training_time,
            'results': metrics,
            'model_path': f"models/{experiment_id}.pkl"
        }
        
        results_path = Path(output_dir) / f"{experiment_id}_results.json"
        with open(results_path, 'w') as f:
            json.dump(results, f, indent=2)
        
        return experiment_id, results
        
    except Exception as e:
        # Log failure
        error = {
            'experiment_id': experiment_id,
            'status': 'failed',
            'end_time': datetime.now().isoformat(),
            'error': str(e)
        }
        
        error_path = Path(output_dir) / f"{experiment_id}_error.json"
        with open(error_path, 'w') as f:
            json.dump(error, f, indent=2)
        
        raise
Data Versioning
Version Management
python
class MLDataVersion:
    """Manage versions of ML training data"""
    
    def __init__(self, data_dir="data/exports/ml"):
        self.data_dir = Path(data_dir)
        self.version_file = self.data_dir / "versions.json"
    
    def create_version(self, version, description, datasets):
        """Create new data version"""
        
        version_info = {
            'version': version,
            'created_date': datetime.now().isoformat(),
            'description': description,
            'datasets': datasets,
            'checksums': {}
        }
        
        # Calculate checksums
        for name, path in datasets.items():
            file_path = self.data_dir / path
            if file_path.exists():
                version_info['checksums'][name] = self._calculate_md5(file_path)
        
        # Load existing versions
        versions = self._load_versions()
        versions[version] = version_info
        
        with open(self.version_file, 'w') as f:
            json.dump(versions, f, indent=2)
        
        return version_info
    
    def get_version(self, version):
        """Get specific version info"""
        versions = self._load_versions()
        return versions.get(version)
    
    def list_versions(self):
        """List all versions"""
        versions = self._load_versions()
        return [{'version': v, 'created_date': info['created_date'], 
                'description': info['description']} 
                for v, info in versions.items()]
    
    def _load_versions(self):
        if self.version_file.exists():
            with open(self.version_file, 'r') as f:
                return json.load(f)
        return {}
    
    def _calculate_md5(self, file_path):
        import hashlib
        md5 = hashlib.md5()
        with open(file_path, 'rb') as f:
            for chunk in iter(lambda: f.read(4096), b""):
                md5.update(chunk)
        return md5.hexdigest()
Integration Examples
Load Data for Training
python
import numpy as np
import json
from sklearn.ensemble import RandomForestClassifier

def load_training_data(version="latest"):
    """Load training data for model training"""
    
    if version == "latest":
        # Load latest dataset
        features = np.load('data/exports/ml/labeled/training_set.npy')
        labels = np.load('data/exports/ml/labeled/training_set_labels.npy')
    else:
        # Load specific version
        version_info = load_version_info(version)
        features = np.load(version_info['datasets']['training_features'])
        labels = np.load(version_info['datasets']['training_labels'])
    
    return features, labels

# Usage
X_train, y_train = load_training_data()
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)
Load Pre-trained Model
python
import pickle
import json

def load_production_model():
    """Load the latest production model"""
    
    # Load model metadata
    with open('data/exports/ml/models/model_metadata.json', 'r') as f:
        metadata = json.load(f)
    
    # Load model
    with open(metadata['model_path'], 'rb') as f:
        model = pickle.load(f)
    
    # Load scaler
    with open(metadata['scaler_path'], 'rb') as f:
        scaler = pickle.load(f)
    
    return model, scaler, metadata
Storage Guidelines
Retention Policy
Data Type	Retention	Compression	Archive
Feature exports	90 days	gzip	Quarterly
Labeled datasets	1 year	None	Permanent
Evaluation results	1 year	None	Permanent
Model artifacts	Permanent	None	Versioned
Experiment logs	6 months	gzip	Quarterly
Raw training data	30 days	gzip	Monthly
Storage Limits
python
def check_ml_storage():
    """Check ML data storage usage"""
    
    ml_dir = Path("data/exports/ml")
    total_size = sum(f.stat().st_size for f in ml_dir.rglob("*") if f.is_file())
    size_gb = total_size / (1024 ** 3)
    
    limits = {
        'warning': 5,     # 5 GB warning
        'critical': 10,   # 10 GB critical
        'max': 20         # 20 GB maximum
    }
    
    return {
        'size_gb': size_gb,
        'file_count': len(list(ml_dir.rglob("*"))),
        'status': 'ok' if size_gb < limits['warning'] else 'warning' if size_gb < limits['critical'] else 'critical'
    }
Troubleshooting
Common Issues
Issue	Cause	Solution
Features mismatch	Version inconsistency	Check feature names and order
Memory error	Dataset too large	Use chunked loading
Model loading fails	Pickle version	Use compatible Python version
Missing dependencies	Library not installed	Install required packages
Data Validation
python
def validate_ml_export(export_path):
    """Validate ML export integrity"""
    
    export_path = Path(export_path)
    
    if export_path.suffix == '.npy':
        try:
            data = np.load(export_path)
            return {'valid': True, 'shape': data.shape, 'dtype': str(data.dtype)}
        except Exception as e:
            return {'valid': False, 'error': str(e)}
    
    elif export_path.suffix == '.json':
        try:
            with open(export_path, 'r') as f:
                data = json.load(f)
            return {'valid': True, 'keys': list(data.keys())}
        except Exception as e:
            return {'valid': False, 'error': str(e)}
    
    elif export_path.suffix == '.pkl':
        try:
            with open(export_path, 'rb') as f:
                data = pickle.load(f)
            return {'valid': True, 'type': str(type(data))}
        except Exception as e:
            return {'valid': False, 'error': str(e)}
    
    return {'valid': False, 'error': 'Unknown format'}
Best Practices
Data Versioning
python
# Recommended versioning scheme
VERSIONING_SCHEME = {
    'format': 'v{major}.{minor}.{patch}',
    'major': 'Breaking changes (feature set changes)',
    'minor': 'New features or samples added',
    'patch': 'Bug fixes or minor updates'
}

# Example versions
VERSIONS = {
    'v1.0.0': 'Initial release - 46 features, 10,000 samples',
    'v1.1.0': 'Added 2,500 samples, 5 new drone types',
    'v2.0.0': 'Added 8 new features, removed 3 deprecated features'
}
Model Export Checklist
Export model in multiple formats (pickle, ONNX)

Save feature scaler

Include model metadata

Generate model card

Record evaluation metrics

Save feature importance

Document dependencies

Calculate model checksum
