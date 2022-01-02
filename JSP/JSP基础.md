## JSP基础
### 1.JSP是什么

```
1.	JSP,即Java Server Pages,Java服务器页面，即运行在服务器的页面。
2.	JSP文件的本质是Servlet.两者的不同之处在于，JSP是专门用于进行数据展示的Servlet,有其特殊的写法。而Servlet是用于完成业务逻辑处理的。两者都是运行在单例多线程环境下的。
```

### 2.JSP规范

```
1.JSP文件翻译成Servlet的过程：
	.jsp文件---(jsp翻译引擎)--->.java文件---(编译)--->.class文件
	
2.JSP规范：如何将jsp页面翻译为Servelt.
	eg:jsp页面中的HTML、CSS、JavaScript,及普通文本，均被翻译到out.write()中
```

### 3.JSP注释

```
1.格式：<%--  文本  --%>
	细节：HTML注释会被jsp翻译到Servlet的out.write()方法中，而jsp注释会被忽略掉。
```

### 4.JSP的Java代码块

```
1.JSP的Java代码块：<%  Java语句  %>	// 整个页面的java代码块会被翻译成Java语句置入Servlet的_jspService()方法中
	eg：<% System.out.println("Hello World!"); %>

2.注意：
	(1).声明的变量是不能添加权限访问控制符的；	//	_jspService()方法中不能设置权限访问控制符的变量
	(2).不能定义方法；		//	Java中一个方法里不能再定义方法
	(3).不能定义静态语句块。	// 静态语句块不能设置在Servlet的方法中，只能设置在类里
```

### 5.JSP的声明语句块

```
1.声明你将要在JSP程序中用到的变量和方法
JSP的声明语句块:<%!    %>	//	内容会被翻译到Servlet的类体里，没有包含到哪个方法体中
eg:
	<%!	// 可以添加权限访问控制符
		private int amount = 3;
		// 可以定义方法
		public void showData(double data){
			System.out.println("data = " + data);
		}
		// 可以定义静态语句块
		static {
			System.out.println("=========");
		}
	%>
```

### 6.JSP的表达式

```
1.表示的是一个在脚本语言中被定义的表达式。
JSP的表达式块:<%=  %>,其可在JSP页面输出变量，常量，及它们组成的各种表达式的值。
eg:
	<%=amount =>		// 	该表达式将被JSP引擎翻译到Servlet的_jspService()方法的out.write()方法中输出
注意，是表达式，而不是语句，是没有分号的。
```
