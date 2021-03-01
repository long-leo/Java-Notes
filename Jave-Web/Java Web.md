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

#### 3.8.4close()

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



### 3.8 练习

emp.html

```html
<html>
    <head>
        <title>ll</title>
        <script language="JavaScript" src="check.js">
        	
        </script>
    </head>
    <form action="" method="post" name= empForm onSubmit="return check(this)">
        雇员编号:<input type="text" name="empno" >
        <p name="empnoError"></p><br />
        雇员姓名:<input type="text" name="empName">
        <p name="empnoNameError"></p><br />
        雇员工作:<input type="text" name="job">
        <p name="jobError"></p><br />
        雇佣日期:<input type="text" name="date">
        <p name="dateError"></p><br />
        基本工资:<input type="text" name="salary">
        <p name="salaryError"></p><br />
        奖&nbsp;&nbsp;&nbsp;&nbsp;金:<input type="text" name="bonus">
        <p name="bonusError"></p><br />
        <hr />
        <input type="submit" value="提交">
        <input type="reset" value="重置">
    </form>
</html>
```

<form action="" method="post">
        雇员编号:<input type="text" name="empno" ><br />
        雇员姓名:<input type="text" name="empName"><br />
        雇员工作:<input type="text" name="job"><br />
        雇佣日期:<input type="text" name="date"><br />
        基本工资:<input type="text" name="salary"><br />
        奖&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;金:<input type="text" name="bonus"><br />
        <hr />
        <input type="submit" value="提交">
        <input type="reset" value="重置">
    </form>

check.js

```js
function check(f){
    if (! /^\d+$/.test(f.empno)){
        f.empnoError.value ="只能是数字";
        f.empno.focus();
        f.empno.select();
        return false;
    }
    if (f.empName == ""){
        f.empNameError.value ="不能为空";
        f.empName.focus();
        f.empName.select();
        return false;
    }
    if (f.job == ""){
        f.jobError.value ="不能为空";
        f.job.focus();
        f.job.select();
        return false;
    }
    if (! /^\d{4}-\d{2}-\d{2}$/.test(f.date)){
        f.dateError.value="日期格式:年-月-日, 如2021-02-28";
        f.date.focus();
        f.date.select();
        return false;
    }
    if (! (/^\d+.\d+$/.test(f.salary) || /^\d+$/.test(f.salary) )){
        f.salaryError.value="必须是整数或小数";
        f.salary.focus();
        f.salary.select();
        return false;
    }
     if (! (/^\d+.\d+$/.test(f.bonus) || /^\d+$/.test(f.bonus )){
        f.bonusError.value="必须是整数或小数";
        f.bonus.focus();
        f.bonus.select();
    	return false;
    }
	return true;
}
```

