---
abbrlink: '0'
---
# SpringBoot 的核心注解是哪个？它主要由哪几个注解组成的？

启动类上面的注解是@SpringBootApplication，它也是 SpringBoot 的核心注解，主要组合包含了以下 3 个注解：

1，@SpringBootConfiguration:组合了@Configuration注解,实现配置文件的功能。

2，@EnableAotuConfiguration:打开自动配置功能，也可以关闭某些自动配置的选项 

3，@ComponentScan:Spring组件扫描功能，让SpringBoot扫描到Configuration类并把它加入到程序的上下文。



# springboot内置tomcat

