---

layout: post

title: "学习Java Servlet&JSP Nuts and Bolts"

data: 2015-03-20

categories: jekyll update

---

## 2.1 Import java code into JSPs

目标：将Java Object嵌入到JSPs中去

其实创建一个JSP他的工作路径是这样的：`JSP -> Servlet -> Html Page`

我们可以在一个JSP中嵌入任何Java code。

比如我们如果想要import一个类供后面的Java code使用，那么：

	<%@ page import="java.util.Data, anouther pacage"%>
		
	<%= new Data() %>

## 2.2 Getting URL parameters

这里的课程为后面做准备。
当我们在form中提交信息的时候，我们的信息通常会表现在url中，比如`localhost:8080/yes?user=jack&id=101`

这样，我们需要获取后面的parameter为进一步的操作做准备。

在这节课程中，我知道了，在一个Servlet中，我们可以在`doGet`函数中，通过`request.getParameter`函数可以获取某个parameter的String。

而在JSP中，我们想想前面`JSP -> Servlet -> Html Page`的路径，所以在JSP中有一个默认的request/response。所以我们可以直接使用`request.getParameter`

## 2.3 Scripting HTML

这节的课程是真正学习如果使用JSP和Java，实现Scripting HTML。简单来说，就是在JSP中配合Java，来获取一个丰富的HTML page。

一个简单的例子就是，在一个JSP的body中：

	<% for(int i=0; i<5; i++) { %>
	This is a JSP loop.
	<% } %>
		
这时候，我们会发现打印了5遍这句话，说明这里的java code影响了整个html page的显示。别的Java语句都是适用的。

## 2.4 Including other files

这节的课程目的是将一些文件直接作用于JSP，比如直接显示一个txt文件的内容。

静态include：知道文件不会变，而且必然会被这个jsp include，那么就是静态include，使用方法：

	<%@ include file="somefile.txt" %>


动态include：文件内容会发生变化，或者被include是条件的，那么就使用动态include，使用方法：

	<jsp:include page="somepage.html"/>
		
这里说的有条件，就是比如嵌入java code，`if...else...`·那么就需要使用`jsp:inclde` tag.

## 2.5 Forwarding and Redirecting

### Forward
进入一个JSP以后，如果我们想显示另外一个JSP，也就是Forward，那么我们可以：

	<jsp:forward page="some.jsp"> </jsp:forward>
	
这样做完以后，我们的url还是显示最初的url访问。

另一种方法是：

	<% 
	request.getRequestDispatcher("some.jsp").forward(request, response);
	%>

### Redirect

我们还可以重定向：

	<% 
	response.sendRedirect("some.jsp")
	%>
	

两者的区别是，Forward是重写内容，发现url未变，Redirect是直接指向另一个页面，url变成了重定向的页面的url。

<b>并且Redirect的request已经被重置了，如果需要Parameter，需要自己加入</b>。

## 2.6 Declaration Tag

`jsp:scriptlet` (`<% %>`)中定义的变量只能是final，也就是只读变量。如果想要自由地定义java变量，那么需要Declaration Tag：

	<%!
	private String name = "Jack";
	%>

	<%= name %>

=========
`Small Cake`

1. 使用Tomcat 8以后显示 `The superclass "javax.servlet.http.HttpServlet" was not found on the Java Build`。之后我手动修改properties中targeted runtime，解决了问题。

## 2.7 Architecture Models

除了正常的使用JSP相互link跳转以外。现在主要的一种Model是使用MVC。

比如简单的页面跳转，我们在JSP中可以写主要的页面显示的内容。而跳转时，可以构建Contorller Servlet，动态地确定跳转的目的地。

##2.8 Jar Files

一个工程需要的jar可以直接放在`/WebContent/WEB-INF/lib`中。