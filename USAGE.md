# Workflow

**Before attempting any of this, please make sure you have read, understood and completed the [installation instructions](../master/INSTALL.md). If you are experiencing issues, please raise them in the [faceswap Forum](https://faceswap.dev/forum) or the [FaceSwap Discord server](https://discord.gg/FdEwxXd) instead of the main repo.**

- [Workflow](#Workflow)
- [Introduction](#Introduction)
  - [Disclaimer](#Disclaimer)
  - [Getting Started](#Getting-Started)
- [Extract](#Extract)
  - [Gathering raw data](#Gathering-raw-data)
  - [Extracting Faces](#Extracting-Faces)
  - [General Tips](#General-Tips)
- [Training a model](#Training-a-model)
  - [General Tips](#General-Tips-1)
- [Converting a video](#Converting-a-video)
  - [General Tips](#General-Tips-2)
- [GUI](#GUI)
- [Video's](#Videos)
- [EFFMPEG](#EFFMPEG)
- [Extracting video frames with FFMPEG](#Extracting-video-frames-with-FFMPEG)
- [Generating a video](#Generating-a-video)
- [Notes](#Notes)
  
# Introduction

## Disclaimer
This guide provides a high level overview of the faceswapping process. It does not aim to go into every available option, but will provide a useful entry point to using the software. There are many more options available that are not covered by this guide. These can be found, and explained, by passing the `-h` flag to the command line (eg: `python faceswap.py extract -h`) or by hovering over the options within the GUI.     

本指南概述了换脸过程。 它的目的不是深入解释所有可用的选项，而是为使用该软件提供有用的切入点。 本指南未涵盖所有可用选项，不过可以通过在命令行中传递-h标志（例如：pythonfaceswap.py extract -h）或将鼠标悬停在GUI中的选项中来找到这些选项和对应的解释。


## Getting Started
So, you want to swap faces in pictures and videos? Well hold up, because first you gotta understand what this application will do, how it does it and what it can't currently do.     
因此，您想交换图片和视频中的面孔吗？ 好吧，因为首先您要了解此应用程序将要执行的操作，其执行方式以及当前无法执行的操作。

The basic operation of this script is simple. It trains a machine learning model to recognize and transform two faces based on pictures. The machine learning model is our little "bot" that we're teaching to do the actual swapping and the pictures are the "training data" that we use to train it. Note that the bot is primarily processing faces. Other objects might not work.      
该脚本的基本操作很简单。 它训练一种机器学习模型，以基于图片识别和变换两个面孔。 机器学习模型是我们正在教做实际交换的小“机器人”，而图片是我们用来训练它的“训练数据”。 请注意，机器人主要处理人脸。 其他对象可能不起作用。

So here's our plan. We want to create a reality where Donald Trump lost the presidency to Nic Cage; we have his inauguration video; let's replace Trump with Cage.      
我们有个计划，我们创造处一个情景，Cage扮演的Trump 失去总统职位的演讲。我们有Trump的视频，让我们用Cage将Trump替换掉就好。


# Extract
## Gathering raw data
In order to accomplish this, the bot needs to learn to recognize both face A (Trump) and face B (Nic Cage). By default, the bot doesn't know what a Trump or a Nic Cage looks like. So we need to show it lots of pictures and let it guess which is which. So we need pictures of both of these faces first.
为了完成这个事情，机器需要学习识别A和B。在默认情况下，机器是不知道A和B看起来是什么样子的。所以我们需要给机器看大量的图片，让他猜哪个是哪个，所以我们首先需要A和B的面孔图片。     

A possible source is Google, DuckDuckGo or Bing image search. There are scripts to download large amounts of images. A better source of images are videos (from interviews, public speeches, or movies) as these will capture many more natural poses and expressions. Fortunately FaceSwap has you covered and can extract faces from both still images and video files. See [Extracting video frames](#Extracting_video_frames) for more information.      
一种可能的来源就是从网上搜索，有些脚本可以下载大量图像。 更好的图像来源是视频（来自访谈，公开演讲或电影），因为这些视频将捕获更多自然的姿势和表情。 幸运的是，FaceSwap已为您服务，可以从静止图像和视频文件中提取面部。从 [Extracting video frames](#Extracting_video_frames) 中可以查看更多的信息.      

Feel free to list your image sets in the [faceswap Forum](https://faceswap.dev/forum), or add more methods to this file.

So now we have a folder full of pictures/videos of Trump and a separate folder of Nic Cage. Let's save them in our directory where we put the FaceSwap project. Example: `~/faceswap/src/trump` and `~/faceswap/src/cage`

## Extracting Faces
So here's a problem. We have a ton of pictures and videos of both our subjects, but these are just of them doing stuff or in an environment with other people. Their bodies are on there, they're on there with other people... It's a mess. We can only train our bot if the data we have is consistent and focuses on the subject we want to swap. This is where FaceSwap first comes in.     
但是这有一个问题，我们有关于我们两个主题的大量图片和视频，但是这些知识他们的一些素材，图片和视频里面有可能包含大量的其他的人或者身体部位或者背景等等，这些都是我们不关心的。我们只想让机器关注我们感兴趣要交换的东西（脸部）上，所以需要面部提取。这也是FaceSwap首次出现的地方。


**Command Line:**
```bash
# To extract trump from photos in a folder:
python faceswap.py extract -i ~/faceswap/src/trump -o ~/faceswap/faces/trump
# To extract trump from a video file:
python faceswap.py extract -i ~/faceswap/src/trump.mp4 -o ~/faceswap/faces/trump
# To extract cage from photos in a folder:
python faceswap.py extract -i ~/faceswap/src/cage -o ~/faceswap/faces/cage
# To extract cage from a video file:
python faceswap.py extract -i ~/faceswap/src/cage.mp4 -o ~/faceswap/faces/cage
```

**GUI:**

To extract trump from photos in a folder (Right hand folder icon):
![ExtractFolder](https://i.imgur.com/H3h0k36.jpg)

To extract cage from a video file (Left hand folder icon):
![ExtractVideo](https://i.imgur.com/TK02F0u.jpg)

For input we either specify our photo directory or video file and for output we specify the folder where our extracted faces will be saved. The script will then try its best to recognize face landmarks, crop the images to a consistent size, and save the faces to the output folder. An `alignments.json` file will also be created and saved into your input folder. This file contains information about each of the faces that will be used by FaceSwap.       
对于输入我们可以指定图片的路径或者视频文件，对于输出我们需要指定从图片或者视频中提取出来的人脸所存储的路径。这个脚本将完成人脸关键点的识别、人脸的提取矫正并将图片输出到指定的文件中。`alignments.json`文件也会被创建并且保存到输入的文件夹中，这个文件包含了在FaceSwap中使用的每个人脸的信息。


Note: this script will make grabbing test data much easier, but it is not perfect. It will (incorrectly) detect multiple faces in some photos and does not recognize if the face is the person whom we want to swap. Therefore: **Always check your training data before you start training.** The training data will influence how good your model will be at swapping.     
该脚本将使获取测试数据更加容易，但这并不是完美的。 它会（错误地）检测到某些照片中的多张面孔，并且无法识别该面孔是否是我们要交换的人。因此：**始终在开始训练之前检查训练数据。**因为训练数据将影响模型在交换时的性能。

## General Tips
When extracting faces for training, you are looking to gather around 500 to 5000 faces for each subject you wish to train. These should be of a high quality and contain a wide variety of angles, expressions and lighting conditions.       
提取面部进行训练时，您希望为每个想要训练的主题收集500至5000张面部。 这些应该是高质量的，并且包含各种各样的角度，表情和照明条件。

You do not want to extract every single frame from a video for training as from frame to frame the faces will be very similar.     
我们不想提取视频中的每一帧图像，因为连续帧图像之间的脸部基本没什么变化很相似。

If you plan to train with a mask or use the Warp to Landmarks option, then you will need to copy the output `alignments.json` file from your source frames folder into your output faces folder for training. If you have extracted from multiple sources, you can use the alignments tool to merge several `alignments.json` files together.       
如果你想使用mask 或者 warp to landmarks 的选项的话，需要将`alignments.json` 文件也拷贝到，输出的人脸文件夹中，用于训练使用。如果是从多个资源提取的人脸，则需要将`alignments.json` 文件合并到一起。

Some of the plugins have configurable options. You can find the config options in: `<faceswap_folder>\config\extract.ini`. You will need to have run Extract or the GUI at least once for this file to be generated.      
一些插件具有可配置的选项。 您可以在以下目录中找到配置选项：`<faceswap_folder> \ config \ extract.ini`。 您至少需要运行一次Extract或GUI才能生成此文件。 

# Training a model
Ok, now you have a folder full of Trump faces and a folder full of Cage faces. What now? It's time to train our bot! This creates a 'model' that contains information about what a Cage is and what a Trump is and how to swap between the two.     
好，现在你有两个文件，一个是A的face, 一个是B的face。现在需要去训练模型，我们会创建一个模型，它包含了什么是A和什么是B以及如果去换他们俩的信息。

The training process will take the longest, how long depends on many factors; the model used, the number of images, your GPU etc. However, a ballpark figure is 12-48 hours on GPU and weeks if training on CPU.      
训练的过程是耗时最长的，他取决于很多因素，模型大小、数据量、GPU等等。但是，在GPU上的大致数字是12-48小时，而在CPU上训练则是数周。

We specify the folders where the two faces are, and where we will save our training model.      
我们需要指定两个人脸文件的地址，以及我们模型保存的地址。

**Command Line:**
```bash
python faceswap.py train -A ~/faceswap/faces/trump -B ~/faceswap/faces/cage -m ~/faceswap/trump_cage_model/
# or -p to show a preview
python faceswap.py train -A ~/faceswap/faces/trump -B ~/faceswap/faces/cage -m ~/faceswap/trump_cage_model/ -p 
```
**GUI:**

![Training](https://i.imgur.com/j8bjk4I.jpg)

Once you run the command, it will start hammering the training data. If you have a preview up, then you will see a load of blotches appear. These are the faces it is learning. They don't look like much, but then your model hasn't learned anything yet. Over time these will more and more start to resemble trump and cage.     
一旦运行命令，它将开始锻造训练数据。如果你有预览，你将会看到大量的斑点出现，这是学习人脸的过程。而且他们看起来并不相似，因模型还没有学到任何东西。不过随着模型的训练它们开始越来越相似。

You want to leave your model learning until you are happy with the images in the preview. To stop training you can:     
您想让模型学习，直到对预览中的图像满意为止。 要停止训练，您可以：
- Command Line: press "Enter" in the preview window or in the console
- GUI: Press the Terminate button

When stopping training, the model will save and the process will exit. This can take a little while, so be patient. The model will also save every 100 iterations or so.     
停止训练后，模型将保存，并且过程将退出。 这可能需要一些时间，请耐心等待。 该模型还会每100迭代保存一个模型。

You can stop and resume training at any time. Just point FaceSwap at the same folders and carry on.     
您可以随时停止并继续训练。 只需将FaceSwap指向相同的文件夹并继续。


## General Tips
If you are training with a mask or using Warp to Landmarks, you will need to pass in an `alignments.json` file for each of the face sets. See [Extract - General Tips](#general-tips) for more information.      
如果你训练中用到了mask或者 Warp to Landmarks, 您需要用到 `alignments.json`文件，详情请看[Extract - General Tips](#general-tips)。

The model is automatically backed up at every save iteration where the overall loss has dropped (i.e. the model has improved). If your model corrupts for some reason, you can go into the model folder and remove the `.bk` extension from the backups to restore the model from backup.      


You can see the full list of arguments for training by hovering over the options in the GUI or passing the help flag. i.e:

```bash
python faceswap.py train -h
```

Some of the plugins have configurable options. You can find the config options in: `<faceswap_folder>\config\train.ini`. You will need to have run Train or the GUI at least once for this file to be generated.


# Converting a video
Now that we're happy with our trained model, we can convert our video. How does it work? 

Well firstly we need to generate an `alignments.json` file for our swap. To do this, follow the steps in [Extracting Faces](#extracting-faces), only this time you want to run extract for every face in your source video. This file tells the convert process where the face is on the source frame.

You are likely going to want to cleanup your alignments file, by deleting false positives, badly aligned faces etc. These will not look good on your final convert. There are tools to help with this.

Just like extract you can convert from a series of images or from a video file.

Remember those initial pictures we had of Trump? Let's try swapping a face there. We will use that directory as our input directory, create a new folder where the output will be saved, and tell them which model to use.

**Command Line:**
```bash
python faceswap.py convert -i ~/faceswap/src/trump/ -o ~/faceswap/converted/ -m ~/faceswap/trump_cage_model/
```

**GUI:**

![convert](https://i.imgur.com/GzX1ME2.jpg)

It should now start swapping faces of all these pictures.


## General Tips
You can see the full list of arguments for training by hovering over the options in the GUI or passing the help flag. i.e:

```bash
python faceswap.py convert -h
```

Some of the plugins have configurable options. You can find the config options in: `<faceswap_folder>\config\convert.ini`. You will need to have run Convert or the GUI at least once for this file to be generated.

# GUI
All of the above commands and options can be run from the GUI. This is launched with:
```bash
python faceswap.py gui
```

The GUI allows a more user friendly interface into the scripts and also has some extended functionality. Hovering over options in the GUI will tell you more about what the option does.

# Video's
A video is just a series of pictures in the form of frames. Therefore you can gather the raw images from them for your dataset or combine your results into a video.

# EFFMPEG
You can perform various video processes with the built-in effmpeg tool. You can see the full list of arguments available by running:
```bash
python tools.py effmpeg -h
```

# Extracting video frames with FFMPEG
Alternatively, you can split a video into separate frames using [ffmpeg](https://www.ffmpeg.org) for instance. Below is an example command to process a video to separate frames.

```bash
ffmpeg -i /path/to/my/video.mp4 /path/to/output/video-frame-%d.png
```

# Generating a video
If you split a video, using [ffmpeg](https://www.ffmpeg.org) for example, and used them as a target for swapping faces onto you can combine these frames again. The command below stitches the png frames back into a single video again.

```bash
ffmpeg -i video-frame-%0d.png -c:v libx264 -vf "fps=25,format=yuv420p" out.mp4
```

# Notes
This guide is far from complete. Functionality may change over time, and new dependencies are added and removed as time goes on. 

If you are experiencing issues, please raise them in the [faceswap Forum](https://faceswap.dev/forum) or the [FaceSwap Discord server](https://discord.gg/FdEwxXd). Usage questions raised in this repo are likely to be closed without response.
