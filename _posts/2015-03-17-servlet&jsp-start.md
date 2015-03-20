---

layout: post

title: "学习Java Servlet"

data: 2015-03-17

categories: jekyll update

---

## 1.2 配置

Eclipse Workbench中建立一个Tomcat server。

1. 下载Tomcat包
2. Eclipse建立server关联Tomcat


## 1.3 Servlet

这个部分主要讲解如何使用上面建立的Server创建一个servlet。

1. 首先我们需要创建一个Eclipse Project `Dynamic Web Project` (需要查看这个含义)
2. 然后我们看到这个Project的Content：

		Java Resources: java classes用于连接相应的页面。
		WebContent: web实际的内容，比如html，xml，css等等
3. 在Java Resources中创建一个Servlet

		创建的时候我们可以看到，一个servlet可以预设一些method，默认有get和post，还有init和destroy等等。

4. 这样我就可以在doGet函数中进行一个操作，当用户对这个servlet进行一次GET的时候，便会执行这个函数。


## 1.4 JSP - Java Server Pages

这个部分主要简单讲解JSP。
JSP的实质是一个HTML page，但是它比较特殊，因为它可以内嵌Java语句，从而实现更加灵活的内容。

1. 在Webcontent中我们可以直接创建一个html file，也可以直接创建一个JSP
2. 直接运行html或者JSP，可以看到这个页面的效果
3. JSP的正确打开方式：这里我学习了两种标签

		<%=
		Put a String here, and it will appear on the page directly.
		%>
		
		<%
		Put some java code here, and it will exist behind the page, and you can use some data in the above tag.		
		%>


## 1.5 Web.xml

Web.xml是控制Servlet URL的文件，编程者可以根据Web.xml的设置，个性化设置各个页面的url。

这个文件的内容是这样的：

	<?xml version="1.0" encoding="UTF-8"?>
	<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" id="WebApp_ID" version="2.5">
	  <display-name>TestWebXML</display-name>
	  
	  <welcome-file-list>
	    <welcome-file>index.html</welcome-file>
	    <welcome-file>index.htm</welcome-file>
	    <welcome-file>index.jsp</welcome-file>
	    <welcome-file>default.html</welcome-file>
	    <welcome-file>default.htm</welcome-file>
	    <welcome-file>default.jsp</welcome-file>
	  </welcome-file-list>
	  
	  <servlet>
	    <description></description>
	    <display-name>Hello</display-name>
	    <servlet-name>Hello</servlet-name>
	    <servlet-class>demo.hello.Hello</servlet-class>
	  </servlet>
	  <servlet-mapping>
	    <servlet-name>Hello</servlet-name>
	    <url-pattern>/Hello</url-pattern>
	  </servlet-mapping>
	</web-app>

可以看到welcome-file-list是关于index的。

servlet tag是关于一个servlet的的url设置。
`servlet-name`是这个servlet的class name
`servlet-class`是这个class的地址

servlet-mapping tag是关于实际的url mapping。
`url-pattern`是url的一个正则表达式。

如果我们写了一个JSP，想要构建新的url给这个page的话，我们该怎么修改Web.xml呢？

类似地，我们构建一组tag：

	  <servlet>
	    <description></description>
	    <display-name>Hello</display-name>
	    <servlet-name>Hello</servlet-name>
	    <jsp-file>/some.jsp</jsp-file>
	  </servlet>
	  <servlet-mapping>
	    <servlet-name>Hello</servlet-name>
	    <url-pattern>/Hello</url-pattern>
	  </servlet-mapping>

## 1.6 Deployment

本节，我学习如果将一个Dynamic Web Project部署在网络上。