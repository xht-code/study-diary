# Spring Boot

## 目录

1. [@RestController](#@restcontroller)
    1. [作用](#作用)
    1. [样例](#样例)
    1. [参考](#参考)
1. [运行命令](#运行命令)
    1. [命令](#命令)
    1. [解析](#解析)
    1. [补充](#补充)
    1. [参考](#参考-1)
1. [Druid](#druid)
1. [PageHelper](#pagehelper)

## @RestController

  ### 作用
  > Spring4之后新加入的注解，原来返回json需要 `@ResponseBody` 和 `@Controller` 配合。即 `@RestController` 是 `@ResponseBody` 和 `@Controller` 的组合注解。

  ### 样例
  ``` java
  @RestController
  public class HelloController {

    @RequestMapping(value="/hello",method= RequestMethod.GET)
    public String sayHello(){
      return "hello";
    }
  }
  ```
  与下面的代码作用一样
  ``` java
  @Controller
  @ResponseBody
  public class HelloController {

    @RequestMapping(value="/hello",method= RequestMethod.GET)
    public String sayHello(){
      return "hello";
    }
  }
  ```

  ### 参考
  <https://blog.csdn.net/u010412719/article/details/69710480>

## 运行命令

  ### 命令
  ```
  nohup java -jar xxx.jar >/dev/null 2>&1 &
  ```

  ### 解析
  - `nohup` 不挂断地运行命令

  - `/dev/null` 是一个虚拟的空设备
  
    > *任何输出信息被重定向到该设备后，将会石沉大海*

  - `>/dev/null` 表示将标准输出信息重定向到**空设备**

  - `2>&1` 表示将标准错误重定向到标准输出

  ### 补充
  > 可通过 `jobs` 命令查看后台运行任务


  ### 参考
  <https://www.cnblogs.com/yjmyzz/p/4831182.html>

  <https://www.cnblogs.com/baby123/p/6477429.html>

## Druid

  ### 环境
  > JDK: 1.8.0_171
  > Druid: 1.1.10
  > IDE: Intellij IDEA

  ### 配置 Maven
  ``` xml
  <dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid-spring-boot-starter</artifactId>
    <version>1.1.10</version>
  </dependency>
  ```

  ### 配置 application.yml
  ``` yml
  spring:
    datasource:
      druid:
        initial-size: 2
        min-idle: 2
        max-active: 20
        max-wait: 60000
        validationQuery: SELECT 1
        filters: stat,wall,log4j
        stat-view-servlet:
          enabled: true
          url-pattern: /druid/*
          reset-enable: true
          login-username: admin
          login-password: admin
          allow: 127.0.0.1
        one:
          driver-class-name: com.mysql.jdbc.Driver
          initialize: true
          url: jdbc:mysql://localhost:3306/db_one?useUnicode=true&characterEncoding=UTF8&useSSL=true
          username: root
          password: root
        two:
          driver-class-name: com.mysql.jdbc.Driver
          initialize: true
          url: jdbc:mysql://localhost:3306/db_two?useUnicode=true&characterEncoding=UTF8&useSSL=true
          username: root
          password: root
  ```

  ### 配置 DateSource
  ``` java
  @Bean
  @Primary
  @ConfigurationProperties(prefix = "spring.datasource.druid.one")
  public DataSource oneData() {
      return DruidDataSourceBuilder.create().build();
  }

  @Bean
  @ConfigurationProperties(prefix = "spring.datasource.druid.two")
  public DataSource twoData() {
      return DruidDataSourceBuilder.create().build();
  }
  ```

  ### 参考
  <https://blog.csdn.net/wkztselina/article/details/79321735>

## PageHelper

  ### Maven引入
  ``` xml
  <dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.2.5</version>
  </dependency>
  ```

  ### application.yml
  ``` yml
  pagehelper:
    helperDialect: mysql
    reasonable: true
    supportMethodsArguments: true
    params: count=countSql
  ```

  ### 参考
  <https://blog.csdn.net/u013305783/article/details/78563389>

