---
title: "SpringBoot Data JPA使用@CreatedDate、@CreatedBy、@LastModifiedDate、@LastModifiedBy自动生成时间和修改者"
date: 2018-06-22T22:47:57+08:00
draft: true
tags: ["Spring Boot"]
---

<!--more-->

## 在启动类上添加`@EnableJpaAuditing`注解
## 在实体类上添加`@EntityListeners(AuditingEntityListener.class)`注解
##  `@CreateDate,@ LastModifiedDate`
```java
 	/**
     * 创建时间
     */
    @Column(name = "TIME_CREATED")
    @CreatedDate
    private LocalDateTime timeCreated;

    /**
     * 更新时间
     */
    @Column(name = "TIME_LAST_UPDATED")
    @LastModifiedDate
    private LocalDateTime timeLastUpdated;
```
## 配置`@CreatedBy,@LastModifiedBy`
> 因为创建和最后更新人没有默认值，所以需要设置默认值

```java
@Configuration
public class AuditingEntityConfiguration implements AuditorAware<String> {
    @Override
    public Optional<String> getCurrentAuditor() {
        // 可以获取Spring容器的bean
        // 使用Spring Security可以拿到对应的登录人信息
        return Optional.of("system");
    }
}
```
