### CodeThink - CodeGuide
# Java 代码规范

## 类

### 类名

类名应该使用大驼峰命名法，不使用 `$` 和 `_`。例如，`XiaoMingCode`、`XiaoMing`。

### 定义

类的继承和实现的父类或接口，和类名一起，一共占三行。例如：

```java
package cn.codethink.util;

/**
 * 字符串工具类
 * 
 * @author Chuanwise 
 */
public class Strings 
        extends StaticUtilities {

    // ...
}
```

## 方法

### 为 `public` 方法添加 `javadoc` 注释

访问器和修改器一般由 `lombok` 生成，无需添加注释。主函数也可以不加，其他的 `public` 方法需要添加注释。

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
        // ...
    }
}
```

方法抛出的必检异常必须在 `javadoc` 注释中使用 `@throws` 声明，非必检异常则可以自由决定是否声明。

### 方法开头断言参数

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
        Preconditions.namedArgumentNonNull(string, "string");                               // 断言参数合法性
        Preconditions.argument(count >= 0, "count must be bigger than or equals to 0!");    // 断言参数合法性
        
        if (count == 0 || string.length() == 0) {
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

## 语句

### 语句块使用 `{}`

当 `if` 等语句的某一分支只有一个语句时，也带 `{}`，例如：

```java
class ClassName {
    /** ... */
    int max(int left, int right) {
        if (left > right) {
            return left;                // 虽然只有一个语句，但也加上了 {}
        } else {
            return right;               // 虽然只有一个语句，但也加上了 {}
        }
    }
}
```

### 语句块左花括号前添加一个空格

```java
class ClassName {       // ClassName 后的语句块左花括号 { 前插入了一个空格
}
```

### 语句块左花括号放在行尾，不另起新行

```java
class ClassName {
    /** ... */
    int max(int left, int right) {
        if (left > right) {             // 大括号并没有另起新行
            return left;
        } else {                        // 大括号并没有另起新行
            return right;
        }
    }
}
```

### 语句块右花括号另起新行

```java
class ClassName {
    /** ... */
    int max(int left, int right) {
        if (left > right) {
            return left;
        } else {                    // 右花括号另起新行
            return right;
        }                           // 右花括号另起新行
    }                               // 右花括号另起新行
}                                   // 右花括号另起新行
```

### `else` 等语句不另起新行

```java
class ClassName {
    /** ... */
    int max(int left, int right) {
        if (left > right) {
            return left;
        } else {                                        // else 没有另起新行
            return right;
        }

        try {
            final Object object = null;
            System.out.println(object.toString());
        } catch (NullPointerException ignored) {        // catch 没有另起新行
        } finally {                                     // finally 没有另起新行
            System.out.println("Hey!");
        }
    }
}
```

### 关键字和括号中间插入空格

例如 `if`、`while`，都是关键字且后面跟括号，则其后需要添加一个空格。

```java
class ClassName {
    /** ... */
    int sum(int[] ints) {
        Preconditions.namedArgumentNonNull(ints, "ints");

        int sum = 0;
        for (int i = 0; i < ints.length; i ++) {            // for 是关键字，和后面的括号相距一个空格
            sum += ints[i];
        }
        return sum;
    }
}
```

### 标识符和括号之间不用空格

例如方法定义时，方法名和后面的括号之间不用空格；方法调用时也是。

```java
class ClassName {
    /** ... */
    int sum(int[] ints) {                                   // 定义方法 sum，方法名和后面的括号之间没有空格
        Preconditions.namedArgumentNonNull(ints, "ints");   // 调用方法 Preconditions.namedArgumentNonNull，方法名和后面的括号之间没有空格

        int sum = 0;
        for (int i = 0; i < ints.length; i ++) {
            sum += ints[i];
        }
        return sum;
    }

    public static void main(String[] args) {                            // 定义方法 main，方法名和后面的括号之间没有空格
        System.out.println("sum of [1, 2, 3] is " + sum({1, 2, 3}));    // 调用方法 System.out.println 和 sum，方法名和后面的括号之间没有空格
    }
}
```
