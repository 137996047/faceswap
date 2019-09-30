# deepfakes_faceswap
<p align="center">
  <a href="https://faceswap.dev"><img src="https://i.imgur.com/zHvjHnb.png"></img></a>
<br />FaceSwap is a tool that utilizes deep learning to recognize and swap faces in pictures and videos.    
FaceSwap 是一个工具：使用深度学习识别和交换图像中和视频中的人脸。
</p>
<p align="center">
<img src = "https://i.imgur.com/nWHFLDf.jpg"></img>
</p>

<p align="center">
<a href="https://www.patreon.com/bePatron?u=23238350"><img src="https://c5.patreon.com/external/logo/become_a_patron_button.png"></img></a>
</p>
<p align="center">
  <a href="https://www.youtube.com/watch?v=r1jng79a5xc"><img src="https://img.youtube.com/vi/r1jng79a5xc/0.jpg"></img></a>
<br />Jennifer Lawrence/Steve Buscemi FaceSwap using the Villain model
</p>

[![Build Status](https://travis-ci.org/deepfakes/faceswap.svg?branch=master)](https://travis-ci.org/deepfakes/faceswap) [![Documentation Status](https://readthedocs.org/projects/faceswap/badge/?version=latest)](https://faceswap.readthedocs.io/en/latest/?badge=latest)

Make sure you check out [INSTALL.md](INSTALL.md) before getting started.    
在开始之前请确保核对 [INSTALL.md](INSTALL.md)文件。


- [deepfakes_faceswap](#deepfakesfaceswap)
- [Manifesto](#manifesto)
  - [FaceSwap has ethical uses.](#faceswap-has-ethical-uses)
- [How To setup and run the project](#how-to-setup-and-run-the-project)
- [Overview](#overview)
  - [Extract](#extract)
  - [Train](#train)
  - [Convert](#convert)
  - [GUI](#gui)
- [General notes:](#general-notes)
- [Help I need support!](#help-i-need-support)
  - [Discord Server](#discord-server)
  - [FaceSwap Forum](#faceswap-forum)
- [Donate](#donate)
  - [Patreon](#patreon)
  - [One time Donations](#one-time-donations)
    - [@torzdf](#torzdf)
    - [@andenixa](#andenixa)
    - [@kvrooman](#kvrooman)
- [How to contribute](#how-to-contribute)
  - [For people interested in the generative models](#for-people-interested-in-the-generative-models)
  - [For devs](#for-devs)
  - [For non-dev advanced users](#for-non-dev-advanced-users)
  - [For end-users](#for-end-users)
  - [For haters](#for-haters)
- [About github.com/deepfakes](#about-githubcomdeepfakes)
  - [What is this repo?](#what-is-this-repo)
  - [Why this repo?](#why-this-repo)
  - [Why is it named 'deepfakes' if it is not /u/deepfakes?](#why-is-it-named-deepfakes-if-it-is-not-udeepfakes)
  - [What if /u/deepfakes feels bad about that?](#what-if-udeepfakes-feels-bad-about-that)
- [About machine learning](#about-machine-learning)
  - [How does a computer know how to recognize/shape faces? How does machine learning work? What is a neural network?](#how-does-a-computer-know-how-to-recognizeshape-faces-how-does-machine-learning-work-what-is-a-neural-network)

# Manifesto

## FaceSwap has ethical uses.

When faceswapping was first developed and published, the technology was groundbreaking, it was a huge step in AI development. It was also completely ignored outside of academia because the code was confusing and fragmentary. It required a thorough understanding of complicated AI techniques and took a lot of effort to figure it out. Until one individual brought it together into a single, cohesive collection. It ran, it worked, and as is so often the way with new technology emerging on the internet, it was immediately used to create inappropriate content. Despite the inappropriate uses the software was given originally, it was the first AI code that anyone could download, run and learn by experimentation without having a Ph.D. in math, computer theory, psychology, and more. Before "deepfakes" these techniques were like black magic, only practiced by those who could understand all of the inner workings as described in esoteric and endlessly complicated books and papers.    
当Faceswapping最初被开发和发布时，该技术是开创性的，这是AI开发的一大步。在学术界之外，它也被完全忽略了，因为该代码是混乱和零碎的。它需要对复杂的AI技术有透彻的了解，并花了很多精力才能解决。直到一个人将其汇集成一个单一的，有凝聚力的集合。 它能跑通了并在能正常工作，并且随着互联网上出现新技术的方式如此频繁，它立即被用于创建不合适的内容。 尽管最初使用该软件的目的不当，但它是第一个无需博士就可以完成下载，运行和学习的AI代码。 也不需要了解相关的数学，计算机理论，心理学等等知识。 在“Deepfakes”之前，这些技术就像是黑魔法，只有那些了解深奥而无穷无尽的书籍和论文中所描述的所有内部工作原理的人才能实践。

"Deepfakes" changed all that and anyone could participate in AI development. To us, developers, the release of this code opened up a fantastic learning opportunity. It allowed us to build on ideas developed by others, collaborate with a variety of skilled coders, experiment with AI whilst learning new skills and ultimately contribute towards an emerging technology which will only see more mainstream use as it progresses.      
“ Deepfakes”改变了这一切，任何人都可以参与AI开发。 对于我们开发人员而言，此代码的发布带来了绝佳的学习机会。 它使我们能够借鉴其他人提出的想法，与各种熟练的编码人员合作，在学习新技能的同时尝试AI，并最终为新兴技术做出贡献，随着技术的进步，这种技术只会看到更多的主流用途。


Are there some out there doing horrible things with similar software? Yes. And because of this, the developers have been following strict ethical standards. Many of us don't even use it to create videos, we just tinker with the code to see what it does. Sadly, the media concentrates only on the unethical uses of this software. That is, unfortunately, the nature of how it was first exposed to the public, but it is not representative of why it was created, how we use it now, or what we see in its future. Like any technology, it can be used for good or it can be abused. It is our intention to develop FaceSwap in a way that its potential for abuse is minimized whilst maximizing its potential as a tool for learning, experimenting and, yes, for legitimate faceswapping.     
有没有人用类似的软件做可怕的事情？ 是。 因此，开发人员一直遵循严格的道德标准。 我们许多人甚至不使用它来创建视频，我们只是修改代码以查看其功能。 可悲的是，媒体只专注于该软件的不道德使用。 不幸的是，这就是它首次向公众公开的性质，但不能代表其创建原因，我们现在的使用方式或未来的前景。 像任何技术一样，它可以永久使用或被滥用。 我们的目的是开发FaceSwap，以便最大程度地减少其滥用的可能性，同时最大程度地提高其作为学习，实验以及是的合法换脸工具的潜力。

We are not trying to denigrate celebrities or to demean anyone. We are programmers, we are engineers, we are Hollywood VFX artists, we are activists, we are hobbyists, we are human beings. To this end, we feel that it's time to come out with a standard statement of what this software is and isn't as far as us developers are concerned.

我们不是要毁名人或贬低任何人。 我们是程序员，我们是工程师，我们是好莱坞VFX艺术家，我们是激进主义者，我们是业余爱好者，我们是人类。 为此，我们认为是时候就该软件的含义和哪些不是我们开发人员要关心的问题而发表声明了。

- FaceSwap is not for creating inappropriate content.
- FaceSwap 不是为了创造不合适的内容而生的。
- FaceSwap is not for changing faces without consent or with the intent of hiding its use.
- FaceSwap 不适用于未经同意或隐藏其使用目的而换脸
- FaceSwap is not for any illicit, unethical, or questionable purposes.
- FaceSwap 不适于任何非法，不道德或可疑目的。
- FaceSwap exists to experiment and discover AI techniques, for social or political commentary, for movies, and for any number of ethical and reasonable uses.
- FaceSwap的存在是为了实验和发现AI技术，用于社会或政治评论，电影以及各种道德和合理用途的实验。

We are very troubled by the fact that FaceSwap can be used for unethical and disreputable things. However, we support the development of tools and techniques that can be used ethically as well as provide education and experience in AI for anyone who wants to learn it hands-on. We will take a zero tolerance approach to anyone using this software for any unethical purposes and will actively discourage any such uses.     
 
FaceSwap可用于不道德和败坏名誉的事情这一事实使我们感到非常困扰。 但是，我们支持开发可合乎道德使用的工具和技术，并为想要动手学习的人提供AI方面的教学和经验。 对于出于任何不道德目的使用本软件的人，我们将采取零容忍的态度，并将积极劝阻任何此类使用。

# How To setup and run the project
FaceSwap is a Python program that will run on multiple Operating Systems including Windows, Linux, and MacOS.

See [INSTALL.md](INSTALL.md) for full installation instructions. You will need a modern GPU with CUDA support for best performance. AMD GPUs are partially supported.

# Overview
The project has multiple entry points. You will have to:
 - Gather photos and/or videos
 - **Extract** faces from your raw photos
 - **Train** a model on the faces extracted from the photos/videos
 - **Convert** your sources with the model

Check out [USAGE.md](USAGE.md) for more detailed instructions.

## Extract
From your setup folder, run `python faceswap.py extract`. This will take photos from `src` folder and extract faces into `extract` folder.

## Train
From your setup folder, run `python faceswap.py train`. This will take photos from two folders containing pictures of both faces and train a model that will be saved inside the `models` folder.

## Convert
From your setup folder, run `python faceswap.py convert`. This will take photos from `original` folder and apply new faces into `modified` folder.

## GUI
Alternatively, you can run the GUI by running `python faceswap.py gui`

# General notes:
- All of the scripts mentioned have `-h`/`--help` options with arguments that they will accept. You're smart, you can figure out how this works, right?!

NB: there is a conversion tool for video. This can be accessed by running `python tools.py effmpeg -h`. Alternatively, you can use [ffmpeg](https://www.ffmpeg.org) to convert video into photos, process images, and convert images back to the video.


**Some tips:**

Reusing existing models will train much faster than starting from nothing.
If there is not enough training data, start with someone who looks similar, then switch the data.

# Help I need support!
## Discord Server
Your best bet is to join the [FaceSwap Discord server](https://discord.gg/FC54sYg) where there are plenty of users willing to help. Please note that, like this repo, this is a SFW Server!

## FaceSwap Forum
Alternatively, you can post questions in the [FaceSwap Forum](https://faceswap.dev/forum). Please do not post general support questions in this repo as they are liable to be deleted without response.

# Donate
The developers work tirelessly to improve and develop FaceSwap. Many hours have been put in to provide the software as it is today, but this is an extremely time-consuming process with no financial reward. If you enjoy using the software, please consider donating to the devs, so they can spend more time implementing improvements.

## Patreon
The best way to support us is through our Patreon page:

[![become-a-patron](https://c5.patreon.com/external/logo/become_a_patron_button.png)](https://www.patreon.com/bePatron?u=23238350)

## One time Donations
Alternatively you can give a one off donation to any of our Devs:
### @torzdf
 There is very little FaceSwap code that hasn't been touched by torzdf. He is responsible for implementing the GUI, FAN aligner, MTCNN detector and porting the Villain, DFL-H128 and DFaker models to FaceSwap, as well as significantly improving many areas of the code.

**Bitcoin:** 385a1r9tyZpt5LyZcNk1FALTxC8ZHta7yq

**Ethereum:** 0x18CBbff5fA7C78de7B949A2b0160A0d1bd649f80

**Paypal:** [![torzdf](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=JZ8PP3YE9J62L)

### @andenixa
Creator of the Unbalanced and OHR models, as well as expanding various capabilities within the training process. Andenixa is currently working on new models and will take requests for donations.

**Paypal:** [![andenixa](https://www.paypalobjects.com/en_GB/i/btn/btn_donate_SM.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=NRVLQYGS6NWTU)

### @kvrooman
Responsible for consolidating the converters, adding a lot of code to fix model stability issues, and helping significantly towards making the training process more modular, kvrooman continues to be a very active contributor.

**Ethereum:** 0x18CBbff5fA7C78de7B949A2b0160A0d1bd649f80

# How to contribute

## For people interested in the generative models
 - Go to the 'faceswap-model' to discuss/suggest/commit alternatives to the current algorithm.

## For devs
 - Read this README entirely
 - Fork the repo
 - Play with it
 - Check issues with the 'dev' tag
 - For devs more interested in computer vision and openCV, look at issues with the 'opencv' tag. Also feel free to add your own alternatives/improvements

## For non-dev advanced users
 - Read this README entirely
 - Clone the repo
 - Play with it
 - Check issues with the 'advuser' tag
 - Also go to the '[faceswap Forum](https://faceswap.dev/forum)' and help others.

## For end-users
 - Get the code here and play with it if you can
 - You can also go to the [faceswap Forum](https://faceswap.dev/forum) and help or get help from others.
 - Be patient. This is a relatively new technology for developers as well. Much effort is already being put into making this program easy to use for the average user. It just takes time!
 - **Notice** Any issue related to running the code has to be opened in the [faceswap Forum](https://faceswap.dev/forum)!

## For haters
Sorry, no time for that.

# About github.com/deepfakes

## What is this repo?
It is a community repository for active users.

## Why this repo?
The joshua-wu repo seems not active. Simple bugs like missing _http://_ in front of urls have not been solved since days.

## Why is it named 'deepfakes' if it is not /u/deepfakes?
 1. Because a typosquat would have happened sooner or later as project grows
 2. Because we wanted to recognize the original author
 3. Because it will better federate contributors and users

## What if /u/deepfakes feels bad about that?
This is a friendly typosquat, and it is fully dedicated to the project. If /u/deepfakes wants to take over this repo/user and drive the project, he is welcomed to do so (Raise an issue, and he will be contacted on Reddit). Please do not send /u/deepfakes messages for help with the code you find here.

# About machine learning

## How does a computer know how to recognize/shape faces? How does machine learning work? What is a neural network?
It's complicated. Here's a good video that makes the process understandable:
[![How Machines Learn](https://img.youtube.com/vi/R9OHn5ZF4Uo/0.jpg)](https://www.youtube.com/watch?v=R9OHn5ZF4Uo)

Here's a slightly more in depth video that tries to explain the basic functioning of a neural network:
[![How Machines Learn](https://img.youtube.com/vi/aircAruvnKk/0.jpg)](https://www.youtube.com/watch?v=aircAruvnKk)

tl;dr: training data + trial and error
