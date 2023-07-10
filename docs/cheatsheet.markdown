### Odyssey in computer science
---
####  Pytorch
* `torch.cuda.is_available()` check cuda
* `tensorboard --logdir=/home/jing/python_code/DeepRT/torch/runs` use tensorboard web graph
* 
#### Conda
* `conda --version` check version
* `conda env list` exsisted environments
* `conda install python==3.6` install specific python
* `conda create -n name python=3.9` create a conda env
* `conda create -n newenv --clone oldenv` copy a conda env
* `conda remove -n envname --all` delete a conda env
* `conda activate envname` activate a conda env
* `conda deactivate` close a conda env
* export to another machone 
  * `conda env export > envname.yaml`
  * `conda env create -f envname.yaml`
#### Python
* `print(sys.version)` print python version
* `print(glob.glob("path/*.mhd"))` print files names
* ` files = os.listdir(path);    files.sort()` sort the files names
* `for x, y in zip(directory_image, directory_label):` double loop
* interpreters/environments
  * Windows-> Python3.8 _for basics_
  * Ubuntu->Anaconda->mc    Python3.8 _for opengate_
  * Ubuntu->Anaconda->base    Python3.8 _for basics_
  * Ubuntu->Anaconda->tf-gpu    Python3.8 _for tensorflow gpu_
  * Ubuntu->Anaconda->torch-gpu    Python3.8 _for pytorch gpu_
* `print(f'text {variable:.3f}')` print in specific format
#### Terminal
* `hostname -I` ip address
* `ps -ef | grep ssh` check ssh
* `python --version` check python version
* `nvidia-smi` check GPU info
* `nvidia-smi -L` check available GPU
* `htop` check memory
* `touch test.py` create a new file
* `vi test.py` edit a file
* `cd ~` come to home
* `bash xxx.sh` run .sh file
* `sudo vim /home/jing/.bashrc` modigy environment variables
* `export PATH=path1:path2: ...... :$PATH` add multiple variables
* `source ~/.bashrc` make it into effect
* `unset PYTORCH_CUDA_ALLOC_CONF` cancel the previous command
* `sudo apt-get update` update software
* `pip install opengate -U` update lib
* `sudo apt-get remove --auto-remove qtcreator` uninstall software
* `scp -r /datapath/* username@ip address:/savepath/` upload data to cluster
* `ls -l . | egrep -c '^-'` check file numbers
* `ffmpeg -i input.mp3 -ss 00:01:00 -to 00:05:23.27 -c copy output.mp3` edit audio length
* 
#### WSL=Windows subsystom linux
* A good subsitute for vmware virtual machine.
* 动态IP地址设置为静态 [solution](https://github.com/microsoft/WSL/issues/4150#issuecomment-504209723)-> failed.
* version ` wsl -l -v`
* `sudo apt-get install x11-apps ` to support visualization, `xeyes` for testing
#### Opengate
* GitHub https://github.com/OpenGATE/opengate
* two parts
  * opengate_core -> C++ based
  * opengate -> Python based 
* Units

      micrometer              (um)        微米
      millimeter              (mm)        毫米
      centimeter              (cm)        厘米
      meter                   (m)         米
      nanosecond              (ns)        纳秒
      second                  (second)    秒
      Kilo election Volt      (KeV)       千电子伏特
      Mega electron Volt      (MeV)       兆电子伏特
      positron charge         (eplus)     正电子电荷
      degree Kelvin           (kelvin)    温度计量单位
      the amount of substance (mole)      摩尔，物质的量
      luminous intensity      (candela)   坎德拉，发光强度
      radian                  (radian)    弧度
      steradian               (steradian) 球面度
      Becquerel               (Bq)        贝克，放射性活度，每秒衰变的原子个数
      gcm3                    (g/cm3)     克每立方厘米，密度单位


* Simulation
  * Geometry
  * Physics
  * Source
  * Actors
* Stats

      NumberOfRun               = 1
      NumberOfEvents            = 20000
      NumberOfTracks            = 103511
      NumberOfSteps             = 726120
      NumberOfGeometricalSteps  = 27558
      NumberOfPhysicalSteps     = 698562
      PPS (Primary per sec)     = 7998.91
      TPS (Track per sec)       = 41398.7
      SPS (Step per sec)        = 290408

#### Hybrid programming between python and C/C++
* Essence: python calls dynamic link libraries compiled by C/C++. e.g. convert the data types in python to those in c/c++, pass them to the compiled functions, and then convert returned parameters to the data types in python.
* C/C++ --> dynamic link library (Pybind11) <-- Python

#### Medical Image Analysis Using FIJI software
* open/import a specific file in different formats
* zoom in/out an image: +/- key
* browse a slice: left/right key
* see 3D image in 3 directions
  * stacks->orthogonal views  
  * stacks->reslice '/' key
* compute mean/std value: 'm' key
  * results/analyse->set measurements
  * the whole slice
  * the selected area 
* Image->Lookup Tables, set different show ways
* Analyse->Plot profile, make a plot of selected area
* Image->Stacks->Statistics, statistics of a image
* Image->Show Info, save image info to a file
* Color bar: Analyze > Tools > Calibration Bar
* View 3D imagein 3 directions: Ctrl+Shift+H
* Image > Stacks > Make Montage: show all slices in a table
* Image > Stacks > Images to Stack: make multiple images into a stack
* Process > Enhance Contrast: show pet image more clearly
* Image > Overlay: add another image on the current image
* 

#### Medical Image Analysis Using Slicer software
* generate a gif 
  * Modules-> Utilities->ScreenCapture
  * Output type: video, image series, lightbox image
* show : click left-up coner buttons on three views respectily
* Colar bar: Volume > Color Legend. Or right click the image to show the color legent
* Overlay: Left upper coner of show panel > F > B 
* MIP: Lookup tables > PET-Maximum Intensity Projection
* Isodose: In radiotherapy, set threshold value of each line

#### Latex
adjust blank:

`\setlength{\abovedisplayskip}{3pt} `    
`\setlength{\belowdisplayskip}{3pt}`    
adjust the space between title and fig
`\setlength{\abovecaptionskip}{-0.2cm}`    
adjust the distance between title and the below context
`\setlength{\belowcaptionskip}{-1cm} `

```\begin{equation}
\setlength{\abovedisplayskip}{3pt}
\setlength{\belowdisplayskip}{3pt}
y(t)=a(t)-b(t).
\end{equation}```
