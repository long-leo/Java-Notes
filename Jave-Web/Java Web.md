# Java Web

## 一. Java Web简介

### 1.1 胖客户端与瘦客户端

- 胖客户端

  ```bash
  指一个程序运行时需要一个单独的客户端程序支持, 例如登录QQ需要一个客户端程序.
  
  ## "远古时代"的Applet技术就是运行在客户端的程序, 在客户端完成动态代码的开发很复杂, 现在使用的可在客户端实现动态效果的JavaScript也是只完成一些简单的表单验证功能实现
  
  ```

- 瘦客户端

  ```
  不需要任何其他程序的安装, 直接使用即可,比如网上论坛, 只需要一个浏览器即可使用
  ```

### 1.2 动态Web与静态Web

#### 1.2.1 两者本质区别

```
静态Web无法进行数据库操作, 动态Web可以进行数据库操作
```

#### 1.2.2 动态Web流程图

![image-20210228184819663](Java Web.assets/image-20210228184819663.png)
```
Web容器会采用拼凑代码(主要时HTML)的形式动态生成数据并通过Web服务器发挥给客户端浏览器
```

#### 1.2.3 实现动态Web

- CGI (Common Gateway interface, 公共网关接口)
  ```
  多进程机制处理, 效率低
  ```

- PHP (Hypertext Preprocessor, 超文本预处理)

  ```
  服务器端嵌入式脚本语言, 只能运行在Apache服务器下, 且在使用MySQL数据库时才可以达到性能的最大发挥
  
  # 适合个人或小型项目开发
  ```

- ASP (Active Server Pages, 动态服务页)

  ```
  只能运行在IIS(Internet Information Services)服务器上, 在SQL Server数据库上才可以得到最大的发挥
  
  # 不适合Java开发
  ```

- ASP.NET

  ```
  基于.NET框架, 可选择自己喜欢的语言开发, 微软产品, 受限于平台, 往往用于中型项目的开发
  ```

- JSP (Java Server Page, Jave服务页)

  ```
  不受操作系统或平台制约
  服务器支持: Tomcat, WebLogic, JBoss, Websphere
  ```

### 1.3 企业开发架构

```
程序运行在中间件上, 并且通过中间件进行数据库的操作, 而具体一些的相关处理, 如事物/安全完全由中间件负责
```



![image-20210228190910138](Java Web.assets/image-20210228190910138.png)

### 1.4 Java EE架构

> Java EE架构只是工作在中间层的一种组件

![image-20210228191659625](Java Web.assets/image-20210228191659625.png)

#### 1.4.1 Java EE容器

> 各容器负责处理各自的程序, 互相之间没有任何影响, 而如果需要运行Web程序, 一定要有Web容器的支持

- Applet Container
- Application Client Container
- Web Container
- EJB Container

#### 1.4.2 Jave EE 组件

- EJB组件本身提供一个业务中心, 属于分布式开发的范畴

#### 1.4.3 Jave EE服务(了解即可, 需要用时再研究)

> 现阶段需要知道: JNDI, JAXP, JSTL等

<img src="Java Web.assets/image-20210228192336003.png" alt="image-20210228192336003" style="zoom: 25%;" />

### 1.5 Java EE核心设计模式

- MVC (Mode-View-Controller)设计模式

  ```
  用户一旦发出请求之后会将所有请求交给控制层处理, 由控制层调用模型层中的模型组件, 并通过这些组件进行持久层的访问, 再将所有结果都保存在JavaBean(Java类)中, 最终由JSP和JavaBean一起完成页面的显示.
  
  # EJB技术不一定会使用
  ```

  

![image-20210228194553894](Java Web.assets/image-20210228194553894.png)

### 1.6 Struts框架

> Struts框架主要作用在Web层上, 使用框架前, 应该熟练使用标准MVC进行项目的开发

![image-20210228195247963](Java Web.assets/image-20210228195247963.png)

## 二. HTML

### 2.1 URL与HTTP

#### 2.1.1 URL

```
URL(Uniform Resource Locator, 统一资源定位符)
```

#### 2.1.2 HTTP

```
HTTP协议(Hypertext Transfer Protocol, 超文本传输协议), 客户端请求与回应的标准协议, 输入地址与端口号即可获取服务器上的网页信息
```

### 2.2 编写HTML

#### 2.2.1 表格与文本显示效果

