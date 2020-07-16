# Developability of Heightfields
Public code release for "Developability of Heightfields via Rank Minimization", presented at SIGGRAPH 2020 and authored by Silvia Sellán, Noam Aigerman and Alec Jacobson



## Installation
To use this library, please start by cloning the repository recursively
```
git clone --recursive https://github.com/sgsellan/developability-of-heightfields.git
```
After this, we will build the mex functions in the `gptoolbox` directory:
```
cd developability-of-heightfields/gptoolbox/mex
mkdir build
cd build
cmake ..
make
```
Then, build our own mex files by entering Matlab and, in Matlab, adding this repository in its entirety to your Matlab path (for instance, by running `addpath(genpath(path/to/developability-of-heightfields))`), navigating to `developability-of-heightfields/mex` and running `setup_mex` in the Matlab console.

## Use
