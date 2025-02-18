# Installing faceswap
- [Installing faceswap](#Installing-faceswap) 安装 faceswap
- [Prerequisites](#Prerequisites) 前提条件
  - [Hardware Requirements](#Hardware-Requirements) 硬件需求
  - [Supported operating systems](#Supported-operating-systems) 支持的操作系统
- [Important before you proceed](#Important-before-you-proceed)  在继续之前重要的事
- [Windows Install Guide](#Windows-Install-Guide) 安装指南
  - [Installer](#Installer) 安装器
  - [Manual Install](#Manual-Install) 手动安装
  - [Prerequisites](#Prerequisites-1) 前提条件
    - [Anaconda](#Anaconda)
    - [Git](#Git)
  - [Setup](#Setup) 安装
    - [Anaconda](#Anaconda-1)
      - [Set up a virtual environment](#Set-up-a-virtual-environment)
      - [Entering your virtual environment](#Entering-your-virtual-environment)
    - [faceswap](#faceswap)
      - [Easy install](#Easy-install)
      - [Manual install](#Manual-install)
  - [Running faceswap](#Running-faceswap)
  - [Create a desktop shortcut](#Create-a-desktop-shortcut)
  - [Updating faceswap](#Updating-faceswap)
- [General Install Guide](#General-Install-Guide)
  - [Installing dependencies](#Installing-dependencies)
    - [Git](#Git-1)
    - [Python](#Python)
    - [Virtual Environment](#Virtual-Environment)
  - [Getting the faceswap code](#Getting-the-faceswap-code)
  - [Setup](#Setup-1)
    - [About some of the options](#About-some-of-the-options)
  - [Run the project](#Run-the-project)
  - [Notes](#Notes)

# Prerequisites
Machine learning essentially involves a ton of trial and error. You're letting a program try millions of different settings to land on an algorithm that sort of does what you want it to do. This process is really really slow unless you have the hardware required to speed this up. 

机器学习基本上都会涉及大量的尝试和错误的结果, 你让一个程序尝试上百万种不同的设置，然后在某种程度上实现你想要的算法。这个过程是很慢很慢的，除非你使用硬件加速它。

The type of computations that the process does are well suited for graphics cards, rather than regular processors. **It is pretty much required that you run the training process on a desktop or server capable GPU.** Running this on your CPU means it can take weeks to train your model, compared to several hours on a GPU.       
该过程所做的计算类型非常适合图形卡，而不是常规处理器。**这就非常需要你在有GPU的机器上跑训练过程**如果在CPU上跑会很慢。

## Hardware Requirements
**TL;DR: you need at least one of the following: 你至少需要满足下面一个条件**

- **A powerful CPU**
    - Laptop CPUs can often run the software, but will not be fast enough to train at reasonable speeds       
    - 笔记本上的CPU通常是可以跑这个软件的，但是会特别的慢。
- **A powerful GPU**
    - Currently, Nvidia GPUs are fully supported. and AMD graphics cards are partially supported through plaidML.         
    - 现在 GPU 已经完全支持了，并且AMD图像卡只是部分支持。     
    - If using an Nvidia GPU, then it needs to support at least CUDA Compute Capability 3.0 or higher.        
    - 如果用GPU，它需要至少支持CUDA Compute Capability 3.0 或者更高。     
      To see which version your GPU supports, consult this list: https://developer.nvidia.com/cuda-gpus        
      可以在https://developer.nvidia.com/cuda-gpus 中查看你的GOU支持哪一个版本。     
      Desktop cards later than the 7xx series are most likely supported.         
      最有可能支持7xx系列以后的桌面卡。
- **A lot of patience**

## Supported operating systems 
- **Windows 10**
  Windows 7 and 8 might work. Your mileage may vary. Windows has an installer which will set up everything you need. See: https://github.com/deepfakes/faceswap/releases
- **Linux**
  Most Ubuntu/Debian or CentOS based Linux distributions will work.
- **macOS**
  GPU support on macOS is limited due to lack of drivers/libraries from Nvidia.
- **All operating systems must be 64-bit for Tensorflow to run.**     
- **所有的操作系统必须支持64位的TensorFlow**

Alternatively, there is a docker image that is based on Debian.

# Important before you proceed 
**In its current iteration, the project relies heavily on the use of the command line, although a gui is available. if you are unfamiliar with command line tools, you may have difficulty setting up the environment and should perhaps not attempt any of the steps described in this guide.** This guide assumes you have intermediate knowledge of the command line.      
 在当前版本中，尽管图形界面已经可以用了，但是在此项目中还是很依赖用命令行执行步骤，如果你不熟悉命令行的工具，你也许很难去设置环境并且可能不应尝试本指南中描述的任何步骤。本指南假设你了解命令行的知识。    
The developers are also not responsible for any damage you might cause to your own computer.     
开发者们也不会负责关于你在使用此项目中你电脑受损的情况。     

# Windows Install Guide

## Installer
Windows now has an installer which installs everything for you and creates a desktop shortcut to launch straight into the GUI. You can download the installer from https://github.com/deepfakes/faceswap/releases.     
Windows 现在有安装器，它可以帮你安装好所有的事情并且在桌面创建一个快捷方式去直接启动GUI。你可以从 https://github.com/deepfakes/faceswap/releases 中下载安装器。

If you have issues with the installer then read on for the more manual way to install faceswap on Windows.     
如果你用安装器遇到了问题，你可以使用手动的方式去安装faceswap。

## Manual Install

Setting up faceswap can seem a little intimidating to new users, but it isn't that complicated, although a little time consuming. It is recommended to use Linux where possible as Windows will hog about 20% of your GPU Memory, making faceswap run a little slower, however using Windows is perfectly fine and 100% supported.     
对于新手来说安装faceswap看起来似乎有点害怕，尽管安装过程有点耗时，但是它并不复杂。我们建议尽可能的使用Linux系统，因为用Windows的话会多占20%的GPU内存, 并使得换脸的过程会慢一点，但是是100%支持Windows系统的。

## Prerequisites

### Anaconda
Download and install the latest Python 3 Anaconda from: https://www.anaconda.com/download/. Unless you know what you are doing, you can leave all the options at default.      
从下面网址中安装Anaconda3 https://www.anaconda.com/download/ 你可以保持所有的默认选择，除非你知道你在做什么。

### Git
Download and install Git for Windows: https://git-scm.com/download/win. Unless you know what you are doing, you can leave all the options at default.      
在Windows中下载Git从下面的网址  https://git-scm.com/download/win  保持默认选项即可。    

## Setup
Reboot your PC, so that everything you have just installed gets registered.     
重启你的机器，让刚才安装的软件在系统中注册成功。

### Anaconda
#### Set up a virtual environment
- Open up Anaconda Navigator
- Select "Environments" on the left hand side
- Select "Create" at the bottom
- In the pop up:
    - Give it the name: faceswap
    - **IMPORTANT**: Select python version 3.6
    - Hit "Create" (NB: This may take a while as it will need to download Python 3.6)
![Anaconda virtual env setup](https://i.imgur.com/Tl5tyVq.png)

#### Entering your virtual environment
To enter the virtual environment:
- Open up Anaconda Navigator
- Select "Environments" on the left hand side
- Hit the ">" arrow next to your faceswap environment and select "Open Terminal"
![Anaconda enter virtual env](https://i.imgur.com/rKSq2Pd.png)

### faceswap
- If you are not already in your virtual environment follow [these steps](#entering-your-virtual-environment)
- Get the faceswap repo by typing: `git clone --depth 1 https://github.com/deepfakes/faceswap.git`
- Enter the faceswap folder: `cd faceswap`

#### Easy install
- Enter the command `python setup.py` and follow the prompts:
- If you have issues/errors follow the Manual install steps below.

#### Manual install
Do not follow these steps if the Easy Install above completed succesfully.
- Install tkinter (required for the GUI) by typing: `conda install tk`
- Install requirements: `pip install -r requirements.txt`
- Install Tensorflow (either GPU or CPU version depending on your setup):
    - GPU Version: `conda install tensorflow-gpu`
    - Non GPU Version: `conda install tensorflow`

## Running faceswap
- If you are not already in your virtual environment follow [these steps](#entering-your-virtual-environment)
- Enter the faceswap folder: `cd faceswap`
- Enter the following to see the list of commands: `python faceswap.py -h` or enter `python faceswap.py gui` to launch the GUI

## Create a desktop shortcut
A desktop shortcut can be added to easily launch straight into the faceswap GUI:

- Open Notepad
- Paste the following:
```
%USERPROFILE%\Anaconda3\envs\faceswap\python.exe %USERPROFILE%/faceswap/faceswap.py gui
```
- Save the file to your desktop as "faceswap.bat"

## Updating faceswap
It's good to keep faceswap up to date as new features are added and bugs are fixed. To do so:
- If using the GUI you can go to the Tools Menu and select "Check for Updates...". This will update faceswap to the latest code and update your dependencies.
- If you are not already in your virtual environment follow [these steps](#entering-your-virtual-environment)
- Enter the faceswap folder: `cd faceswap`
- Enter the following `git pull --all`
- Once the latest version has downloaded, make sure your dependencies are up to date. There is a script to help with this: `python update_deps.py`

# General Install Guide
## Installing dependencies
### Git
Git is required for obtaining the code and keeping your codebase up to date.
Obtain git for your distribution from the [git website](https://git-scm.com/downloads).

### Python
The recommended install method is to use a Conda3 Environment as this will handle the installation of Nvidia's CUDA and cuDNN straight into your Conda Environment. This is by far the easiest and most reliable way to setup the project.
  - MiniConda3 is recommended: [MiniConda3](https://docs.conda.io/en/latest/miniconda.html)
  
Alternatively you can install Python (>= 3.2-3.7 64-bit) for your distribution (links below.) If you go down this route and are using an Nvidia GPU you should install CUDA (https://developer.nvidia.com/cuda-zone) and cuDNN (https://developer.nvidia.com/cudnn). for your system. If you do not plan to build Tensorflow yourself, make sure you install no higher than version 10.0 of CUDA and 7.5.x of CUDNN.
  - Python distributions:
    - apt/yum install python3 (Linux)
    - [Installer](https://www.python.org/downloads/release/python-368/) (Windows)
    - [brew](https://brew.sh/) install python3 (macOS)

### Virtual Environment
  It is highly recommended that you setup faceswap inside a virtual environment. In fact we will not generally support installations that are not within a virtual environment as troubleshooting package conflicts can be next to impossible.

  If using Conda3 then setting up virtual environments is relatively straight forward. More information can be found at [Conda Docs](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)

  If using a default Python distribution then [virtualenv](https://github.com/pypa/virtualenv) and [virtualenvwrapper](https://virtualenvwrapper.readthedocs.io) may help when you are not using docker.


## Getting the faceswap code
It is recommended to clone the repo with git instead of downloading the code from http://github.com/deepfakes/faceswap and extracting it as this will make it far easier to get the latest code (which can be done from the GUI). To clone a repo you can either use the Git GUI for your distribution or open up a command prompt, enter the folder where you want to store faceswap and enter:
```bash
git clone https://github.com/deepfakes/faceswap.git
```


## Setup
Enter your virtual environment and then enter the folder that faceswap has been downloaded to and run:
```bash
python setup.py
```
If setup fails for any reason you can still manually install the packages listed within requirements.txt

### About some of the options
   - CUDA: For acceleration. Requires a good nVidia Graphics Card (which supports CUDA inside)
   - Docker: Provide a ready-made image. Hide trivial details. Get you straight to the project.
   - nVidia-Docker: Access to the nVidia GPU on host machine from inside container.

CUDA with Docker in 20 minutes.
```
INFO    The tool provides tips for installation
        and installs required python packages
INFO    Setup in Linux 4.14.39-1-MANJARO
INFO    Installed Python: 3.6.5 64bit
INFO    Installed PIP: 10.0.1
Enable  Docker? [Y/n] 
INFO    Docker Enabled
Enable  CUDA? [Y/n] 
INFO    CUDA Enabled
INFO    1. Install Docker
        https://www.docker.com/community-edition
        
        1. Install Nvidia-Docker & Restart Docker Service
        https://github.com/NVIDIA/nvidia-docker
        
        1. Build Docker Image For faceswap
        docker build -t deepfakes-gpu -f Dockerfile.gpu .
        
        1. Mount faceswap volume and Run it
        # without gui. tools.py gui not working.
        nvidia-docker run --rm -it -p 8888:8888 \
            --hostname faceswap-gpu --name faceswap-gpu \
            -v /opt/faceswap:/srv \
            deepfakes-gpu
        
        # with gui. tools.py gui working.
        ## enable local access to X11 server
        xhost +local:
        ## enable nvidia device if working under bumblebee
        echo ON > /proc/acpi/bbswitch
        ## create container 
        nvidia-docker run -p 8888:8888 \
            --hostname faceswap-gpu --name faceswap-gpu \
            -v /opt/faceswap:/srv \
            -v /tmp/.X11-unix:/tmp/.X11-unix \
            -e DISPLAY=unix$DISPLAY \
            -e AUDIO_GID=`getent group audio | cut -d: -f3` \
            -e VIDEO_GID=`getent group video | cut -d: -f3` \
            -e GID=`id -g` \
            -e UID=`id -u` \
            deepfakes-gpu
        
        1. Open a new terminal to interact with the project
        docker exec faceswap-gpu python /srv/faceswap.py gui
```

A successful setup log, without docker.
```
INFO    The tool provides tips for installation
        and installs required python packages
INFO    Setup in Linux 4.14.39-1-MANJARO
INFO    Installed Python: 3.6.5 64bit
INFO    Installed PIP: 10.0.1
Enable  Docker? [Y/n] n
INFO    Docker Disabled
Enable  CUDA? [Y/n] 
INFO    CUDA Enabled
INFO    CUDA version: 9.1
INFO    cuDNN version: 7
WARNING Tensorflow has no official prebuild for CUDA 9.1 currently.
        To continue, You have to build your own tensorflow-gpu.
        Help: https://www.tensorflow.org/install/install_sources
Are System Dependencies met? [y/N] y
INFO    Installing Missing Python Packages...
INFO    Installing tensorflow-gpu
INFO    Installing pathlib==1.0.1
......
INFO    Installing tqdm
INFO    Installing matplotlib
INFO    All python3 dependencies are met.
        You are good to go.
```

## Run the project
Once all these requirements are installed, you can attempt to run the faceswap tools. Use the `-h` or `--help` options for a list of options.

```bash
python faceswap.py -h
```

or run with `gui` to launch the GUI
```bash
python faceswap.py gui
```


Proceed to [../blob/master/USAGE.md](USAGE.md)

## Notes
This guide is far from complete. Functionality may change over time, and new dependencies are added and removed as time goes on. 

If you are experiencing issues, please raise them in the [faceswap Forum](https://faceswap.dev/forum) instead of the main repo. Usage questions raised in the issues within this repo are liable to be closed without response.