```
元素属性的属性值需要用""括起来
```

```html
<html>
    <head>
        <title>ll</title>
    </head>
    <body>
        <center>
        	<table border="1" width="80%">
                <tr>
                	<td colspan="6">
                    	<font size="15">字体显示</font>
                    </td>
                    <td rowspan="2">
                    	<img src="./Java Web.assets/自然码双拼.png"/>
                    </td>
                </tr>
                <tr>
                	<td><b>粗体</b></td>
                    <td><i>斜体</i></td>
                    <td><u>下划线</u></td>
                    <td><s>中划线</s></td>
                    <td>90<sup>o</sup></td>
                    <td>H<sub>2</sub>O</td>
                </tr>
            </table>
        </center>
    </body>
</html>
```

        <center>
        	<table border="1" width="80%">
                <tr>
                	<td colspan="6">
                    	<font size="15">字体显示</font>
                    </td>
                    <td rowspan="2">
                    	<img src="./Java Web.assets/自然码双拼.png"/>
                    </td>
                </tr>
                <tr>
                	<td><b>粗体</b></td>
                    <td><i>斜体</i></td>
                    <td><u>下划线</u></td>
                    <td><s>中划线</s></td>
                    <td>90<sup>o</sup></td>
                    <td>H<sub>2</sub>O</td>
                </tr>
            </table>
        </center>
#### 2.2.2 表单

```html
<html>
    <head>
        <title>ll</title>
    </head>
    <body>
        <form action="" method="post">
            <input type="text" name="userid" value="NO." size="2" maxlength="2"><br>
            <input type="text" name="username" value="请输入用户名"><br>
            <input type="password" name="userpass" value="请输入密码"><br>
            <input type="radio" name="sex" value="男" checked>男
            <input type="radio" name="sex" value="女">女<br>
            <select name="dept">
                <option value="技术部">技术部</option>
                <option value="销售部">销售部</option>
                <option value="财务部">财务部</option>
            </select><br>
            <input type="checkbox" name="inst" value="唱歌">唱歌
            <input type="checkbox" name="inst" value="游泳">游泳
            <input type="checkbox" name="inst" value="跳舞">跳舞
            <input type="checkbox" name="inst" value="编程" checked>编程
            <input type="checkbox" name="inst" value="上网">上网<br>
            <textarea name="note" cols="30" rows="3">请输入文本描述</textarea><br>
            <input type="submit" value="提交">
            <input type="reset" value="重置">
        </form>
    </body>
</html>
```

  <form action="" method="post">
            <input type="text" name="userid" value="NO." size="2" maxlength="2"><br>
            <input type="text" name="username" value="请输入用户名"><br>
            <input type="password" name="userpass" value="请输入密码"><br>
            <input type="radio" name="sex" value="男" checked>男
            <input type="radio" name="sex" value="女">女<br>
            <select name="dept">
                <option value="技术部">技术部</option>
                <option value="销售部">销售部</option>
                <option value="财务部">财务部</option>
            </select><br>
            <input type="checkbox" name="inst" value="唱歌">唱歌
            <input type="checkbox" name="inst" value="游泳">游泳
            <input type="checkbox" name="inst" value="跳舞">跳舞
            <input type="checkbox" name="inst" value="编程" checked>编程
            <input type="checkbox" name="inst" value="上网">上网<br>
            <textarea name="note" cols="30" rows="3">请输入文本描述</textarea><br>
            <input type="submit" value="提交">
            <input type="reset" value="重置">
        </form>

## 三. JavaScript 

> 基于对象(Object)和事件驱动(Event Driven)并具有安全性能的脚本语言, 嵌入在HTML语言中

### 3.1 

```html
<html>
   	<head>
        <title>ll</title>
        <script language="JavaScript">
            document.write("<h1>hello world</h1>");
    		alert("Hello World!!!");
    	</script>
    </head>
    <body>
        
    </body>
</html>
```

### 3.2 html导入*.js文件

1. hello.js

   ```js
   alert("Hello World");
   ```

2. hello.html

   ```html
   <html>
       <head>
           <title>ll</title>
           <script language="JavaScript" src="hello.js">
           </script>
       </head>
   </html>
   ```

### 3.3  顺序, 分支, 循环

> 语法与, Java一致, 字符串之间的比较不同, JavaScript字符串比较之间用"=="比较即可

