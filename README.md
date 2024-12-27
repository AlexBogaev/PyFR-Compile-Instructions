# PyFR
## Overview

PyFR is an open-source Python based framework for solving advection-diffusion
type problems on streaming architectures using the Flux Reconstruction
approach of Huynh. The framework is designed to solve a range of governing
systems on mixed unstructured grids containing various element types. It is
also designed to target a range of hardware platforms via use of an in-built
domain specific language derived from the Mako templating engine.

## Examples

Test cases are available in the
[PyFR-Test-Cases](https://github.com/PyFR/PyFR-Test-Cases) repository.

## Installation

### Install PyFR on Ubuntu
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
cd ..
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
pyfr --help    # Should display PyFR help information
```

# Gmsh
## Overview
Gmsh is an automatic three-dimensional finite element mesh generator with built-in pre- and post-processing facilities.

### Install Gmsh on Ubuntu
1. To install or upgrade Gmsh:
```bash
sudo apt install gmsh
```

After installation you can either run the Gmsh GUI app:
```
gmsh
```

Or use the command line interface:
```
gmsh input.geo -[dimension] -o output.msh
```

# Conduit and Ascent Visualization
## Overview
Conduit and Ascent are required for in-situ visualization capabilities in PyFR. Conduit provides data description services, while Ascent enables visualization of simulation data.

## Installation
### Install Conduit and Ascent on Ubuntu

1. Install build dependencies:
```bash
sudo apt update
sudo apt install cmake build-essential libopenmpi-dev openmpi-bin curl
```

2. Install Conduit:
```
git clone --recursive https://github.com/llnl/conduit.git
cd conduit
python3 scripts/uberenv/uberenv.py --install --prefix="build"
cd ..
```

3. Install Ascent with MPI support:
```
git clone --recursive https://github.com/alpine-dav/ascent.git
cd ascent

# Clean any existing builds
rm -rf build/
rm -rf src/

# Build with MPI and OpenMP support
env prefix=build \
    enable_mpi=ON \
    enable_cuda=OFF \
    enable_openmp=OFF \
    ./scripts/build_ascent/build_ascent.sh
cd ..
```

4. Configure environment (add to ~/.bashrc):
```
# PyFR Ascent configuration
export PYFR_CONDUIT_LIBRARY_PATH=/home/username/conduit/build/spack/conduit-install/lib/libconduit.so
export PYFR_ASCENT_MPI_LIBRARY_PATH=/home/username/ascent/build/install/ascent-develop/lib/libascent_mpi.so
export LD_LIBRARY_PATH=/home/username/ascent/build/install/vtk-m-v2.1.0/lib:$LD_LIBRARY_PATH

# After editing ~/.bashrc, either start a new terminal or run:
source ~/.bashrc
```
Note: Replace /home/username/ with your actual home directory path.

