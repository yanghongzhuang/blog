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

> logback-spring.xml
```xml
<!--debug=true开启调试模式 scan=true自动重新加载配置文件 scanPeriod扫描间隔时间，不带单位时默认为单位为毫秒-->
<configuration debug="false" scan="true" scanPeriod="30 seconds">

    <!--xml自上而下解析，变量一定要配置在引用变量之前-->
    <property name="app-name" value="mew-kit"/>
    <property name="log-path" value="log"/>
    <property name="console-encoder-pattern"
              value="%magenta(%date{HH:mm:ss.SSS}) %highlight(%-5level) %green([%.32thread]) %cyan(%logger{36}) : %msg%n"/>
    <property name="file-encoder-pattern" value="%date{HH:mm:ss.SSS} %-5level [%.32thread] %logger{36} : %msg%n"/>

    <!--上下文名称-->
    <contextName>${app-name}</contextName>

    <!--控制台日志-->
    <!--顾名思义，附加在控制台上，或者更准确地说上的System.out或System.err的，前者是默认的目标。
    在用户指定的编码器的帮助下格式化事件。它们被包装在一个缓冲I / O操作的容器中。-->
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
        <!--默认情况下，withJansi属性设置为false。设置withJansi以true激活Jansi库，该库在Windows计算机上提供对ANSI颜色代码的支持。
        在Windows主机上，如果将此属性设置为true，则需要引入"org.fusesource.jansi:jansi（版本号和logback引入的相对应）"。
        请注意，默认情况下，基于Unix的操作系统（例如Linux和Mac OS X）支持ANSI颜色代码。-->
        <withJansi>true</withJansi>
        <!--阈值过滤器 过滤低于指定阈值的事件。对于等于或高于阈值的事件，将在调用其decide()方法时响应NEUTRAL，级别低于阈值的事件将被拒绝。-->
        <filter class="ch.qos.logback.classic.filter.ThresholdFilter">
            <level>INFO</level>
        </filter>
        <encoder>
            <pattern>${console-encoder-pattern}</pattern>
            <!--为了便于解析日志文件，logback可以将用于日志输出的模式插入日志文件的顶部。默认情况下禁用此功能。
            可以通过将outputPatternAsHeader属性设置为'true'来启用它-->
            <outputPatternAsHeader>true</outputPatternAsHeader>
        </encoder>
    </appender>

    <!--info日志-->
    <!--具有扩展FileAppender日志文件功能的功能。例如，RollingFileAppender可以登录到名为log.txt的文件，
    一旦满足特定条件，就可以将其记录目标更改为另一个文件。-->
    <appender name="FILE-INFO" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <!--如果为true，则事件将附加到现有文件的末尾。如果append为false，则任何现有文件都会被截断。默认情况下，append选项设置为true。-->
        <append>true</append>
        <!--要写入的文件名。如果该文件不存在，则会创建它。在MS Windows平台上，用户经常忘记转义反斜杠。例如，值c\temp\test.log不太可能正确解释，
        因为'\t'是一个转义序列，解释为单个制表符（\u0009）。正确的值可以被指定为C:/temp/test.log或C:\\temp\\test.log，该文件选项没有默认值。
        如果文件的父目录不存在， FileAppender将自动创建它，包括任何必要但不存在的父目录。-->
        <file>${log-path}/${app-name}-info.log</file>
        <!--默认情况下，每个日志事件都会立即刷新到基础输出流。从某种意义上说，这种默认方法更安全，因为在应用程序未正确关闭附加程序而退出的情况下，
        不会丢失日志记录事件。但是，为了显着提高日志记录吞吐量，可能需要将InstantFlush属性设置为 false。-->
        <immediateFlush>true</immediateFlush>
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
            <!--每天归档-->
            <!--强制性的fileNamePattern属性定义了过渡（存档）日志文件的名称。其值应包括文件名以及适当放置的%d转换说明符。
            所述%d由指定的转换说明可包含日期和时间模式java.text.SimpleDateFormat类。如果省略了日期和时间模式，则采用默
            认模式 yyyy-MM-dd。请注意，除了%d外，还包含%i转换令牌。%i和%d令牌都是必需的。每次当前日志文件在当前时间段结
            束之前达到maxFileSize时，将使用从0开始的递增索引进行归档。-->
            <fileNamePattern>${log-path}/${app-name}-info.%d{yyyy-MM-dd}.%i.gz</fileNamePattern>
            <!--日志文件最大值，满足时进行归档-->
            <maxFileSize>30MB</maxFileSize>
            <!--控制要保留的周期数，以异步方式删除较旧的文件。
            例如，如果指定每月滚动，并将maxHistory设置为6，则将保留6个月的归档文件，并删除6个月以上的文件。
            请注意，由于删除了旧的归档日志文件，因此将适当删除为日志文件归档而创建的所有文件夹。-->
            <maxHistory>30</maxHistory>
            <!--控制所有存档文件的总大小。当超过总大小上限时，最早的档案将被异步删除。
            该totalSizeCap属性要求maxHistory属性设置为好。此外，始终会首先应用“最大历史记录”限制，然后再应用“总大小上限”限制。-->
            <totalSizeCap>10GB</totalSizeCap>
            <!--如果设置为true，则将在附加程序启动时执行归档删除。默认情况下，此属性设置为false。
            通常在过渡期间执行归档删除。但是，某些应用程序的生存时间可能不足以触发翻转。因此，对于这种短暂的应用程序，归档删除可能永远都没有执行的机会。
            通过将cleanHistoryOnStart设置为true，将在附加程序启动时执行归档删除。-->
            <cleanHistoryOnStart>false</cleanHistoryOnStart>
        </rollingPolicy>
        <!--只放行info级别日志-->
        <!--LevelFilter根据精确的级别匹配过滤事件。如果事件的级别等于已配置的级别，则过滤器将接受或拒绝事件，具体取决于onMatch和onMismatch属性的配置。-->
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>info</level>
            <!--匹配时策略，ACCEPT接受-->
            <onMatch>ACCEPT</onMatch>
            <!--不匹配时策略，DENY拒绝-->
            <onMismatch>DENY</onMismatch>
        </filter>
        <encoder>
            <pattern>${file-encoder-pattern}</pattern>
        </encoder>
    </appender>

    <!--error日志-->
    <appender name="FILE-ERROR" class="ch.qos.logback.core.rolling.RollingFileAppender">
        <file>${log-path}/${app-name}-error.log</file>
        <rollingPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedRollingPolicy">
            <fileNamePattern>${log-path}/${app-name}-error.%d{yyyy-MM-dd}.%i.gz</fileNamePattern>
            <maxFileSize>30MB</maxFileSize>
            <maxHistory>30</maxHistory>
            <totalSizeCap>10GB</totalSizeCap>
        </rollingPolicy>
        <encoder>
            <pattern>${file-encoder-pattern}</pattern>
        </encoder>
        <filter class="ch.qos.logback.classic.filter.LevelFilter">
            <level>error</level>
            <onMatch>ACCEPT</onMatch>
            <onMismatch>DENY</onMismatch>
        </filter>
    </appender>

    <root level="DEBUG">
        <appender-ref ref="STDOUT"/>
        <appender-ref ref="FILE-INFO"/>
        <appender-ref ref="FILE-ERROR"/>
    </root>
</configuration>
```

### reference:
- https://my.oschina.net/pipimao/blog/4841544
- https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-logging