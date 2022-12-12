## Install Singularity on WSL


#### Motivation
When we do high performance computing (HPC) on cluster, the corresponding running environment should also be uploaded. In the other words, the programs should work in a specific container.
Luckily, Singlularity is just doing this. It's a platform that can load various containers. 
Plus, Singularity is mainly used on Linux system. But personally I prefer to Windows system, in order to run programs on Linux, Windows Subsystem Linux (WSL) is a good choise.

Thus, this note records the installation of Singularity on WSL.
![flowchart](https://github.com/jizhang02/Figure-Factory/blob/becd08a8af7027a7f77a6cbcce654f6f810972f3/Fig_CS/Figure-Factory-install%20singularity.drawio.png)
#### Installlation and Test
* step 1 -> Start: open terminal of WSL
* step 2 -> install Singularity: [official user guide](https://docs.sylabs.io/guides/latest/user-guide/quick_start.html)
* step 3 -> pull a container: `sudo singularity -d build --sandbox sandbox_anaconda/ docker://continuumio/anaconda3`  
* step 4 -> run: `sudo singularity run --writable sandbox_anaconda/`
* step 5 -> install libraries: `apt-get update`; `apt install -y vim`; `pip install opengate`
* step 6 -> install missing libraries
* step 7 -> Test: `python`; `import opengate`
* step 8 -> Build the container into image: `sudo singularity build conda_single.sif sandbox_anaconda/`

#### Note
In step 5, before installing opengate or a library, I create a conda environment via `conda create -n mc python=3.9`, this can prevent from being affected by other complicated settings. To make the `mc` environment as default, change the `~/.bashrc`, add a line `conda activate mc` or `export PATH="/opt/conda/envs/mc/bin:$PATH" `, then `source ~/.bashrc` to make it into effect.

In step 7, when I want run a real program, it should mount a folder where the data and scripts are located in.    
`sudo singularity shell -B /my absolute path conda_single.sif`

#### Reference
  * [Singularity 容器使用介绍](https://www.xiexianbin.cn/hpc/singularity/index.html)
  * [Singularity实践教程 + Docker 转 Singularity 的避坑指南](https://blog.csdn.net/Tanqy1997/article/details/125304273)
  * [anaconda设置默认的启动环境](https://blog.csdn.net/weixin_40548136/article/details/106331324)
  * [Docker Image Anaconda3](https://hub.docker.com/r/continuumio/anaconda3)
  * [missing libraries when installing opengate](https://stackoverflow.com/questions/55313610/importerror-libgl-so-1-cannot-open-shared-object-file-no-such-file-or-directo)
