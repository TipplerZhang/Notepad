## EL表达式

### 1.从四大域依次查找数据

```
EL:Expression Language,表达式语言，是一种在JSP页面中获取数据的简单方式。
基本语法形式：
	在JSP页面的任何静态部分均可通过${expression}的形式获取到指定表达式的值。
```

```
1.从四大域依次查找数据
	*.EL只能从四大域属性空间中获取数据；(四大域属性空间：pageContext、session、request、application)
	*.其查找数据的循序是，依次按照由小到大的范围从四大域中查找指定名称的属性值。
error eg:
	<%
		int sum = 50;
	%>
	<!-- 这个数据sum是取不出来的，因为其没有在四大域属性空间中 -->
	sum = ${sum }<br>
true eg:
	<%	// 下列四个任一个都可以
		// pageContext.setAttribute("address","China");
		// request.setAttribute("address","Canada");
		// session.setAttribute("address","Japan");
		application.setAttribute("address","USA");
	%>
	address = ${address} <br>	// 输出USA
```

###  2.从指定域中获取数据

```
2.从指定域中获取数据
	从pageContext依次查找到application域空间，会降低执行效率，若某属性确定存放在某个域属性空间，则可指定直接从该空间中查找。此时需要借助EL的四个域属性空间相关的内置对象。
eg:
	<%	
		pageContext.setAttribute("address","China");
		request.setAttribute("address","Canada");
		session.setAttribute("address","Japan");
		application.setAttribute("address","USA");
	%>
	address = ${pageScope.address} <br>		// 输出China
	address = ${requestScope.address} <br>	// 输出Canada
	address = ${sessionScope.address} <br>	// 输出Japan
	address = ${applicationScope.address} <br>	// 输出USA
```

|     内置对象     |                    说明                    |
| :--------------: | :----------------------------------------: |
|    pageScope     |    从page范围域属性空间中查找指定的key     |
|   requestScope   |   从request范围域属性空间中查找指定的key   |
|   sessionScope   |   从session范围域属性空间中查找指定的key   |
| applicationScope | 从application范围域属性空间中查找指定的key |

