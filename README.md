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
sudo apt install libmetis-dev               # Optional: for mesh partitioning
pip3 install virtualenv

```
2. Install libxsmm:
```
git clone https://github.com/libxsmm/libxsmm.git
cd libxsmm
make clean  # If rebuilding
make -j4 STATIC=0 BLAS=0 CC=gcc-12 CXX=g++-12 FC=gfortran-12
