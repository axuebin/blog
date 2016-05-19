## Maven简单了解

最重要的就是POM，就是通过一个POM.XML来管理整个项目的依赖关系，jar包等。

## Maven的安装

### 下载Maven

Maven下载地址：[https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi) 如图所示，选择这个zip就可以了

![QQ截图20160518212442.png](C:\Users\b\Desktop\QQ截图20160518212442.png)

解压至你喜欢的目录就好了

### 配置环境变量

- M2_HOME: D:\apache-maven-3.3.1 也就是你maven的目录
- path：%M2_HOME%\bin

### 测试一下

简单的两部就安装好了，在命令行中测试一下：

```
mvn -version
```

会得到这样的结果：


![QQ截图20160518213039.png](C:\Users\b\Desktop\QQ截图20160518213039.png)

也就是可以在命令行中看到maven、java等一些信息。

## 创建Maven项目

### eclipse中配置maven

在eclipse中点击Window -> Preferences,然后

![QQ截图20160518214757.png](C:\Users\b\Desktop\QQ截图20160518214757.png)

再修改

![QQ图片20160518215308.png](C:\Users\b\Desktop\QQ图片20160518215308.png)

这就就配置好maven了

### 