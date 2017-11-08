生学网项目初始化流程
===

> Author: larry.koo  Date: 2017-11-08

**1. 从 Git 仓库 Checkout 源代码**

推荐使用`SourceTree`工具进行本地 Git 版本化的管理；
下载地址: https://www.sourcetreeapp.com/

> git 使用不在详细叙述……

**2. 使用通用 pom 文件创建 Maven 根工程**

根据以下 `pom.xml`文件模版，创建相应工程的 pom 文件：

```
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
        <!-- 可以在这里强制覆盖依赖默认的版本号，只需要与依赖版本号使用的属性名称一致即可 -->
    </properties>

    <scm>
        <url>http://git.sxw.cn/sxw-java/sxw-cms-service</url>
        <connection>scm:git:git@git.sxw.cn:sxw-java/sxw-cms-service.git</connection>
        <developerConnection>scm:git:git@git.sxw.cn:sxw-java/sxw-cms-service.git</developerConnection>
    </scm>
</project>
```