---

layout: post

title: "学习Java Servlet&JSP Nuts and Bolts"

data: 2015-03-20

categories: jekyll update

---

## Import java code into JSPs

目标：将Java Object嵌入到JSPs中去

其实创建一个JSP他的工作路径是这样的：`JSP -> Servlet -> Html Page`

我们可以在一个JSP中嵌入任何Java code。

比如我们如果想要import一个类供后面的Java code使用，那么：

		<%@ page import="java.util.Data, anouther pacage"%>
		
		<%= new Data() %>

## Getting URL parameters

这里的课程为后面做准备。
当我们在form中提交信息的时候，我们的信息通常会表现在url中，比如`localhost:8080/yes?user=jack&id=101`

这样，我们需要获取后面的parameter为进一步的操作做准备。

在这节课程中，我知道了，在一个Servlet中，我们可以在`doGet`函数中，通过`request.getParameter`函数可以获取某个parameter的String。

而在JSP中，我们想想前面`JSP -> Servlet -> Html Page`的路径，所以在JSP中有一个默认的request/response。所以我们可以直接使用`request.getParameter`
