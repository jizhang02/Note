# Singularity container with tensorflow/pytorch GPU

#### Step 0: Make sure `nvidia-smi` worked after installing the NVIDIA GPU driver
   
> Every CUDA toolkit also ships with an NVIDIA display driver package for convenience. This driver supports all the features introduced in that version of the CUDA Toolkit. [Nvidia official guide](https://developer.nvidia.com/cuda-downloads)

#### Step 1: Download container, build it into sandbox
`sudo singularity -d build --sandbox sandbox_tensorflow  docker://tensorflow/tensorflow:tags`    
`sudo singularity -d build --sandbox sandbox_torch  docker://pytorch/pytorch:tags`

👉 Note: the `tags` depends on own requests, see DockerHub:    
[https://hub.docker.com/r/tensorflow/tensorflow/tags](https://hub.docker.com/r/tensorflow/tensorflow/tags)    
[https://hub.docker.com/r/pytorch/pytorch/tags](https://hub.docker.com/r/pytorch/pytorch/tags)    

#### Step 2: Install specific python libraries in sandbox    
  
`sudo singularity build --sandbox image_name/ image_name.sif` Convert a singularity image to a sandox folder with superuse privileges       
`sudo singularity shell --writable sandbox_tensorflow/` Shell writable to image_name       
`sudo singularity shell --writable sandbox_torch/`   
   
`pip install libname`    
test:    
`python`   
`import libname`    

#### Step 3: Build sandbox into image file     
`sudo singularity build image_tensorflow.sif sandbox_tensorflow/`    
`sudo singularity build image_torch.sif sandbox_torch/`    

#### Step 4: Run python file in image file
* on the cluster
`srun singularity exec --nv /home/jzhang/image_tensorflow.sif python3 test.py`  [shell example](/docs/SLURM.md), run `sbatch test.sh`      
* on the local machine 
`sudo singularity exec --nv /home/jzhang/image_torch.sif python3 test.py`    

test.py
```
# import torch

# print(torch.__version__)
# print(torch.cuda.is_available())
# print(torch.cuda.device_count())
# print(torch.cuda.device(0))
# print(torch.cuda.current_device())
# print(torch.cuda.get_device_name(0))

import tensorflow as tf 

print(tf.__version__)
print(tf.test.is_gpu_available())
print(tf.config.list_physical_devices('GPU'))    
```
