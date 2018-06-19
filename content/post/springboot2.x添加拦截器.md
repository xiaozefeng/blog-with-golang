---
title: "SpringBoot2.x 添加拦截器"
date: 2018-06-13T21:48:56+08:00
draft: true
---

<!--more-->
## 声明拦截器
```java
@Slf4j
public class HttpInterceptor extends HandlerInterceptorAdapter {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        log.info("preHandler");
        return true;
    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        RequestHolder.remove();
        log.info("afterCompletion");
        return;

    }
}
```

## 配置拦截器
```java
@Configuration
public class WebConfiguration implements WebMvcConfigurer {

    /**
     * spring boot 2.x 添加拦截器的方式
     * @param registry
     */
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new HttpInterceptor()).addPathPatterns("/**");
    }
}
```
