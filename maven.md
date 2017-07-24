# maven学习教程

## maven常见命令

> - ==mvn package==  
来构建项目
> - ==mvn compile==  
来编译项目
> - ==mvn clean==           
来清理项目
> - ==mvn test==            
来执行单元测试
> - ==mvn install==         
打包和部署项目到本地资源库
> - ==mvn site==            
来为您的项目生成信息文档站点
> - ==mvn site-deploy==     
通过WebDAV部署自动生成的文档站点到服务器
> - ==mvn tomcat:deploy==   
以 WAR 文件部署到 Tomcat
> - ==mvn eclipse:eclipse==   
将maven项目转化为Eclipse项目
> - ==mvn archetype:generate[-DgroupId -DartifactId -Dversion -Dpackage]==   
按照提示进行选择创建maven模板项目  
-DgroupId 组织名，公司网址的反写+项目名  
-DartifactId 项目名-模块名  
-Dversion 版本号  
-Dpackage 代码所存在的包名




## 配置maven的简单步骤

> 1. 配置jdk（略过，大家应该都会）
> 2. 下载并安装maven（去官网下载，然后解压。。不需要多说）
> 3. 配置M2_HOME和MAVEN_HOME (PS:其实一般配置一个就OK的，但一些项目仍然引用Maven文件夹MAVEN_HOME)
> 4. 修改path变量
> 5. 控制台下输入mvn -v 查看是否配置成功

## maven启用代理访问

我们可以在配置文件中配置代理服务器  
需要在安装目录的conf文件夹中的settings.xml中设置  
> {M2_HOME}/conf/settings.xml  

```
<!-- proxies
   | This is a list of proxies which can be used on this machine to connect to the network.
   | Unless otherwise specified (by system property or command-line switch), the first proxy
   | specification in this list marked as active will be used.
   |-->
  <proxies>
    <!-- proxy
     | Specification for one proxy, to be used in connecting to the network.
     |
    <proxy>
      <id>optional</id>
      <active>true</active>
      <protocol>http</protocol>
      <username>proxyuser</</username>
      <password>proxypass</password>
      <host>proxy.host.net</host>
      <port>80</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
    -->
  </proxies>
```
取消注释代理选项，然后填写您的代理服务器的详细信息ヾ(=ﾟ･ﾟ=)ﾉ喵♪

同样的，我们也可以在配置文件中修改仓库位置:
> 找到 {M2_HOME}\conf\setting.xml, 更新 localRepository 到其它名称。

## maven依赖机制
在 Maven 依赖机制的帮助下自动下载所有必需的依赖库，并保持版本升级。

### 案例分析

让我们看一个案例研究，以了解它是如何工作的。假设你想使用 Log4j 作为项目的日志。这里你要做什么？ 


#### 传统模式:

1. 访问jar包的网址
2. 下载log4j的jar库
3. 复制jar包到项目类路径
4. 手动将其包含到项目的依赖
5. 所有的一切管理需要自己做  

如果jar包要升级，就要重复以上步骤。


#### Maven模式

1. 你需要知道jar包的maven坐标，例如:  
```
<groupId>log4j</groupId>
<artifactId>log4j</artifactId>
<version>1.2.14</version>
```
2. 它会自动下载jar包的1.2.14版本库。如果version标签被忽略，它会在有新版本的时候自动升级库。
3. 声明maven的坐标转换为pom.xml文件。

```
<dependencies>
    <dependency>
	<groupId>log4j</groupId>
	<artifactId>log4j</artifactId>
	<version>1.2.14</version>
    </dependency>
</dependencies>
```

4. 当maven编译或构建时,log4j的jar包会自动下载,并把它放到Maven本地存储库。  
5. 所有都由maven管理


##### 原理解析

> 看看有什么不同？那么到底在Maven发生了什么？当建立一个Maven的项目，pom.xml文件将被解析，如果看到 log4j 的 Maven 坐标，然后 Maven 按此顺序搜索 log4j 库：


1.	在 Maven 的本地仓库搜索 log4j  
2.	在 Maven 中央存储库搜索 log4j 
3.	在 Maven 远程仓库搜索 log4j(如果在 pom.xml 中定义) 

> Maven 依赖库管理是一个非常好的工具，为您节省了大量的工作。 
> 如何找到 Maven 坐标？
> 访问 Maven 中心储存库，搜索下载您想要的jar。 


此外，maven还可以定制库到Maven本地资源库，需要时候可以自己查。



## 使用maven模板创建Java项目

**所需工具**
- Maven
- Eclipse
- JDK

### 从 Maven 模板创建一个项目

在命令行提示符中，浏览到要创建Java项目的文件夹，键入以下命令:  


```
mvn archetype:generate -DgroupId=com.henrygentry -DartifactId=helloworld2 -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```

ms-dos常见命令大全请参见：https://zhidao.baidu.com/question/59940919.html

生成的项目目录布局：

```
helloworld
   |-src
   |---main
   |-----java
   |-------com
   |---------henrygentry   
   |-----------App.java
   |---test|-----java
   |-------com
   |---------henrygentry 
   |-----------AppTest.java
   |-pom.xml
```

很简单的，所有的源代码放在文件夹 /src/main/java/, 所有的单元测试代码放入 /src/test/java/。

注意，请阅读 [Maven标准布局目录](http://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html)

> mvn eclipse-eclipse 命令可以将maven项目转化为eclipse项目进而导入eclipse

## 使用maven模板建立web项目

命令行为:  

```
$ mvn archetype:generate -DgroupId=com.henrygentry -DartifactId=CounterWebApp -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
```




