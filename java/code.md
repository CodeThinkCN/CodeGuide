### CodeThink - CodeGuide
# Java 代码规范

## 方法

### 方法开头应该断言参数

例如，下面的代码是重复字符串的代码：

```java
package cn.codethink.util;

/**
 * 字符串工具类
 * 
 * @author Chuanwise 
 */
public class Strings 
        extends StaticUtilities {
    
    /**
     * 将一个字符串的内容重复若干次
     * 
     * @param string 字符串
     * @param count 重复次数
     * @return 重复后的字符串
     * @throws IllegalArgumentException string 为 null 或 count < 0
     */
    public static String repeat(String string, int count) {
        Preconditions.namedArgumentNonNull(string, "string");
        Preconditions.argument(count >= 0, "count must be bigger than or equals to 0!");
        
        if (count == 0) {
            return string;
        }
        
        final StringBuilder stringBuilder = new StringBuilder(string.length() * count);
        for (int i = 0; i < count; i++) {
            stringBuilder.append(string);
        }
        return stringBuilder.toString();
    }
}
```

方法在开头两行断言了参数的情况，随后执行了相关的操作。