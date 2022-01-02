## JSP核心

### 1.内置对象

```
1.request :用户端请求，此请求会包含来自Get/Post请求的参数
2.response :网页传回用户端的回应
3.pageContext :网页的属性是在这里管理
4.session :与请求有关的会话期
5.application :Servlet正在执行的内容
6.out :用来传送回应的输出
7.config :Servlet的构架部件
8.page :JSP网页
9.exception :针对错误网页，未捕捉的例外
```

```
seession对象：在多个请求之间持续有效的会话对象，该对象允许用户存储和提取会话状态信息
API:
	getAttribute(String name): Returns the object bound with the specified name in this session, or null if no object is bound under the name.
	setAttribute(String name, Object value):
	Binds an object to this session, using the name specified.
```



### 2.JSP指令

```
1.作用：为当前的页面做一些基本的属性设置，为当前的页面的运行提供基本的环境。有三类指令：
	(1).page指令：页面指令，指定了页面的内容类型
	(2).include指令：包含指令；
	(3).taglib指令：标签库指令，声明该页面所使用的自定义标签
格式：
	<%@ 指令名称  属性名=属性值	属性名=属性值 ...  %>

```

### 3.page指令

```
1.用于设置当前页面的相关信息。一个JSP文件可以包含多个page指令，以下为常见的page指令的属性
eg:
	<%@ page contentType="text/html;charset=UTF-8" language="java" %>
	
(1).pageEncoding属性：用于当前页面所使用的字符编码格式，功能与contentType属性类似。
eg:
	<%@ page pageEncoding="utf-8" language="java" %>

(2).import= "Package.class"属性:用于完成在JSP页面导入指定的类。
eg:
	<%@ page import="java.util.Date" %>
	
(3).errorPage属性：当当前页面发生错误的时候会跳转到你指定的页面。
eg:
	<%@ page errorPage="/error.jsp" %>
	
(4).isErrorPage属性：指定页面设置属性值为“true",表示当前页面为一个“错误处理页面”。发生错误时，异常信息是封装在异常对象exception中的。可以通过调用对象方法，显示错误信息。
eg：
	<%@ page isErrorPage="true" %>
	
	错误信息：<%=exception.getMessage() %>

(5).isThreadSafe= "true|false" :
	值为（true）时，将进行普通的Servlet处理，多个请求将被一个Servlet实例并行处理。
	值为（flase）时，Servlet将实现单线程模式，不管什么请求，都将提供不同的分离的Servlet实例
	
(6).session= "true|false" :
	值为（true）时，预定义变量session（继承HttpSession)应该绑定到一个已存在的session，否则就创建一个session对象并将之绑定。
	值为（flase）时，将不使用session对象，如果试图使用，会报错。
	
(7).extends= "package.class" :
	将为Servlet创建一个超类，请慎用，也许服务器已经定义一个了。
	
(8).info = "message":
	定义一个可以通过调用getServletInfo方法得到的串。
```

### 4.include指令

```
1.用于将指定的文件包含到当前的JSP文件中，改文件只有一个属性file，用于指定要包含的文件。两者交互方式为静态联编。
eg:
	<%@ include file="/next.jsp" %>
用法：
	被include指定包含的文件，可以是JSP动态页面文件，也可以是HTML静态页面文件。
```

### 5.taglib指令

```
1.标签库指令，声明该页面所使用的自定义标签
eg:		// 声明了一个JSTL标记库；uri属性包含了一个标识库的惟一的字符串
	<%@ taglib prefix="c" uri="http://java.sun.com/jstl/core" %>
		// prefix属性定义的则是用于该页面的库名的前缀
```