### 3.4 函数

#### 3.4.1 如何定义

```js
function  functionName(param1, param2,...){
    [return returnValue];
}
```

1. 无需声明返回值

2. 参数类型不需要声明

### 3.5 数组

```js
function fun(){
    var arr = new array(3);
    var arr = new array("MLDN", "MLDNJAVA", "LiXingHua");
    var str = "字符串内容";
}
```

### 3.6 事件处理

#### 3.6.1 窗口事件(Window Event)

- onload : 文档载入时执行脚本 (body, frameset)

- onunload: 文档下载时执行脚本(body, frameset)

  ```html
  <html>
      <head>
          <title>ll</title>
          <script language="JavaScript">
          	function hello(){
                  alert("hello");
  			}
              function byebye(){
  				alert("byebye");
              }
          </script>
      </head>
       <body onload="hello()" onunload="byebye()">
              
          </body>
  </html>
  ```

#### 3.6.2 鼠标事件

- onclick

  ```html
  配合button
  <input type="button" value="显示" onClick="show()">
  ```

  ```html
  <html>
      <head>
          <title>ll</title>
          <script language="JavaScript">
          	function fun(){
                  alert("hello");
              }
          </script>
      </head>
      
      <body>
          <h3>
              <a href="#" onClick="fun()">press</a>
          </h3>
      </body>
  </html>
  ```

#### 3.6.3 onSubmit

> 1. 只能在<form>元素中使用
> 2. 需要使用return来接收函数的返回值, false不能提交, true可以提交
> 3. this在<form>元素上, 就是代表整个表达元素对象, 使用"this."可以访问表单内部元素, 其他元素同理
> 4. "document.formName." 可以访问表单的元素, 单选按钮, 复选框需采用数组操作, 如documetn.formName.sex[0]

1.  validate.js

   ```js
   function validate(f){
       var value = f.email.value;
       if (! /^\w+@\w+.\w+$/.test(value)){
           alert("EMAIL格式不正确!");
           f.email.focus();
           f.email.select();
           return false;
       }
       return true;
   }
   ```

2. validate.html

   ```html
   <html>
       <head>
           <title>ll</title>
           <script language="JavaScript" src="validate.js">
   
           </script>
       </head>
       <body>
           <form action="" method="post" onSubmit="return validate(this)">
               <input type="text" name="email">
               <input type="submit" value="提交">
           </form>
       </body>
   </html>
   ```

3. document.

   > 表单名为myform, sex为单选框名, inst为复选框名

   ```js
   function show(){
       var sex;
       if (document.myform.sex[0].checked){
           sex = document.myform.sex[0].value;
       } else{
           sex = document.myform.sex[2].value;
       }
       var inst = "";
       for (i = 0; i < document.myform.inst.length; i++){
   		if (document.myform.inst[i].checked){
   			inst += document.myform.inst[i].value + ", ";
           }
       }
   }
   ```

#### 3.6.4 onChange

- onChange

  ```html
  <!--配合下拉列表-->
  <select name="dept" onChange= "show(this.value)">
      
  </select>
  <input type="text" name="result" value="">
  ```

  show.js

  ```js
  function show(val){
      document.myform.result.value=val;
  }
  ```

### 3.7 使用正则表达式

```js
/正则表达式/.test(验证的内容)
```

### 3.8 window对象

#### 3.8.1 open()

> 新开一个窗口, 该窗口打开了指定的url

```js
function fun(thisurl){
    window.open(thisurl, "页面标题", "width=470, height=150, scrollbars=yes, resizable=no");
}
```

#### 3.8.2 confirm()

> 弹出一个确认框, 返回一个boolean值

```js
function fun(){
    if (window.confirm("确认删除?")){
        alert("已删除");
    }else{
        alert("未删除");
    }
}
```

#### 3.8.3 重定向 location

> 跳转到指定页面

```js
function fun(thisurl){
    window.location=thisurl;
}
```

#### 3.8.4 close()

> 关闭窗口

```js
function closeWin(){
    window.close();
}
```

#### 3.8.5 opener

```js
function closeWin(){
    window.close();
}
// window.opener就是访问父窗口
window.opener.location.reload();
// 获取窗口可以访问父窗口的元素
var doc = window.opener.document;
doc.parentform.result.value=city;
```

## 4. XML

