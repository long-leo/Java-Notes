# Maven 

## 1. idea中配置Maven及使用

[Mave配置: 包含设置镜像及常用仓库](https://zhuanlan.zhihu.com/p/122429605)

[IDEA+MAVEN：踩坑指南](https://zhuanlan.zhihu.com/p/104311658)

[Maven最全教程，看了必懂](https://zhuanlan.zhihu.com/p/62841181)

## 2. 

```bash
mvn -version
```

![image-20210303235148830](Maven.assets/image-20210303235148830.png)

![image-20210303235731394](Maven.assets/image-20210303235731394.png)

## 3

#### maven在idea中配置详解

<img src="Maven.assets/image-20210304222636635.png" alt="image-20210304222636635" style="zoom:50%;" />

<img src="Maven.assets/image-20210304223101655.png" alt="image-20210304223101655" style="zoom:50%;" />

<img src="Maven.assets/image-20210304223200643.png" alt="image-20210304223200643" style="zoom:50%;" />

<img src="Maven.assets/image-20210304223331405.png" alt="image-20210304223331405" style="zoom:50%;" />![image-20210304223728273](Maven.assets/image-20210304223728273.png)

<img src="Maven.assets/image-20210304223331405.png" alt="image-20210304223331405" style="zoom:50%;" />![image-20210304223728273](Maven.assets/image-20210304223728273.png)![image-20210304223829752](Maven.assets/image-20210304223829752.png)

![image-20210304223829752](Maven.assets/image-20210304223829752.png)





#### 普通Maven项目

![image-20210304224137115](Maven.assets/image-20210304224137115.png)

<img src="Maven.assets/image-20210304224317513.png" alt="image-20210304224317513" style="zoom:50%;" />

<img src="Maven.assets/image-20210304224355132.png" alt="image-20210304224355132" style="zoom:50%;" />

<img src="Maven.assets/image-20210304224516161.png" alt="image-20210304224516161" style="zoom:50%;" />



#### idea中配置Tomcat

![image-20210304224738795](Maven.assets/image-20210304224738795.png)

![image-20210304224819285](Maven.assets/image-20210304224819285.png)

![image-20210304224900801](Maven.assets/image-20210304224900801.png)

![image-20210304225108978](Maven.assets/image-20210304225108978.png)

![image-20210304225303064](Maven.assets/image-20210304225303064.png)

![image-20210304225147510](Maven.assets/image-20210304225147510.png)

![image-20210304225206234](Maven.assets/image-20210304225206234.png)

![image-20210304225354636](Maven.assets/image-20210304225354636.png)

![image-20210304225500010](Maven.assets/image-20210304225500010.png)

![image-20210304225633834](Maven.assets/image-20210304225633834.png)

#### POM文件

> maven的核心配置文件

![image-20210304230031248](Maven.assets/image-20210304230031248.png)

![image-20210304230138441](Maven.assets/image-20210304230138441.png)

![image-20210304230243177](Maven.assets/image-20210304230243177.png)

#### 干净的maven项目

> 手动配置

![image-20210304230440794](Maven.assets/image-20210304230440794.png)

![image-20210304230737831](Maven.assets/image-20210304230737831.png)

![image-20210304230658630](Maven.assets/image-20210304230658630.png)

#### 原build文件

```xml
<build>
    <finalName>javaweb-01-maven01</finalName>
    <pluginManagement><!-- lock down plugins versions to avoid using Maven defaults (may be moved to parent pom) -->
        <plugins>
            <plugin>
                <artifactId>maven-clean-plugin</artifactId>
                <version>3.1.0</version>
            </plugin>
            <!-- see http://maven.apache.org/ref/current/maven-core/default-bindings.html#Plugin_bindings_for_war_packaging -->
            <plugin>
                <artifactId>maven-resources-plugin</artifactId>
                <version>3.0.2</version>
            </plugin>
            <plugin>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.0</version>
            </plugin>
            <plugin>
                <artifactId>maven-surefire-plugin</artifactId>
                <version>2.22.1</version>
            </plugin>
            <plugin>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.2.2</version>
            </plugin>
            <plugin>
                <artifactId>maven-install-plugin</artifactId>
                <version>2.5.2</version>
            </plugin>
            <plugin>
                <artifactId>maven-deploy-plugin</artifactId>
                <version>2.8.2</version>
            </plugin>
        </plugins>
    </pluginManagement>
</build>
```



![image-20210304230824499](Maven.assets/image-20210304230824499.png)

 