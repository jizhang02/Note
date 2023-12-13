## Install OpenGATE on WSL


#### Motivation
OpenGATE is a work in progress. I record the installation and test process in Windows Subsystem Linux (WSL). We can regard this system as a duo system (Windows and Linux) or a virtual machine, anyway, it's convenient to use both two systems.

#### Installlation and Test

1. Install WSL: open CMD, input `wsl --install`, for detail, see [Official tutorial](https://learn.microsoft.com/en-us/windows/wsl/install#Overview) .
2. Install Anaconda in WSL terminal: download the package on Win, then copy to the WSL dirctory like `home/user/`, then input `bash package.sh`, then following the instructions.
3. Create conda environment: input  `conda create -n gate python=3.9`
4. Install OpenGATE in the `gate` environment: `pip install -pre opengate`
5. Test: input `opengate_tests` install the missing lib according to the instructions, mainly `.so` files. e.g. `conda install -c conda-forge libstdcxx-ng` `conda install qt=5`Also pay attention to step 6.
6. Declare path `export PATH="/opt/conda/envs/gate/bin:$PATH"` in the terminal(temporal) or write in the `~/.bashrc`(permanent), then `source ~/.bashrc`, to make it into effect.
