# spring boot 学习笔记

## 1、spring jpa
#### 数据库连接
    在src/main/resources 目录下的application.properties文件中添加如下配置
    spring.datasource.driverClassName = com.mysql.jdbc.Driver
    spring.datasource.url=jdbc:mysql://127.0.0.1:3306/restfulldemo?useUnicode=true&characterEncoding=utf-8
    spring.datasource.username = root
    spring.datasource.password =
    
## log4j
    spring boot 默认使用的日志是Logback。 如果想使用log4j,首先修改pom文件
    排除默认的loging
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <exclusions>
		        <exclusion>
		            <groupId>org.springframework.boot</groupId>
		            <artifactId>spring-boot-starter-logging</artifactId>
		        </exclusion>
		    </exclusions>
        </dependency>
        添加log4j
        <dependency>
        	<groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-log4j</artifactId>
        </dependency>