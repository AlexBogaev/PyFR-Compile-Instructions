# PyFR
## Overview
[existing overview content...]

## Installation

### Ubuntu 22.04 LTS
Follow these steps to install PyFR with OpenMP backend support:

1. Install system dependencies:
```bash
sudo apt update
sudo apt install python3 python3-pip libopenmpi-dev openmpi-bin
sudo apt install gcc-12 g++-12 gfortran-12  # Required for OpenMP 5.1 support
pip3 install virtualenv

```
2. Install libxsmm:
```
git clone https://github.com/libxsmm/libxsmm.git
cd libxsmm
make -j4 STATIC=0 BLAS=0 CC=gcc-12 CXX=g++-12 FC=gfortran-12

```
3. Setup Python virtual environment:
```
python3 -m virtualenv pyfr-venv
source pyfr-venv/bin/activate

```
4. Install PyFR:
```
pip install pyfr

```
5. Configure environment (add to ~/.bashrc):
```
# Add to end of ~/.bashrc
export PYFR_XSMM_LIBRARY_PATH=/path/to/libxsmm/lib/libxsmm.so
# After editing ~/.bashrc, either start a new terminal or run:
source ~/.bashrc

```
To verify the installation:
```
activate-pyfr  # Activate the virtual environment
pyfr --help    # Should display PyFR help information

