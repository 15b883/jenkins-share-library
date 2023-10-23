## Node.js 项目

在sonar-project.properties中设置sonar.exclusions

例如:

```
sonar.exclusions=test/**,config/db.js
```

## Java项目

不能直接在sonar-project.properties文件中设置sonar.exclusions来排除扫描的文件或目录。

因为SonarQube在扫描Java项目时,不是基于sonar-project.properties文件,而是直接解析Maven构建文件,来获取配置信息。

指定排除规则的正确方式是:

1. 在Maven项目中,通过命令行参数指定排除:

```
mvn sonar:sonar -Dsonar.exclusions=src/test/**,src/main/resources/sql/**
```

2. 对于Maven项目,还可以在pom.xml中指定:

```xml
<properties>
  <sonar.exclusions>src/test/**</sonar.exclusions> 
</properties>

<properties>
  <sonar.coverage.exclusions>
    src/test/**/*,
    **/StringUtil.java
  </sonar.coverage.exclusions>
</properties>
```

综上,Java项目主要是通过Maven的参数来指定sonar.exclusions,不建议直接修改sonar-project.properties文件。

因为SonarQube在扫描时不会读取该文件。