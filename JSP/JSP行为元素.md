## JSP行为元素

```
JSP行为元素把动态数据插入到模板文本中的适当位置，表示的是发生在运行时的动态行为.
```

### 1.JSP标准行为

```
原因：
	由于在JSP页面大量使用Java代码块，表达式块等内容，会使JSP页面看起来“杂乱无章”，为了是页面尽可能简洁明了，会尽量少使用Java代码块与表达式块，取而代之的是使用EL表达式，JSTL标签，及JSP标准行为。
	
1.JSP标准行为：使用系统定义好的标签来完成本应由Java来完成的动作。
语法格式：
	<jsp:行为名称 属性名=属性值 属性名=属性值 .... ></jsp:行为名称>
或： <<jsp:行为名称 属性名=属性值 属性名=属性值 .... />

	JSP标准行为很多，但常用的就两个：转发动作(forward)和包含动作(include).这两个行为的完成使用的是底层RequestDispatcher的forward()与include()方法实现。两者都具有一个page属性，属于指定要转向的页面。
	这两种请求转发方式的本质区别为：标准输出流的开启时间不同。
		*.forward()的标准输出流是在目标资源中开启的标准输出流。
		*.include()的标准输出流是在当前发出包含运作的页面中开启的。
```

```
1.<jsp:forward> 行为：页面一旦有了forward行为，那么当前页面中的所有要显示的内容都将无法显示，因为页面直接转发到了下一个页面。
eg:
	<jsp:forward page="/next.jsp"></jsp:forward>
或  <<jsp:forward page="/next.jsp"/>
```

![](E:\MarkDown文件\JSP\forward()请求动作.png)

```
2.<jsp:include> 行为：用于完成将指定页面包含到当前页面的功能。两者交互方式为动态联编。
eg:
	<jsp:include page="/next.jsp"></jsp:include>
或  <<jsp:include page="/next.jsp"/>
```

![](E:\MarkDown文件\JSP\include()动作.png)

```
静态联编与动态联编的应用场景
	1.两者均可使用时，一般使用静态联编。因为在程序运行时只存在一个Servlet,对资源的消耗较少，且不存在调用问题，效率高。
	2.若两个文件间需要共享同一变量，此时只能使用静态联编。
	3.若在两个文件间存在同名变量，且不能混淆，此时只能使用动态联编。
```

```
3.<jsp:usebean> 行为：创建了由class属性指定的bean类的一个实例，并将其与id属性指定的名称关联起来。
eg:
	<jsp:usebean id="cartoon" class="com.ora.jsp.beans.mota.CartoonBean" />
	express: <jsp:getProperty name="cartoon" property="fileName" />
属性：
id="beanName": 定义生成bean组件的名字。
scope="page|request|session|application": 定义bean的活动范围
	page：bean的缺省使用范围
	request: 作用于任何相同请求的JSP文件
	session：作用于整个session的生存周期内
	application：作用于整个application的生存周期内
```

```
4.<jsp:setProperty>：设置已经实例化的bean对象的属性值
eg:		// 	等价于<% student.age=18; %>
	<jsp:setProperty name="student" property="age" value="18" />
属性：
	name: 表示要设置属性的是哪个bean。
	property: 表示要设置哪个属性。
	value: 用来指定bean属性的值(可选)
	param: 指定用那个请求参数作为Bean属性的值
```

```
5.	<jsp:getProperty>：从一个JavaBeans组件中获得某个属性值，并将其添加到应答中。
eg:
	<jsp:getProperty name="student" property="name" /> ====<%=student.name %>
属性：
	name: 表示要获取属性的是哪个bean。
	property: 表示要提取哪个属性的值。
```



```
其他行为：

	<jsp:param>：使用<jsp:forward>或<jsp:include>将请求转发给另一个Servlet或JSP页面时，向这个请求中加入一个参数值。
eg:
	<jsp:param name="name" value="<%=usename%>"/>
	
	<jsp:plugin>：生成包含了独立于适当浏览器的元素(OBJECT或EMBED)的HTML.当使用Java插件软件来执行一个applet时，这些元素是必需的。
```

### 2.自定义行为

```

```

### 3.JSP标准标签库

```
1.JSP标准标签库（JSP Standard Tag Library）是Java EE网络应用程序开发平台的组成部分。它在JSP规范的基础上，扩充了一个JSP的标签库来完成一些通用任务，比如XML数据处理、条件执行、数据库访问、循环和国际化。

2.下面是全部六个JSTL标签库的描述：
核心库:	如<c:if>和<c:when>。
格式化库:	具有国际化功能。
数据库标签库 :包括查询、创建和更新数据库表的标签。
XML库 :	XML数据的处理，比如转换和访问单个元素。
函数库 
TLV :	允许JSP页面的XML视图在翻译时验证。JSTL提供的TLV允许标签库作者根据JSP页面中脚本元素的使用和被允许的标签库来执行限制条件。

```

```
eg:
	// 声明了一个JSTL标记库；uri属性包含了一个标识库的惟一的字符串
	<%@ taglib prefix="c" uri="http://java.sun.com/jstl/core" %>
			// prefix属性定义的则是用于该页面的库名的前缀
		...
   <c:out value="${1 + 2 + 3}" />	//JSTL核心库的行为
   
语法格式：//	有行为体
	<prefix:action_name attr1="value1" attr2="value2">
		action_body
	</prefix:action_name>
	
	//	无行为体
	<prefix:action_name attr1="value1" attr2="value2" />
```

```
3.备注：
	(1).行为元素，通常也成为标记，都被集中到JSTL库，开始与结束由两部分组成：库的前缀和库中行为的名称，中间由冒号分隔。
	(2).前缀有两种用途：一是使得不同库中的行为可以具有同样的名称；二是使得容器可以得知某个特定行为属于哪个库。
```