![image-20210301121303598](Java Web.assets/image-20210301121303598.png)

### 4.1 XML的特性

#### 4.1.1 组成

- 前导区

  ```bash
  规定XML页面的一些属性
  version: XML版本
  encoding: 页面使用的编码
  standalone: 此XML文件是否独立运行, 如果需要进行显示可以使用CSS或XSL(与XPath结合使用)控制
  
  ## 这三个属性必须按照固定的顺序写: version, encoding, standalone
  ```

- 数据区

  ```
  1. 必须有一个根元素
  2. 一个根元素可以放多个子元素
  3. 每一个元素必须完结
  ```

#### 4.1.2 XML引入CSS

attrib.css

```css
name
{
    display:block;
    color:blue;
    font-size:20pt;
    font-weight:bold;}
id,company,email,tel,site
{
    display:block;
    color:black;
    font-size:14pt;
    font-weight:normal;
    font-style:italic;
}
```

xml_demo_03.xml

```xml
<?xml version="1.0" encoding="utf-8" standalone="no"?>
<?xml-stylesheet type="text/css" href="attrib.css"?>
<addresslist>
    <linkman>
        <name>李兴华</name>
        <id>001</id>
        <company>魔乐科技</company>
        <email>mldnqa@163.com</email>
        <tel>(010)51283346</tel>
        <site>www.MLDNJAVA.cn</site>
    </linkman>
</addresslist>
```

#### 4.1.3 元素还是属性

> 1. 如果需要显示或者为了解析方便, 那么使用元素会更好, 属性是无法显示的

#### 4.1.4  实体参照表

| 实体参照 | 对应字符 |
| -------- | -------- |
| \&amp;   | \&       |
| \&lt;    | <        |
| \&gt;    | >        |
| \&quot;  | "        |
| \&apos;  | '        |

#### 4.1.5 CDATA

- 格式语法

  ```
  <![CDATA[ 不解析的内容 ]]>
  ```

#### 4.1.6 DTD/Schema

```
现在的XML文件的内容都是任意的定义的, 如果要对一个XML文件中经常出现的元素或属性进行严格定义, 需要使用DTD和Schema技术
```



### 4.2 DOM解析

> DOM(Document Object Model, 文档对象模型)

#### 4.2.1特点

1. 随机访问

2. DOM树放在了内存中

   ```
   如果文档较大或结构比较复杂, 对内存的需求就比较高, 结构复杂树的遍历也是一项耗时的操作, 对机器的性能要求较高, 程序的效率并不十分理想.
   ```

#### 4.2.2 核心操作接口

- **Document**

  > 提供了对文档中数据进行访问和操作的入口

  1. 取得指定节点名称的NodeList

     ```java
     public NodeList getElementByTagName(String tagname);
     ```

  2. 创建一个指定名称的节点

     ```java
     public Element createElement(String tagName) throws DOMException;
     ```

  3. 创建一个文本内容节点

     ```java
     public Text createTextNode(String data)
     ```

  4. 创建一个属性

     ```java
     public Attr createAttribute(String name) throws DOMException;
     ```

- **Node**

  > 每一个Node接口代表了DOM树的一个节点

  ![image-20210301142109523](Java Web.assets/image-20210301142109523.png)

  1. 在当前节点下增加一个新节点

     ```java
     Node appendChild(Node newChild) throws DOMException;
     ```

  2. 取得本节点下的全部字节点

     ```java
     public NodeList getChildNodes();
     ```

  3. 取得本节点下的第一个子节点

     ```java
     public Node getFirstChild();
     ```

  4. 取得本节点下的最后一个字节点

     ```java
     public Node getLastChild();
     ```

  5. 判断本节点下是否还有其他节点

     ```java
     public boolean hasChildNodes();
     ```

  6. 判断是否还有其他属性

     ```java
     public boolean hasAtrributes();
     ```

  7. 取得节点内容

     ```java
     String getNodeValue() throws DOMException;
     ```

- **NodeList**

  > 表示一个节点的集合, 一般用于表示有顺序关系的一组节点

  1. 取得节点的个数

     ```java
     public int getLength();
     ```

  2. 根据索引取得节点对象

     ```java
     public Node item(int index);
     ```

- **NamedNodeMap**

  > 表示一组节点和其唯一名称的一一对应关系, 主要用于属性节点的表示

#### 4.2.3  DOM解析读操作

