# Halo

## 准备工作

[halo运行](https://www.jianshu.com/p/4a64a9666415)

[helo官方文档](https://docs.halo.run/developer-guide/core/prepare)

[java运行环境](https://blog.csdn.net/programminging/article/details/80770294?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&dist_request_id=&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.control)

[多个jdk版本安装](https://blog.csdn.net/zdl177/article/details/105246997)

[commad line is too long](https://blog.csdn.net/ZXJ_1223/article/details/80611089)

[查看端口被哪个程序占用](https://jingyan.baidu.com/article/3c48dd34491d47e10be358b8.html)

[halo页面主题找不到的解决办法](https://bbs.halo.run/d/504-themes-anatole)



## 组成

| 名称         | 简介                                                         |
| ------------ | ------------------------------------------------------------ |
| halo         | 提供整个系统的服务, 采用**spring boot**开发                  |
| halo-admin   | 负责后台管理的渲染, 采用**Vue**开发, 已集成在halo允许包内, 无须独立部署 |
| halo-comment | **Vue**开发, 在主题中运行方式:  在主题中引入构建好的**JavaScript**文件即可 |
| halo-theme-* | 主题项目集，采用 [Freemarker](https://freemarker.apache.org/) 模板引擎编写，需要包含一些特殊的配置才能够被 halo 所使用 |



## 自定义配置

`Halo` 配置目录优先级如下（从上到下优先级越来越小，上层的配置将会覆盖下层）:

>  `Halo`自定义配置

- file:~/.halo/
- file:~/.halo-dev/

> `Spring Boot`默认配置

- file:./config/
- file:./
- classpath:/config/
- classpath:/



## halo

