---

layout: post

title:  "毕业设计 Logging"

date:   2015-03-02

categories: jekyll update

---

### tools:

对于origin image和VOC files的文件（.dot .desc .actions .xml）文件的相互转换

而且raw data中的数据，dotfile可以直接反应VDR（可以转换成.conll）


### parser:

现在只是知道emnlp2013文件夹中可以用于训练和测试，但不知道输入到底什么，输出到底是什么。

### Next Step - 3.5

现在已经知道rawData里面dotfiles是VDRs，他们直接可以转换成一个parsing tree。
现在Image Parsing和Description Parsing的原料已经有了。

Next Step:
	
	1. 用stanford nlp构建Description Parsing
	2. 规范化Image Parsing的数据，用stanford nlp尝试进行parsing