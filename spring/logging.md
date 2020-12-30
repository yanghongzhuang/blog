# SpringBoot Logging


> application.yml
```yml
logging:
  level:
    root: info
  # 文件路径
  file.name: logs/server.log
  #file.path: log
  # 滚动日志
  logback.rollingpolicy:
    file-name-pattern: ${LOG_FILE}.%d{yyyy-MM-dd}.%i.gz
    max-file-size: 10MB
    total-size-cap: 10GB
    max-history: 7

```


### reference:
- https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-logging