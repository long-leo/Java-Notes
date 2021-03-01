# Git

本地文件上传到github

ssh密钥获取

```bash
ssh-keygen -t rsa -C "coderliaolong"
```

回车回车回车(不设置密码)

在窗口提示的目录下找到id_rsa.pub文件, 这是ssh公钥, 然后再github账号中添加这个ssh

新建一个仓库, 获取仓库的ssh  url

clone该仓库

```java
git clone "your ssh url"
```



