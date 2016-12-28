# SpringMVC学习笔记

## 一、SpringMVC基础入门，创建一个HelloWorld程序

### 1.首先使用maven引用jar包
     
       commons-logging-1.2.jar
       spring-aop-4.1.6.RELEASE.jar
       spring-beans-4.1.6.RELEASE.jar
       spring-context-4.1.6.RELEASE.jar
       spring-core-4.1.6.RELEASE.jar
       spring-expression-4.1.6.RELEASE.jar
       spring-web-4.1.6.RELEASE.jar
       spring-webmvc-4.1.6.RELEASE.jar
     

### 2.添加web.xml配置文件中关于SpringMVC的配置

       <!--configure the setting of springmvcDispatcherServlet and configure the mapping-->
       <servlet>
          <servlet-name>springmvc</servlet-name>
          <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
          <init-param>
             <param-name>contextConfigLocation</param-name>
             <param-value>classpath:spring/springmvc-servlet.xml</param-value>
          </init-param>
         <!-- <load-on-startup>1</load-on-startup> -->
       </servlet>

       <servlet-mapping>
          <servlet-name>springmvc</servlet-name>
          <url-pattern>/</url-pattern>
       </servlet-mapping>
          
### 3.在resource/spring下添加springmvc-servlet.xml文件
      <?xml version="1.0" encoding="UTF-8"?>
      <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:context="http://www.springframework.org/schema/context"
           xmlns:mvc="http://www.springframework.org/schema/mvc"
           xsi:schemaLocation="http://www.springframework.org/schema/beans 
               http://www.springframework.org/schema/beans/spring-beans.xsd
               http://www.springframework.org/schema/context
               http://www.springframework.org/schema/context/spring-context-4.1.xsd
               http://www.springframework.org/schema/mvc 
               http://www.springframework.org/schema/mvc/spring-mvc-4.1.xsd">                    

      <!-- scan the package and the sub package -->
      <context:component-scan base-package="com.lihebin.SpringMVC"/>

      <!-- don't handle the static resource -->
      <mvc:default-servlet-handler />

      <!-- if you use annotation you must configure following setting -->
      <mvc:annotation-driven />
    
      <!-- configure the InternalResourceViewResolver -->
      <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver" 
            id="internalResourceViewResolver">
        <!-- 前缀 -->
        <property name="prefix" value="/WEB-INF/jsp/" />
        <!-- 后缀 -->
        <property name="suffix" value=".jsp" />
      </bean>
    </beans>

### 4.在webapp/WEB-INF文件下创建名为jsp的文件夹，用来存放jsp视图。创建一个hello.jsp

### 5.建立包及对应的java文件，并编写代码


## 二、配置解析
   
### 1.Dispatcherservlet

    DispatcherServlet是前置控制器，配置在web.xml文件中的。拦截匹配的请求，Servlet拦截匹配规则要自已定义，把拦截下来的请求，依据相应的规则分发到目标Controller来处理，是配置spring MVC的第一步。

### 2.InternalResourceViewResolver

     视图名称解析器

## 三、SpringMVC常用注解

     @Controller

         负责注册一个bean到spring上下文

     @RequestMapping

         注解为控制器指定可以处理哪些URL请求

     @RequestBody
      
         该注解用于读取Request请求的body部分数据，使用系统默认配置的HttpMessageConverter进行
       解析，然后把相应的数据绑定到要返回的对象上，再把HttpMessageConverter返回的对象数据绑定
       到controller中方法的参数上。
     
     @ResponseBody

         该注解用于将Controller的方法返回的对象，通过适当的HttpMessageConverter转换为指定格式
       后,写入到Response对象的body数据区。
     
     @ModelAttribute
      
         在方法定义上使用@ModelAttribute注解:Spring MVC在调用目标处理方法前，会先逐个调用在方法
       级上标注了@ModelAttribute的方法
          在方法的入参前使用@ModelAttribute注解：可以从隐含对象中获取对象，再将请求参数绑定到对象
       中，再传入入参，将方法对象添加到模型中。

    @RequestParam

         在处理方法入参处使用@RequestParam可以把请求参数传递给请求方法

    @PathVariable

         绑定URL占位符到入参

    @ExceptionHandler
       
         注解到方法上，出现异常时会执行该方法
    
    @ControllerAdvice
    
        使一个Contoller成为全局的异常处理类，类中用@ExceptionHandler方法注解的方法可以处理所
     有Controller发生的异常

    