从零开始搭建生学网项目
===

> Author: larry.koo  Date: 2017-11-08


### 项目结构搭建流程

**1. 从 Git 仓库 Checkout 源代码**

推荐使用`SourceTree`工具进行本地 Git 版本化的管理；  
下载地址: [https://www.sourcetreeapp.com/](https://www.sourcetreeapp.com/)

> git 使用不在详细叙述……

**2. 使用通用 pom 文件创建 Maven 根工程**

根据以下 `pom.xml`文件模版，创建相应工程的 pom 文件,这里已 sxw-cms-service为例，实际情况请根据项目规范名称和约定定义名称以及相应版本号；

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <parent>
        <groupId>cn.sxw.commons</groupId>
        <artifactId>sxw-commons-parent</artifactId>
        <version>1.2.0-SNAPSHOT</version>
    </parent>

    <modelVersion>4.0.0</modelVersion>

    <groupId>cn.sxw.pros.cms</groupId>
    <artifactId>sxw-cms-service</artifactId>
    <version>2.0.0-SNAPSHOT</version>
    <packaging>pom</packaging>

    <modules>
        <module>web</module>
    </modules>

    <name>sxw-cms-service</name>
    <description>生学网 - 内容管理服务 - Service</description>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <!-- 可以在这里强制覆盖依赖默认的版本号，只需要与依赖版本号使用的属性名称一致即可 -->
    </properties>

    <scm>
        <url>http://git.sxw.cn/sxw-java/sxw-cms-service</url>
        <connection>scm:git:git@git.sxw.cn:sxw-java/sxw-cms-service.git</connection>
        <developerConnection>scm:git:git@git.sxw.cn:sxw-java/sxw-cms-service.git</developerConnection>
    </scm>
</project>
```

将更新好的 `pom.xml` 文件放到 git 源代码根目录，然后从 IDEA 中导入该工程即可，导入后效果如下：

![](/assets/cms-service-parent.jpg)

**3. 创建需要的 Module**

导入POM工程后，我们在该Project 上右键创建需要的 Module 工程，这里以`sxw-cms-service`为例，创建以下 Module:

| Module名称 | 描述信息 |
| :--- | :--- |
| domain | Java Entity 对象 |
| client | API Interface 定义，同时暴露 Restful API 依赖 |
| biz | API Service 实现 |
| server | Web 启动 Module |

注意：除了 server module 需要保留`src/main/resources`和`src/test/java`以外，其他 module只需要保留 `src/main/java`源代码 Package 即可；

### 相关 Module 模版请参见下一节