> 哪一个知识点和这特别像???

1. 建立DocumentBuilderFactory

   ```java
   DocumentBuilderFactory factory = DocumentBuilder Factory.newInstance();
   ```

2. 建立DocumentBuilder

   ```java
   DocumentBuilder builder = factory.newDocumentBuilder();
   ```

3. 建立Document

   ```java
   Document doc = builder.parse("要读取的文件路径");
   ```

4. 建立NodeList

   ```java
   NodeList nl = doc.getElementByTagName("读取节点");
   ```

5. 进行XML信息读取

   - **为什么要把NodeList中的获取的Node向下转型为Element?**

   ![image-20210301150002832](Java Web.assets/image-20210301150002832.png)

#### 4.2.4 DOM解析写操作

1. 取得一个TransformerFactory对象

   ```java
   TransformerFactory tf = TransformFactory.newInstance();
   ```

2. 取得一个Transformer对象并设置编码

   ```java
   Transformer t = tf.newTransformer();
   ```

   ```java
   t.setOutputProperty(OutputKeys.ENCODING, "utf-8");
   ```

3. 取得一个DOMSource对象

   ```java
   # 4.3.3 获取document实例化对象, 第三步可改为
   Document doc = builder.newDocument();来获取空白Document对象, 
   此对象用于DOMSource的构造参数
   ```

   ```java
   DOMSource source = new DOMSource(doc);
   ```

4. 指定输出流对象

   ```java
   public StreamResult(File f);
   public StreamResult(OutputStream outputStream);
   ```

5. 将XML写入指定的输出流

   ```java
   t.transform(source, result);
   ```

<img src="Java Web.assets/image-20210302233726961.png" alt="image-20210302233726961" style="zoom:50%;" />

<img src="Java Web.assets/image-20210302233803375.png" alt="image-20210302233803375" style="zoom:50%;" />

### 4.3 SAX解析

> Simple APIs for XML

#### 4.3.1 特点

1. 顺序模式访问, 可以快速读取XML, 操作时会触发一系列的事件

   <img src="Java Web.assets/image-20210301152327031.png" alt="image-20210301152327031" style="zoom:50%;" />

2. 主要事件

   - 文档开始

     ```java
     public void startDocument() throws SAXException;
     ```

   - 文档结束

     ```java
     public void endDocument() throws SAXException;
     ```

   - 元素开始

     > 可以取得元素的名称及元素的全部属性

     ```java
     public void startElement(String uri, String localName, String qName, Attributes attributes) throws SAXException;
     ```

   - 元素结束

     > 可以取得元素的名称及元素的全部属性

     ```java
     public void endElement(String uri, String localName, String qName) throws SAXException;
     ```

   - 元素内容

     ```java
     public void characters(char[] ch, int start, int length)throws SAXException;
     ```

#### 4.3.2 编写SAX解析器

> 该类需要继承DefaultHandler类

<img src="Java Web.assets/image-20210301153535763.png" alt="image-20210301153535763" style="zoom:50%;" />

#### 4.3.3 解析XML文件

1. 建立SAX解析工厂

   ```java
   SAXParserFactory factory = SAXParserFactory.newInstance();
   ```

2. 构造解析器

   ```java
   SAXParser parser = factory.newSAXParser();
   ```

3. 指定需要解析的XML文件和SAX解析器

   ```java
   parser.parse("XML file path", new MySAX())
   ```

   

### 4.4  DOM与SAX解析的区别

> 1. DOM适合对文件进行修改和随机存取, 不适合大型文件的操作
> 2. SAX适合处理大型文件, 可以建立自己的对象模型

![image-20210301154216185](Java Web.assets/image-20210301154216185.png)



### 4.5 JDOM

#### 4.5.1 主要操作类

1. Document

   > 定义了XML文件的各种操作

2. DOMBuilder

   > 用来建立JDOM结构树

3. Element

   > 定义了XML元素的各种操作

4. Attribute

   > 对元素中属性进行操作

5. XMLOutputter

   > 将一个JDOM结构树格式化为一个XML文件, 并指定输出对象

#### 4.5.2 使用JDOM生成XML文件

<img src="Java Web.assets/image-20210301160749935.png" alt="image-20210301160749935" style="zoom:50%;" />

#### 4.5.2 使用JDOM读取XML文件

> SAX解析方式读取

