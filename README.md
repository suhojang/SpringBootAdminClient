### Spring Boot Admin Client

- Spring Boot Admin Client
    * 사용 가이드
        + [Dependency](#Dependency), [Gradle](#Gradle)
        + [SecurityConfig 설정](#SecurityConfig)
        + [yml 설정](#yml)
        + [Spring Boot Admin Viewer](#SpringBootAdminView)
        + [Spring Boot Admin GitHub](https://github.com/suhojang/SpringBootAdminClient)
    * Reference SITE
        + [Spring Boot Admin Reference Guide](https://codecentric.github.io/spring-boot-admin/current/)

#### Dependency
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
    <groupId>de.codecentric</groupId>
    <artifactId>spring-boot-admin-starter-client</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>

<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-test</artifactId>
    <scope>test</scope>
</dependency>
```

#### Gradle
```groovy
implementation 'org.springframework.boot:spring-boot-starter-web'
implementation 'de.codecentric:spring-boot-admin-starter-client'
implementation 'org.springframework.boot:spring-boot-starter-actuator'
implementation 'org.springframework.boot:spring-boot-starter-security'
testImplementation 'org.springframework.boot:spring-boot-starter-test'
testImplementation 'org.springframework.security:spring-security-test'
```
#### SecurityConfig
````java
package com.jsh.SpringBootClient;

import org.springframework.context.annotation.Configuration;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;

@Configuration
public class SecurityPermitAllConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests().anyRequest().permitAll()
                .and().csrf().disable();
    }
}
````

#### yml
````yml
spring:
  application:
    name: boot admin A Client
  boot:
    admin:
      client:
        #Spring Boot Admin Server
        url: http://localhost:8080
        instance:
          #meta 정보
          metadata:
            name: ${spring.application.name}
            user.name: ${spring.security.user.name}
            user.password: ${spring.security.user.password}
        #Spring Boot Admin Security user/password 설정
        username: ${spring.security.user.name}
        password: ${spring.security.user.password}
  security:
    user:
      name: jsh2808
      password: 1234
# actuator endPoint 설정      
management:
  endpoints:
    web:
      exposure:
        include: "*"
    health:
      show-details: always
# Server 정보 설정
server:
  address: localhost
  port: 18080

# logging정보 설정
logging:
  file:
    name: boot-admin-A-Client.log
    max-history: 5
    max-size: 10MB
````
#### SpringBootAdminView
![Spring Boot Admin](https://github.com/suhojang/SpringBootAdmin/blob/master/springbootAdmin.png)
