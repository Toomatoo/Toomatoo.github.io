---

layout: post

title: "学习Java Servlet&JSP Nuts and Bolts"

data: 2015-03-20

categories: jekyll update

---

## 3.1&3.2 JSP Beans

Bean是一个单独的类（并不是Servlet）。它主要用于存储数据等活动。
我们可以使用`<jsp:useBean>` tag来调用一个bean或者创建一个新的bean。
	
其中有一些这个tag的attributtion：

	id="ID": 是这个bean专属的名字，用于检索到这个bean
	class="package.Class": 这bean定义的类
	scope="session|request|page|application": 表示这个bean的使用范围，定义尚未弄明白。
		session: 和cookie相关，在10分钟内打开仍然可以访问
		page: 只能在当前页面中使用
		request: 只能在当前request下使用，如果发送了request之后，这个bean就失效了。forward可以，redirect不可以。
		application: along with application existing
	
## 3.3 Setting Bean Properties using parameters

之前我们使用`jsp:setProperty` tag，我们可以使用attributes: `name`, `property`, `value`来单独设置某一个bean的某个property的值。

现在我们想要更加灵活地设置这些properties，比如我们想取出URL中parameter的值，作为某一个bean的内容，我们该怎么做呢。

同样使用`jsp:setProperty`,不过我们不使用value，而是使用parameter这个attribute：

	<jsp:setProperty name="user" property="email" param="email"></jsp:setProperty>
	
这样我们就可以取出URL变量email的值了。比如这个url：`localhost/index?email=111@qq.com`

更进一步，我们可以让bean的所有property自动匹配url中parameters：

	<jsp:setProperty name="user" property="*"></jsp:setProperty>
