# Running deep learning programs under tensorflow GPU

The workflow of performing a dl program under WSL/Linux system:
### Writing dl programs
  - language: Python (version 3.9)
  - environment: Anaconda
  - library: `pip install tensorflow` (version 2.11.0); etc.
### Runing dl programs on CPU
  - test if it is runnable
### Running dl programs on GPU
  - new environment: tf-gpu (`conda create -n tf-gpu`)
  - under **tf-gpu**:
    - `nvidia-smi` after installing the NVIDIA GPU driver
    - `conda install -c conda-forge cudatoolkit=11.2 cudnn=8.1.0`
    - Configure the system paths. `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$CONDA_PREFIX/lib/`
    - `pip install --upgrade pip`
    - `pip install tensorflow` (version 2.11.0); etc.
    - Verify install `python` -> `import tensorflow as tf` -> `print(tf.reduce_sum(tf.random.normal([1000, 1000])))` `print(tf.config.list_physical_devices('GPU'))`. If output is `[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]`, then succeessful.
    - test if it is runnable
 * Running dl programs on Cluster GPU
   - pull a image `sudo singularity -d build --sandbox sandbox_tensorflow/ docker://continuumio/anaconda3`
   - open image and install libraries in it `sudo singularity run --writable sandbox_tensorflow/`
   - install tensorflow which already supports cpu and gpu `pip install tensorflow`
   - build the container into image: `sudo singularity build tensorflow_single.sif sandbox_tensorflow/`
   - uploading image file `tensorflow_single.sif` to cluster
   - write shell file, select specific available GPU [example](/docs/SLURM.md)
   - run `sbatch test.sh`
  ### Reference
  * [tensorflow install guide](https://www.tensorflow.org/install/pip#windows-wsl2_1)
