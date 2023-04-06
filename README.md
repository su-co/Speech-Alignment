# 语音对齐使用教程

[TOC]

## 什么是语音对齐？

字或音素和相应的音频对齐，通俗来讲，我们KTV里面的歌词和声音是能够对应显示的，可以精确到每一个字和声音对应，这个就是要靠音频和文本对齐来实现。一方面可以靠人工去标注，另一方面就是靠机器的算法去自动对齐。



## 使用什么工具？

主要使用Montreal Forced Aligner开源软件，这个工具是可以用python包的形式安装，底层依赖于[kaldi](https://www.zhihu.com/search?q=kaldi&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A1795942752})进行语音识别的训练，它通过训练把语音的发音特征映射到音素（构成一个字的发音的基本单元：白 bai -->b音素 ai音素）。这样，我们的音频就可以通过这样训练得到的映射关系来进行对齐了。



## 安装教程

采用一般安装形式：

1. Install [Miniconda](https://docs.conda.io/en/latest/miniconda.html)/[Conda installation](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html)
2. Create new environment and install MFA: `conda create -n aligner -c conda-forge montreal-forced-aligner`
   1. You can enable the `conda-forge` channel by default by running `conda config --add channels conda-forge` in order to omit the `-c conda-forge` from these commands
3. Ensure you’re in the new environment created (`conda activate aligner`)
4. Ensure you are in the conda environment created above
5. Install PyTorch a. CPU: `conda install pytorch torchvision torchaudio cpuonly -c pytorch` b. GPU: `conda install pytorch torchvision torchaudio pytorch-cuda=11.7 -c pytorch -c nvidia`
6. Install Speechbrain via pip: `pip install speechbrain`

其他安装方式见：https://montreal-forced-aligner.readthedocs.io/en/latest/installation.html



## 使用教程

1. 下载声学模型https://mfa-models.readthedocs.io/en/latest/acoustic/index.html
2. 下载字典https://mfa-models.readthedocs.io/en/latest/dictionary/index.html

ps: 上述步骤适用于英文，目前中文拼音在官网上是找不到的，可以到GitHub中下载中文拼音声学模型以及词典文件

3. 检查自己的音频和文本的可行性，以及它们是否适合acoustic model和dictionary，以中文拼音为例子`mfa validate (你的音频和文本所在的文件夹) mandarin_pinyin mandarin`
3. 开始对齐操作，`mfa align (你的音频和文本所在的文件夹) mandarin_pinyin mandarin (结果存放文件夹)`
3. 使用praat查看是否对齐

ps：praat下载、安装、使用教程https://zhuanlan.zhihu.com/p/33449448

## python-textgrid库使用教程
对齐后，将获得`.TextGrid`文件，对该文件的操作可看https://blog.csdn.net/duxin_csdn/article/details/88966295

## 参考文献

https://zhuanlan.zhihu.com/p/613596010

https://zhuanlan.zhihu.com/p/540015525

https://www.zhihu.com/question/449645689

https://blog.csdn.net/c2a2o2/article/details/128449004

https://zhuanlan.zhihu.com/p/33449448
