### CodeThink - CodeGuide
# Maven `pom.xml`

### 显式指定源代码和编译版本

你需要在项目 `pom.xml` 中显示指定源代码和编译版本，如下所示：

```xml
<properties>
    <maven.compiler.source>8</maven.compiler.source>
    <maven.compiler.target>8</maven.compiler.target>
</properties>
```

而不是在项目 `profile` 中设置。

### 不要规定本地 `deploy` 目录

请不要在项目 `pom.xml` 中写形如下面的语句：

```xml
<distributionManagement>
    <repository>
        <id>maven-release</id>
        <url>file://xxx</url>
    </repository>
</distributionManagement>
```