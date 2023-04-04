**`CodeThink` - `CodeGuide` - `Java`**
# Java 代码规范

## 包

### 包名使用全小写

类名应该使用全小写，不使用 `$` 和 `_`。例如，`cn.codethink.xiaoming`、`cn.chuanwise.lexicons`。

## 类

### 类名

#### 使用大驼峰命名法

类名应该使用大驼峰命名法，不使用 `$` 和 `_`。例如，`Script`、`PluginEnablingContext`。

#### 抽象类添加 `Abstract` 前缀

当类是抽象类时，类名以 `Abstract` 开头。例如：

```java
public abstract class AbstractList<T>
    implements List<T> {
}
```

### 定义

类的继承和实现的父类或接口，和类名一起，一共占三行。例如：

```java
public abstract class SomeClass
    extends SuperClass
    implements SomeInterfaces {
}
```

## 方法

### 方法名

#### 使用小驼峰命名法

方法名应该使用小驼峰命名法，不使用 `$` 和 `_`。例如，`isEmpty`，`nonEmpty`。

### 为 `public` 方法添加 `javadoc` 注释

访问器和修改器一般由 `lombok` 生成，无需添加注释。主函数也可以不加，其他的 `public` 方法需要添加注释。

```java
package cn.codethink.util;

/**
 * 字符串工具类
 * 
 * @author Chuanwise 
 */
public class Strings {
    
    /**
     * 将一个字符串的内容重复若干次
     * 
     * @param string 字符串
     * @param count  重复次数
     * @return 重复后的字符串
     */
    public static String repeat(String string, int count) {
        // ...
    }
}
```

方法抛出的必检异常必须在 `javadoc` 注释中使用 `@throws` 声明。

### 方法开头断言参数

例如，下面的代码是重复字符串的代码：

```java
package cn.codethink.util;

/**
 * 字符串工具类
 * 
 * @author Chuanwise 
 */
public class Strings {
    
    /**
     * 将一个字符串的内容重复若干次
     * 
     * @param string 字符串
     * @param count 重复次数
     * @return 重复后的字符串
     * @throws IllegalArgumentException string 为 null 或 count < 0
     */
    public static String repeat(String string, int count) {
        Preconditions.objectNonNull(string, "string");
        Preconditions.argument(count >= 0, "count must be bigger than or equals to 0!");
        
        if (count == 0 || string.length() == 0) {
            return "";
        }
        if (count == 1) {
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
int max(int left, int right) {
    if (left > right) {
        return left;                // 虽然只有一个语句，但也加上了 {}
    } else {
        return right;               // 虽然只有一个语句，但也加上了 {}
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
int max(int left, int right) {
    if (left > right) { // 大括号并没有另起新行
        return left;
    } else {            // 大括号并没有另起新行
        return right;
    }
}
```

### 语句块右花括号另起新行

```java
int max(int left, int right) {
    if (left > right) {
        return left;
    } else {            // 右花括号另起新行
        return right;
    }                   // 右花括号另起新行
}                       // 右花括号另起新行
```

### `else` 等语句不另起新行

```java
if (left > right) {
    return left;
} else {                                    // else 没有另起新行
    return right;
}

try {
    final Object object = null;
    System.out.println(object.toString());
} catch (NullPointerException ignored) {    // catch 没有另起新行
} finally {                                 // finally 没有另起新行
    System.out.println("Hey!");
}
```

### 不处理异常时，异常名为 `ignored`

```java
try {
    // 逻辑上不可能抛出 NeverThrownException 的一段代码
    // 但是语法上 NeverThrownException 是必检异常必须捕获
} catch (NeverThrownException ignored) {            // 异常名为 ignored
}
```

### 关键字和括号中间插入空格

例如 `if`、`while`，都是关键字且后面跟括号，则其后需要添加一个空格。

```java
int sum(int[] ints) {
    Preconditions.objectNonNull(ints, "ints");

    int sum = 0;
    for (int i = 0; i < ints.length; i ++) {            // for 是关键字，和后面的括号相距一个空格
        sum += ints[i];
    }
    return sum;
}
```

### 标识符和括号之间不用空格

例如方法定义时，方法名和后面的括号之间不用空格；方法调用时也是。

```java
class Main {
    /** ... */
    int sum(int[] ints) {                            // 定义方法 sum，方法名和后面的括号之间没有空格
        Preconditions.objectNonNull(ints, "ints");   // 调用方法 Preconditions.objectNonNull，方法名和后面的括号之间没有空格

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

### 使用 `@SuppressWarnings(...)` 忽略不必要的警告

特别是泛型转换等操作上。如你确定此处不会出现异常，请用 `@SuppressWarnings(...)` 忽略不必要的警告。

### 遵照接口规范

按照接口方法的语义实现接口方法。例如，`List<T>` 有方法 `int size()`，逻辑上它不可能返回负值，因此实现时也不应该返回负值。