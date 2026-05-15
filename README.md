# GeneticBitcoinSolver Tests

This directory contains comprehensive tests to validate the functionality of the Bitcoin Puzzle genetic solver.

## Test List

1. **test_gpu_kernels.py** - Tests basic GPU kernel operations
2. **test_gpu_integration.py** - Tests integration between GPU kernels and the genetic solver
3. **test_checkpoint.py** - Tests save and load checkpoint functionality
4. **test_gpu_kernels_fixed.py** - Enhanced GPU kernel tests with comprehensive validation
5. **robust_validation_test.py** - Validation tests using real solved Bitcoin puzzles (31-50)
6. **run_all_tests.sh** - Script to run all tests at once

## Running Tests

### Individual Test

To run a specific test:

```bash
python tests/test_gpu_kernels.py
python tests/test_gpu_integration.py
python tests/test_checkpoint.py
python tests/robust_validation_test.py
All Tests
To run all tests at once:

bash
./tests/run_all_tests.sh
Quick Test Mode
For faster testing with smaller parameters:

bash
python tests/test_gpu_integration.py --quick
python tests/test_gpu_kernels_fixed.py
GPU Verification
To test if GPU acceleration is working correctly:

bash
./scripts/test_gpu_acceleration.sh
Or manually:

bash
python -c "from src.environment_detector import get_environment_detector; env = get_environment_detector(); print(f'CUDA: {env.cuda_available}, ROCm: {env.rocm_available}, MPS: {env.mps_available}')"
Test Categories
Unit Tests
Environment detection

GPU kernel initialization

Public key generation

Fitness calculation

SHA-256 hashing

Integration Tests
GPU + Genetic Algorithm integration

Checkpoint save/restore

Multi-strategy coordination

Validation Tests
Real puzzle validation (puzzles 31-50)

Performance benchmarking

Cross-algorithm comparison

Performance Tests
Batch processing efficiency

GPU vs CPU comparison

Scaling analysis

Test Results
Test results will be displayed in the console. If all tests pass, you will see success messages. Otherwise, specific error messages will be displayed.

Test Output Example
text
🚀 COMPLETE GPU KERNELS TEST SUITE
============================================================
Date/Time: 2024-01-15 10:30:00
Python Version: 3.10.12

🧪 ENVIRONMENT DETECTION TEST
==================================================
Environment: local
CPU Cores: 8
CUDA GPU: ✓
ROCm GPU: ✗
Apple MPS: ✗
Total RAM: 15.6 GB

✅ GPU detected successfully

📊 TEST SUMMARY
============================================================
Total tests: 9
Passed: 9
Failed: 0

✅ ALL TESTS PASSED!
Troubleshooting
Common Issues
GPU not detected

Verify GPU drivers are installed

Check if PyTorch with CUDA/ROCm support is installed

Run: python -c "import torch; print(torch.cuda.is_available())"

Module not found errors

Install required dependencies: pip install -r requirements.txt

Activate virtual environment: source venv/bin/activate

Permission denied for shell scripts

Make scripts executable: chmod +x tests/run_all_tests.sh scripts/*.sh

Checkpoint tests failing

Ensure write permissions in project directory

Check disk space availability

Performance Notes
GPU acceleration performance depends on available hardware

For NVIDIA GPUs, significant performance gains are expected (typically 10-50x)

For AMD GPUs, support is experimental (ROCm required)

For Apple Silicon (MPS), support is also experimental but promising

CPU-only mode will work but will be slower for large populations

Expected Performance Gains
Hardware	Expected Speedup	Notes
NVIDIA RTX 3090	20-50x	Full CUDA support
NVIDIA RTX 3060	10-30x	Good CUDA support
AMD RX 6800	5-15x	ROCm required
Apple M1/M2	3-10x	MPS support
CPU Only	1x	Fallback mode
Adding New Tests
To add a new test:

Create a new Python file in the tests/ directory

Name it following the pattern test_*.py

Use pytest conventions for test functions

Add the test to run_all_tests.sh if appropriate

Update this README with the new test information

Test Template
python
#!/usr/bin/env python3
"""
Test description here
"""

import sys
import os
sys.path.append(os.path.abspath(os.path.join(os.path.dirname(__file__), '..')))

def test_feature():
    """Test feature functionality"""
    # Test implementation
    assert True

if __name__ == "__main__":
    test_feature()
    print("✅ Test passed!")
Continuous Integration
These tests are designed to run in CI/CD environments:

GitHub Actions

GitLab CI

Jenkins

Local development

CI Configuration Example
yaml
# .github/workflows/test.yml
name: Tests
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.10'
      - name: Install dependencies
        run: pip install -r requirements.txt
      - name: Run tests
        run: ./tests/run_all_tests.sh
Test Coverage
Current test coverage areas:

✅ Environment detection (100%)

✅ GPU kernel operations (90%)

✅ Genetic algorithm basics (85%)

✅ Checkpoint system (95%)

✅ Key saving (90%)

✅ Blockchain forensics (70%)

⚠️ Advanced strategies (60%)

⚠️ Full puzzle solving (N/A - requires long runtime)
