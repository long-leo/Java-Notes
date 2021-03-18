# Mybatis

### 什么是Mybatis

![image-20210312224733017](Mybatis.assets/image-20210312224733017.png)

![image-20210312225128353](Mybatis.assets/image-20210312225128353.png)

![image-20210312225253100](Mybatis.assets/image-20210312225253100.png)

![image-20210312225611817](Mybatis.assets/image-20210312225611817.png)

### 编写第一个Mybatis程序

**使用新技术的学习思路:** 搭建环境  --->  导入Mybatis  --> 编写代码  --->   测试

1.搭建环境

![image-20210312230424339](Mybatis.assets/image-20210312230424339.png)

2.导入核心依赖

![image-20210312230706771](Mybatis.assets/image-20210312230706771.png)

3.编写Mybatis核心配置文件

![image-20210312231524772](Mybatis.assets/image-20210312231524772.png)

4.编写Mybatis工具类

![image-20210312232125073](Mybatis.assets/image-20210312232125073.png)

5.User类, UserDAO接口

6.编写mapper.xml(替代UserDaoImpl类的繁琐的JDBC操作)

![image-20210312233347810](Mybatis.assets/image-20210312233347810.png)

7.测试

![image-20210312233744482](Mybatis.assets/image-20210312233744482.png)

![image-20210312234034445](Mybatis.assets/image-20210312234034445.png)

![image-20210312234728349](Mybatis.assets/image-20210312234728349.png)

![image-20210312234944669](Mybatis.assets/image-20210312234944669.png)

![image-20210312235424761](Mybatis.assets/image-20210312235424761.png)

![image-20210313190615136](Mybatis.assets/image-20210313190615136.png) 





### 万能的Map

![image-20210313202016228](Mybatis.assets/image-20210313202016228.png)





### 模糊查询

![image-20210313203449691](Mybatis.assets/image-20210313203449691.png)

![image-20210313203341567](Mybatis.assets/image-20210313203341567.png)





### Mybatis配置

![image-20210313204525235](Mybatis.assets/image-20210313204525235.png)

![image-20210313204710665](Mybatis.assets/image-20210313204710665.png)

![image-20210313205135800](Mybatis.assets/image-20210313205135800.png)

### Mapper映射配置

![image-20210313213106134](Mybatis.assets/image-20210313213106134.png)

![image-20210313213251239](Mybatis.assets/image-20210313213251239.png)

### 生命周期和作用域

![image-20210313213956316](Mybatis.assets/image-20210313213956316.png)

### 实体类属性名与数据库字段名不一致的问题

![image-20210313214504340](Mybatis.assets/image-20210313214504340.png)

![image-20210313215049982](Mybatis.assets/image-20210313215049982.png)

![image-20210313215257241](Mybatis.assets/image-20210313215257241.png)





### 日志

![image-20210313221622789](Mybatis.assets/image-20210313221622789.png)

![image-20210313222120154](Mybatis.assets/image-20210313222120154.png)

![image-20210313223007002](Mybatis.assets/image-20210313223007002.png)

```properties
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG，console，file
#控制台输出的相关设置
log4j.appender.console=org.apache.log4j.ConsoleAppender
log4j.appender.console.Target=System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout=org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n
#文件输出的相关设置
log4j.appender.file=org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/liaolong.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n
#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```

```properties
# Set root logger level to DEBUG and its only appender to A1.
log4j.rootLogger=DEBUG, A1

# A1 is set to be a ConsoleAppender.
log4j.appender.A1=org.apache.log4j.ConsoleAppender

# A1 uses PatternLayout.
log4j.appender.A1.layout=org.apache.log4j.PatternLayout
log4j.appender.A1.layout.ConversionPattern=%-4r [%t] %-5p %c %x - %m%n
```



1. 加载配置

   ```java
   BasicConfigurator.configure();
   ```

#### 简单使用

![image-20210313234322701](Mybatis.assets/image-20210313234322701.png)

![image-20210313234306670](Mybatis.assets/image-20210313234306670.png)





### 分页

> 分页是为了减少数据的处理量

![image-20210314101955861](Mybatis.assets/image-20210314101955861.png)



#### RowBounds分页(了解即可)

![image-20210314104558904](Mybatis.assets/image-20210314104558904.png)

![image-20210314104757416](Mybatis.assets/image-20210314104757416.png)





### 使用注解开发

![image-20210314105039868](Mybatis.assets/image-20210314105039868.png)

![image-20210314105052167](Mybatis.assets/image-20210314105052167.png)





### Mybatis详细执行流程

![image-20210314112401841](Mybatis.assets/image-20210314112401841.png)

![image-20210314112429859](Mybatis.assets/image-20210314112429859.png)

![image-20210314112457282](Mybatis.assets/image-20210314112457282.png)

![image-20210314112510737](Mybatis.assets/image-20210314112510737.png)





### 注解实现增删改查

![image-20210314113236595](Mybatis.assets/image-20210314113236595.png) 

![image-20210314113348511](Mybatis.assets/image-20210314113348511.png)





### 多对一

![image-20210314145246638](Mybatis.assets/image-20210314145246638.png)



#### 查询方式一

![image-20210314150428950](Mybatis.assets/image-20210314150428950.png)

#### 查询方式二

![image-20210314150743021](Mybatis.assets/image-20210314150743021.png)

![image-20210314150900048](Mybatis.assets/image-20210314150900048.png)





### 一对多

![image-20210314151800160](Mybatis.assets/image-20210314151800160.png)

![image-20210314152337546](Mybatis.assets/image-20210314152337546.png)

![image-20210314152456649](Mybatis.assets/image-20210314152456649.png)

![image-20210314152816998](Mybatis.assets/image-20210314152816998.png)