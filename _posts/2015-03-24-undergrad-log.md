`---

layout: post

title:  "毕业设计 Log"

date:   2015-03-24

categories: jekyll update

---

1. bootstrap里面有的直接写了js，干涉dispatch的内容
2. stanford: 

`java.lang.ClassNotFoundException: edu.stanford.nlp.trees.TreebankLanguagePack`

直接在Object里的main中启动，`edu.stanford.nlp.trees.TreebankLanguagePack`可以找到，但是如果放在jsp中直接启动，便显示找不到。

<b>Solution</b>
servlet或者别的class import的jar，必须放在WEB-INF/lib下

3. Stanford parser:

Collection 直接跳走：

	Tree parse = lp.parse(query);
	GrammaticalStructure gs = gsf.newGrammaticalStructure(parse);
	//Collection<TypedDependency> tdl = gs.typedDependenciesCCprocessed();
	Collection<TypedDependency> tdl = null;// = gs.typedDependenciesCollapsedTree();
	Iterator<TypedDependency> iterator = tdl.iterator();
		
	while(iterator.hasNext()) {
		TypedDependency dependency = (TypedDependency) iterator.next();
		System.out.println(dependency);
	}
	
转投Intelli IDEA解决

4. split(".")

.是正则表达式的公式，所以这里是错误的

<b>Solution</b>
	
`split("\\.")`

类似的还有"()" `split("[\\(||\\)]")`