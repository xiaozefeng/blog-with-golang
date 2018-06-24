---
title: "SpringCloud Eureak学习(1)"
date: 2018-06-20T19:41:41+08:00
draft: true
tags: ["Spring Cloud"]
---

<!--more-->

## 搭建eureka server
### 使用idea创建一个eureka工程
``` xml
<parent>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-parent</artifactId>
	<version>2.0.3.RELEASE</version>
	<relativePath/> <!-- lookup parent from repository -->
</parent>

<properties>
	<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
	<java.version>1.8</java.version>
	<spring-cloud.version>Finchley.RELEASE</spring-cloud.version>
</properties>

<dependencies>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
	</dependency>

	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-test</artifactId>
		<scope>test</scope>
		</dependency>
	</dependencies>

<dependencyManagement>
	<dependencies>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-dependencies</artifactId>
			<version>${spring-cloud.version}</version>
			<type>pom</type>
			<scope>import</scope>
		</dependency>
	</dependencies>
</dependencyManagement>

```
### 在Application入口类上添加注解
```java
@EnableEurekaServer
```

## 配置eureka server 
```yml
# application name
spring:
  application:
    name: eureka
# eureak 服务地址
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:8761/eureka/
      # 不向自己注册
      register-with-eureka: false
      # 关闭自我保护机制 开发环境使用
      server:
        enable-self-preservation: false
# 端口
server:
  port: 8761

```
## eureka 高可用
### 两个实例的高可用
> 核心思想就是两个eureka服务相互注册

```yml
# 服务A
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:8762/eureka/
      # 不向自己注册
      register-with-eureka: false
server:
  port: 8761
  
# -------
# 服务B
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:8761/eureka/
      # 不向自己注册
      register-with-eureka: false
server:
  port: 8761
```

### 三个实例的高可用
> 核心思想就是服务之间两两注册

```yml
# 服务A
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:8762/eureka/,http://127.0.0.1:8763/eureka/
      # 不向自己注册
      register-with-eureka: false
server:
  port: 8761
  
# -------
# 服务B
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:8761/eureka/,http://127.0.0.1:8763/eureka/
      # 不向自己注册
      register-with-eureka: false
server:
  port: 8762
  
  # -------
# 服务C
eureka:
  client:
    service-url:
      defaultZone: http://127.0.0.1:8761/eureka/,http://127.0.0.1:8762/eureka/
      # 不向自己注册
      register-with-eureka: false
server:
  port: 8763
```