![image-20210301161453878](Java Web.assets/image-20210301161453878.png)



### 4.6 DOM4J

#### 4.6.1 主要接口

| 接口          | 描述                                                        |
| ------------- | ----------------------------------------------------------- |
| Attribute     | 定义了XML属性                                               |
| Branch        | 为了包含字节点的节点, 如XML元素和文档 ,定义了一个公共的行为 |
| CDATA         | 定义了XML CDATA区域                                         |
| CharacterData | 标识接口, 标识基于字符的节点, 如CDATA, Comment,  Text       |
| Comment       | 定义了XML的注释                                             |
| Document      | 定义了XML文档                                               |
| Element       | 定义了XML元素                                               |
| Text          | 定义了XML文本节点                                           |

#### 4.6.2 DOM4J 生成XML文件

<img src="Java Web.assets/image-20210301163221815.png" alt="image-20210301163221815" style="zoom: 50%;" />

<img src="Java Web.assets/image-20210301163459287.png" alt="image-20210301163459287" style="zoom:50%;" />

#### 4.6.3 DOM4J解析XML文件

<img src="Java Web.assets/image-20210301163624356.png" alt="image-20210301163624356" style="zoom:50%;" />



### 4.7 JavaScript操作DOM

#### 4.7.1 取得HTML元素并设置显示内容

<img src="Java Web.assets/image-20210301171451211.png" alt="image-20210301171451211" style="zoom:50%;" />

#### 4.7.2 通过DOM生成下拉列表框

<img src="Java Web.assets/image-20210301171336904.png" alt="image-20210301171336904" style="zoom:50%;" />



#### 4.7.3 JS动态操作表格

1. 增加新的表格行

   ```java
   insertRow();
   ```

2. 删除行中指定的单元格

   ```java
   deleteCell();
   ```

3. 在一行中的指定位置插入一个空的\<td>元素

   ```java
   insertCell();
   ```

   - **使用JS提供方法进行表格操作**

   <img src="Java Web.assets/image-20210301172919778.png" alt="image-20210301172919778" style="zoom:50%;" />

   - **表格的DOM树**

<img src="Java Web.assets/image-20210301173017206.png" alt="image-20210301173017206" style="zoom:50%;" />

- **使用DOM提供的方法进行表格操作**

<img src="Java Web.assets/image-20210301173538210.png" alt="image-20210301173538210" style="zoom:50%;" />

<img src="Java Web.assets/image-20210301173716853.png" alt="image-20210301173716853" style="zoom:50%;" />



## Tomcat

### Web容器

> 1. html, htm之类的一般属于静态请求, jsp, php之类的一般是动态请求
> 2. 静态请求的所以代码都是固定的, 而动态请求的所有代码都是拼凑而成的

![image-20210303215857049](Java Web.assets/image-20210303215857049.png)

### Tomcat

#### 主要目录的作用

![image-20210303223907838](Java Web.assets/image-20210303223907838.png)

![image-20210303223922955](Java Web.assets/image-20210303223922955.png)

## servlet

### servlet简介

![image-20210305193136214](Java Web.assets/image-20210305193136214.png)

![image-20210305193322394](Java Web.assets/image-20210305193322394.png)



![image-20210305201218667](Java Web.assets/image-20210305201218667.png)



![image-20210305203731252](Java Web.assets/image-20210305203731252.png)

#### 编写简单的HelloServlet程序

1.Servlet  java程序

```java
package com.liaolong.servlet;

import javax.servlet.ServletException;
import javax.servlet.ServletInputStream;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

/**
 * @author coderliaolong@outlook.com
 * @date 2021/3/5 20:40
 */
public class HelloServlet extends HttpServlet {

    // 由于get或者post只是请求实现的方式不同, 可以互相调用, 业务逻辑都一样
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

        ServletInputStream inputStream = req.getInputStream();
        // ServletOutputStream outputStream = resp.getOutputStream();
        PrintWriter writer = resp.getWriter();

        writer.print("Hello, Servlet!");

    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        doGet(req, resp);
    }
}
```

2.编写servlet映射 

![image-20210305205350590](Java Web.assets/image-20210305205350590.png)

### Servlet原理

servlet 由web容器调用, 可以实现, web服务器在收到浏览器请求后, 会: 

![image-20210305165343525](Java Web.assets/image-20210305165343525.png)