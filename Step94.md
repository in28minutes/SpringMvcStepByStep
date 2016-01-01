pom.xml
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.in28minutes</groupId>
	<artifactId>spring-mvc-first-web-app-step-by-step</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>

	<dependencies>
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-webmvc</artifactId>
			<version>4.0.6.RELEASE</version>
		</dependency>


		<dependency>
			<groupId>javax</groupId>
			<artifactId>javaee-web-api</artifactId>
			<version>6.0</version>
			<scope>provided</scope>
		</dependency>

		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>
	</dependencies>

	<build>
		<pluginManagement>
			<plugins>
				<plugin>
					<groupId>org.apache.maven.plugins</groupId>
					<artifactId>maven-compiler-plugin</artifactId>
					<version>3.2</version>
					<configuration>
						<verbose>true</verbose>
						<source>1.8</source>
						<target>1.8</target>
						<showWarnings>true</showWarnings>
					</configuration>
				</plugin>
				<plugin>
					<groupId>org.apache.tomcat.maven</groupId>
					<artifactId>tomcat7-maven-plugin</artifactId>
					<version>2.2</version>
					<configuration>
						<path>/</path>
						<contextReloadable>true</contextReloadable>
					</configuration>
				</plugin>
			</plugins>
		</pluginManagement>
	</build>
</project>
```
src\main\java\com\in28minutes\HelloWorldController.java
```
package com.in28minutes;

import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

@Controller
@RequestMapping("/")
public class HelloWorldController {

	@RequestMapping(method = RequestMethod.GET)
	public String sayHello(ModelMap model) {
		model.put("welcomeMessage", "Welcome to the wonderful world of Spring MVC");
		return "welcome";
	}

	@RequestMapping(value = "/something-else", method = RequestMethod.GET)
	public String saySomethingElse(ModelMap model) {
		model.put("welcomeMessage", "What else to say about the wonderful world of Spring MVC");
		return "welcome";
	}
}
```
src\main\webapp\WEB-INF\todo-servlet.xml
```
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:context="http://www.springframework.org/schema/context"
    xmlns:mvc="http://www.springframework.org/schema/mvc"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.0.xsd
    http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.0.xsd
    http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.0.xsd">
 
    <context:component-scan base-package="com.in28minutes" />
 
    <mvc:annotation-driven />
     
    <bean
        class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix">
            <value>/WEB-INF/views/</value>
        </property>
        <property name="suffix">
            <value>.jsp</value>
        </property>
    </bean>
 
</beans>
```
src\main\webapp\WEB-INF\views\welcome.jsp
```
<!DOCTYPE html>
<html>
<head>
<title>HelloWorld page</title>
</head>
<body>
    Greetings from in28Minutes!! ${welcomeMessage}
</body>
</html>
```
src\main\webapp\WEB-INF\web.xml
```
<!-- webapp/WEB-INF/web.xml -->
<web-app xmlns="http://java.sun.com/xml/ns/javaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
    version="3.0">

	<display-name>To do List</display-name>

 	<servlet>
    	<servlet-name>dispatcher</servlet-name>
    	<servlet-class>
        	org.springframework.web.servlet.DispatcherServlet
    	</servlet-class>
    	<init-param>
        	<param-name>contextConfigLocation</param-name>
        	<param-value>/WEB-INF/todo-servlet.xml</param-value>
    	</init-param>
    	<load-on-startup>1</load-on-startup>
 	</servlet>
 
 	<servlet-mapping>
    	<servlet-name>dispatcher</servlet-name>
    	<url-pattern>/</url-pattern>
 	</servlet-mapping>
 
</web-app>
```
