---

layout: post

title:  "毕业设计"

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
		1.1 stanford parser是dependency的，研究一下标签的设置和API先运行起来
		1.2 研究一下parser结果的数据结构，以供后面的使用
	2. 规范化Image Parsing的数据，用stanford nlp尝试进行parsing
		2.1 写一个脚本，能将所有的.dot文件转换为.conll文件
		2.2 写一个小系统，转换.conll的表示为一个parsing tree
		
### Next Step - 3.9

和张老师讨论以后，我们将我的毕设定位成检索系统的开发 - “基于依存分析的图片检索系统”。

#### 本周
1. 写好简单的Decription parsing的接口：

		String -> Tree
	
2. 写好解析Image Parsing的接口：

		.dot -> Tree

3. 查看Query Parsing的部分:

		TreeX/ML相似度
		图相似度
		
#### 完成
		
1. Image / Description Parsing都完成了转换成conll或者直观的依存关系的文件。

		Image Parsing: data/conll/
		Decription Parsing: data/desc-parsed/ (sentences in data/description/)
2. Query Parsing目前仍然使用Stanford nlp的parser。

		我用stanford parser直接试着解析了我自己输入的一些query，发现：
		1. 如果有介词的，会被直接转换成一层关系表现在边上，这个词本身就去掉了


### Next Step - 3.14

1. 查看把Parsing Tree转换成什么数据结构比较好
	
		Image Parsing的关系直接是位置关系；
		Description/Query Parsing的关系是Dependency parsing的tag；
		
	查看一些资料和源代码，学习一下到底表示成什么数据结构比较好。

2. 相似度计算

		现在初步的想法是，由物体（Object）做初步索引，由关系（Dependency）做相似度计算的主体。
		1. 先做直接匹配看看效果
		2. 然后需要整合几个关系的综合考虑
		
3. 工程界面的搭建


### Project - 3.24

#### 工程流程

	index.jsp 输入 query
	index.jsp转入result.jsp页面

现在需要返回ArrayList<String>的一组图片地址，用于result的显示。

##### Similarity No.1

	1. 物体直接匹配：找到候选集
	2. 直接按关系对进行匹配
	
##### Similarity No.2

	1. 找出所有的关系对（N-R-N）
	2. 查找相同的内容
	

### Next Step - 4.12

1. 生成Dependency Parsing Tree
	
	query和image都只有一棵树，description可能是多棵树。
	
2. 运用子树覆盖来找到两个物体的所有关系

	考虑
	1. query和image依存树的比较
	2. query和description每个子树的比较

3. 推理过程

	1. 寻找子树：覆盖所有object
	2. 推导子树中这一对object的所有关系：第一个共同父节点左右路线上的关系都是他们的关系
	3. 面对每一个关系应该有不同的评分（因为上面的“所有关系”可能很多）