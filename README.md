web.xml
============
```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
         version="3.1">
<!-- 解决中文乱码 -->
<filter>
	<filter-name>encoding</filter-name>
	<filter-class>com.kaishengit.Filter.InitValidateFilter</filter-class>
	<init-param>
		<param-name>characterEncoding</param-name>
		<param-value>UTF-8</param-value>
	</init-param>
</filter>

<welcome-file-list>
	<welcome-file>index.jsp</welcome-file>
</welcome-file-list>
	
</web-app>

```
config-properties
==========
```file
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///enter
jdbc.name=root
jdbc.password=rootroot


user.config.salt=!!@@##$$%%^^//盐
```
pom.xml
==========
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  
  <modelVersion>4.0.0</modelVersion>
  
  <groupId>com.kaishengit</groupId>
  <artifactId>myblog</artifactId>
  <version>1.0-SNAPSHOT</version>
  
  <packaging>war</packaging>
  
  <properties>

  </properties>
  
  <dependencies>
	  <dependency>
		   
	  </dependency>
  </dependencies>
  
  <build>
  	<plugins>
  		<!-- 编译插件 -->
  		<plugin>
			<groupId>org.apache.maven.plugins</groupId>
			<artifactId>maven-compiler-plugin</artifactId>
			<version>3.1</version>
			<configuration>
			<source>1.8</source>
			<target>1.8</target>
			<encoding>UTF-8</encoding>
			</configuration>
		</plugin>
		<!-- Tomcat插件 -->
		<plugin>
			<groupId>org.apache.tomcat.maven</groupId>
			<artifactId>tomcat7-maven-plugin</artifactId>
			<version>2.2</version>
			<configuration>
			<port>8080</port>
			<path>/</path>
			</configuration>
		</plugin>
  	</plugins>
  </build>
</project>

```
****
![](http://img2.imgtn.bdimg.com/it/u=3027868233,561243563&fm=27&gp=0.jpg)