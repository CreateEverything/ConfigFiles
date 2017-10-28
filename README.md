# 索引
* [web.xml](#web.xml)
* [config-properties](#config-properties)
* [pom.xml](#pom.xml)
* [MyBatis.xml (MyBatis)](#MyBatis.xml)
* [generatorConfig.xml (MyBatis)](#generatorConfig.xml)
* [applicationContext.xml (Spring)](#applicationContext.xml)




<p id="web.xml"></p>

# web.xml
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
<p id="config-properties"></p>

# config-properties
```file
jdbc.driver=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///enter
jdbc.name=root
jdbc.password=rootroot


user.config.salt=!!@@##$$%%^^//盐
```
<p id="pom.xml"></p>

# pom.xml
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
    <!-- 此处为<apache-version>***<apache-version/> -->
  </properties>
    
  <dependencies>
	  <dependency>
    <!-- maven依赖的资源 -->
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

<p id="MyBatis.xml"><p>

# MyBatis.xml
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
<p id="generatorConfig.xml"></p>

# generatorConfig.xml
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
<p id="applicationContext.xml"></p>

# applicationContext.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
    <!--spring中管理的都是无状态的类,不要将有状态的类交给spring管理-->


    <!--有状态就是有数据存储功能。有状态对象(Stateful Bean)，
    就是有实例变量的对象 ，可以保存数据，是非线程安全的。
    在不同方法调用间不保留任何状态。

    无状态就是一次操作，不能保存数据。
    无状态对象(Stateless Bean)，
    就是没有实例变量的对象 不能保存数据，
    是不变类，是线程安全的-->


    <!--id为抽象方法名 class为抽象方法的实现类的绝对路径-->
    <bean id="action" class="com.kaishengit.test.Language"/>
    <!--起别名-->
    <!--<alias name="旧的name名" alias="新的名字"/>-->
    <!--id为任意但推荐使用类名 class为该类的绝对路径-->
    <bean id="person" class="com.kaishengit.test.Person" scope="prototype" lazy-init="true">
        <!--默认为singleton-->
        <!--bean的scope属性设置为prototype的时候 每次从spring中获取的对象都不相同-->

        <!--lazy-init默认为false 让类在调用getBean方法前就创建出类的对象-->
        <!--bean的lazy-init属性为true的时候 ，让类在调用getBean方法时再创建类的对象（懒加载）-->

        <!--name为该类中的方法去get首字母小写 ref是上面抽象方法id的值-->
        <property name="action" ref="action"/>
    </bean>
</beans>
```