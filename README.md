# 索引
* [web.xml](#web.xml)
* [config-properties](#config-properties)
* [pom.xml](#pom.xml)
* [MyBatis.xml](#MyBatis.xml)
* [generatorConfig.xml](#generatorConfig.xml)




# web.xml
<p id="web.xml"></p>

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
# config-properties

<p id="config-properties"></p>

```file
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///enter
jdbc.name=root
jdbc.password=rootroot


user.config.salt=!!@@##$$%%^^//盐
```
# pom.xml
<p id="pom.xml"></p>

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  
  <modelVersion>4.0.0</modelVersion>
  
  <groupId>com.kaishengit</groupId>
  <artifactId>myblog</artifactId>
  <version>1.0-SNAPSHOT</version>
  <!-- 当程序需要在线上运行的时候是war -->
  <!-- 当程序作为工具类开发的时候是jar -->
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

# MyBatis.xml
<p id="MyBatis.xml"><p>

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <settings>
        <!--将数据库中下划线风格的命名映射为Java中驼峰命名风格-->
        <setting name="mapUnderscoreToCamelCase" value="true"/>
    </settings>

    <!--别名-->
    <typeAliases>
        <!--<typeAlias type="com.kaishengit.entity.Product" alias="Product"/>-->
        <package name="com.kaishengit.entity"/>
    </typeAliases>
    <!--分页插件-->
    <plugins>
        <plugin interceptor="com.github.pagehelper.PageInterceptor"></plugin>
    </plugins>

    <!--配置数据库环境-->
    <environments default="dev">
        <environment id="dev">
            <transactionManager type="JDBC"></transactionManager>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql:///test?useSSL=false"/>
                <property name="username" value="root"/>
                <property name="password" value="rootroot"/>
            </dataSource>
        </environment>
    </environments>

    <!--配置Mapper文件-->
    <mappers>
        <!--classpath中的路径-->
        <mapper resource="mapper/BookMapper.xml"/>
    </mappers>

</configuration>

```
# generatorConfig.xml
<p id="generatorConfig.xml"></p>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE generatorConfiguration
        PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
        "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>

    <!--获得数据库链接的jar包存放位置-->
    <classPathEntry location="C:\study\jar\mysql-connector-java-5.1.6.jar"/>

    <context id="myConfig" targetRuntime="MyBatis3">
        <!--设置不生成注释-->
        <commentGenerator>
            <property name="suppressAllComments" value="true"/>
            <property name="suppressDate" value="true"/>
        </commentGenerator>
        <!--配置数据链接信息-->
        <jdbcConnection driverClass="com.mysql.jdbc.Driver"
                        connectionURL="jdbc:mysql:///test?useSSL=false"
                        userId="root"  password="rootroot"/>
        <!--设置生成的实体类的存放位置-->
        <javaModelGenerator targetPackage="com.kaishengit.entity" targetProject="src/main/java"/>
        <!--设置xml配置文件的存放位置-->
        <sqlMapGenerator targetPackage="mapper" targetProject="src/main/resources"/>
        <!--设置mapper接口的存放位置-->
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.kaishengit.mapper" targetProject="src/main/java"/>
        <!--以去t_ 首字母大写的形式创建实体类-->
        <table tableName="t_book" domainObjectName="Book" enableSelectByExample="true"/>
    </context>
</generatorConfiguration>
```