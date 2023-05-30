# nanoGPT-implementation
## Introduction
This is a repo for learning to build a nanoGPT from Andrej Karpathy:[nanoGPT](https://github.com/karpathy/nanoGPT), 

video tutorial:[Let's build GPT: from scratch, in code, spelled out.](https://www.youtube.com/watch?v=kCc8FmEb1nY)
## 运行环境
torch                          2.0.0

torchaudio                     2.0.1

torchvision                    0.15.1

在终端中运行以下命令安装其他依赖：
```
$ pip install -r requirements.txt
```
## Code
`gpt_dev.ipynb` -> 视频中用到notebook，加了自己的注释

`train.py` -> 训练脚本

`model.py` -> 模型构建脚本

## train
若无足够的时间和资源，仅仅体验一下模型训练过程，可参考此过程训练一个small model

下载莎士比亚数据集
```
$ python data/shakespeare_char/prepare.py
```
开始训练
```
$ python train.py config/train_shakespeare_char.py
```
## sampling / inference

运行以下命令即可生成莎士比亚风格的文本：
```
$ python sample.py --out_dir=out-shakespeare-char
```
我们就得到了一个character-level的模型
## finetuning

通过在这个数据集上对预先训练好的 GPT-2模型进行微调 ，很有可能获得更好的结果。
在另一个路径下，仍然下载莎士比亚数据集
```
$ python data/shakespeare/prepare.py
```
基于gpt2-xl 模型进行微调
```
$ python train.py config/finetune_shakespeare.py
```
生成莎士比亚风格的文本
$ python sample.py --out_dir=out-shakespeare
可以控制参数，生成不同的文本

参数：--init_from: 初始化模型，可选参数：'gpt2', 'gpt2-medium', 'gpt2-large', 'gpt2-xl'，默认为 'gpt2-xl'\n --start:以什么文本为开头\n 
$ python sample.py \
    --init_from=gpt2-xl \
    --start="What is the answer to life, the universe, and everything?" \
    --num_samples=5 --max_new_tokens=100
    
如果资源和时间重组可以使用来自 OpenAI 的 WebText 数据集（12.9G）来训练，步骤与上面类似。
