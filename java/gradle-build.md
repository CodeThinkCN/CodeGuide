# Gradle - `build.gradle`

## 多模块项目

### 在父 `build.gradle` 中声明版本等信息

例如，在父 `build.gradle` 中声明：

```gradle
allprojects {
    group 'cn.codethink'
    version '1.0-SNAPSHOT'
}
```

随后在子 `build.gradle` 中则无需重复声明。