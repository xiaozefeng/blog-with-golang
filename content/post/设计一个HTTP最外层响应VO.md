---
title: "设计一个HTTP最外层响应VO"
date: 2018-06-24T12:44:18+08:00
draft: true
---

<!--more-->

## 直接上代码
```java
@Getter
public class ResultVO {

    private String msg;
    private Integer code;
    private Object data;

    private ResultVO(Status status, Object data) {
        this.msg = status.msg;
        this.code = status.code;
        this.data = data;
    }


    private ResultVO(String msg, Integer code, Object data) {
        this.msg = msg;
        this.code = code;
        this.data = data;
    }

    public ResultVO() {
    }

    @Transient
    public Boolean isOk() {
        return Status.SUCCESS.code.equals(this.code);
    }

    private enum Status {
        SUCCESS("success", 200),
        FAIL("fail", 500),
        ;
        String msg;
        Integer code;

        Status(String msg, Integer code) {
            this.msg = msg;
            this.code = code;
        }
    }

    public static ResultVO ok() {
        return new ResultVO(Status.SUCCESS, null);
    }

    public static ResultVO ok(Object data) {
        return new ResultVO(Status.SUCCESS, data);
    }
    
    public static ResultVO error(String msg) {
        return new ResultVO(msg, Status.FAIL.code, null);
    }
}

```
