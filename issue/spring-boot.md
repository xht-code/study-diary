# Spring Boot

## 1. Whitelabel Error Page

  ### 原因
  > 程序只加载`Application.java`所在包及其子包下的内容

  ### 解决方法
  1. 在`Application`类中加上`@ComponentScan(basePackages = {"com.demo.controller"})`
  1. 把`Application`放在`controller`或上级目录

  ### 参考
  <https://www.cnblogs.com/JealousGirl/p/whitelabel.html>

  ### 官网
  <https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#using-boot-locating-the-main-class>

## 2. Druid 数据源为空

  ### 问题描述
  ```
  (*) property for user to setup
  ```

  ### 解决方法
  应该使用 `druid` 提供的 `DruidDataSourceBuilder` 而不是 `DataSourceBuilder`
  ``` java
  @Bean
  @Primary
  @ConfigurationProperties(prefix = "spring.datasource.druid.one")
  public DataSource oneData() {
      return DruidDataSourceBuilder.create().build();
  }
  ```