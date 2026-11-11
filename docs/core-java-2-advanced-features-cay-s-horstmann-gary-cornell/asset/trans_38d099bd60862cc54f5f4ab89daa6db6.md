

```java
yellowButton = new JButton("Yellow");
blueButton = new JButton("Blue");
redButton = new JButton("Red");

panel.add(yellowButton);
panel.add(blueButton);
panel.add(redButton);

ActionListenerInstaller.processAnnotations(this);

}

@ActionListenerFor(source = "yellowButton")
public void yellowBackground()
{
    panel.setBackground(Color.YELLOW);
}

@ActionListenerFor(source = "blueButton")
public void blueBackground()
{
    panel.setBackground(Color.BLUE);
}

@ActionListenerFor(source = "redButton")
public void redBackground()
{
    panel.setBackground(Color.RED);
}
```

### **清单 8.11** `runtimeAnnotations/ActionListenerFor.java`

```java
package runtimeAnnotations;

import java.lang.annotation.*;

/**
 * @version 1.00 2004-08-17
 * @author Cay Horstmann
 */

@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface ActionListenerFor
{
    String source();
}
```

**`java.lang.reflect.AnnotatedElement` 5.0**

- `boolean isAnnotationPresent(Class<? extends Annotation> annotationType)`  
  如果此项具有给定类型的注解，则返回 true。
- `<T extends Annotation> T getAnnotation(Class<T> annotationType)`  
  获取给定类型的注解；如果此项没有此类注解，则返回 `null`。
- `<T extends Annotation> T[] getAnnotationsByType(Class<T> annotationType)`⁸  
  获取可重复注解类型的所有注解（参见第 8.5.3 节“元注解”，第 472 页），或返回长度为 0 的数组。
- `Annotation[] getAnnotations()`  
  获取此项存在的所有注解，包括继承的注解。如果不存在任何注解，则返回长度为 0 的数组。
- `Annotation[] getDeclaredAnnotations()`  
  获取此项声明的所有注解，不包括继承的注解。如果不存在任何注解，则返回长度为 0 的数组。

## 8.4 注解语法

在接下来的几节中，我们将介绍你需要了解的关于注解语法的全部内容。

### 8.4.1 注解接口

注解由注解接口定义：

```
modifiers @interface AnnotationName
{
   elementDeclaration1
   elementDeclaration2
   . . .
}
```

每个元素声明的形式为

```
type elementName();
```

或

```
type elementName() default value;
```

例如，下面的注解有两个元素：assignedTo 和 severity：

```java
public @interface BugReport
{
    String assignedTo() default "[none]";
    int severity();
}
```

所有注解接口都隐式扩展 `java.lang.annotation.Annotation` 接口。该接口是普通接口，*不是*注解接口。有关该接口提供的方法，请参阅本节末尾的 API 说明。你不能扩展注解接口。换句话说，所有注解接口都直接扩展 `java.lang.annotation.Annotation`。你永远不需要提供实现注解接口的类。

注解接口的方法没有参数，也没有 throws 子句。它们不能是默认方法或静态方法，也不能有类型参数。

注解元素的类型是下列之一：

- 基本类型（`int`、`short`、`long`、`byte`、`char`、`double`、`float` 或 `boolean`）
- `String`
- Class（带有可选类型参数，例如 `Class<? extends MyClass>`）
- 枚举类型
- 注解类型
- 上述类型的数组（数组的数组不是合法的元素类型）

以下是合法元素声明的示例：

```java
public @interface BugReport
{
    enum Status { UNCONFIRMED, CONFIRMED, FIXED, NOTABUG };
    boolean showStopper() default false;
    String assignedTo() default "[none]";
    Class<?> testCase() default Void.class;
    Status status() default Status.UNCONFIRMED;
    Reference ref() default @Reference(); // an annotation type
    String[] reportedBy();
}
```

| `java.lang.annotation.Annotation` 5.0 |
|---|
| • `Class<? extends Annotation> annotationType()`<br>返回表示此注解对象的注解接口的 Class 对象。注意，对注解对象调用 `getClass` 会返回实际类，而不是接口。 |
| • `boolean equals(Object other)`<br>如果 other 是实现与此注解对象相同注解接口的对象，并且此对象和 other 的所有元素都相等，则返回 true。<br><br>• `int hashCode()`<br>返回与 equals 方法兼容的哈希码，该哈希码由注解接口名称和元素值导出。<br><br>• `String toString()`<br>返回包含注解接口名称和元素值的字符串表示形式；例如，`@BugReport(assignedTo=[none], severity=0)`。 |

### 8.4.2 注解

每个注解的格式为

```
@AnnotationName(elementName1=value1, elementName2=value2, . . .)
```

例如，

```
@BugReport(assignedTo="Harry", severity=10)
```

元素名称的顺序无关紧要。注解

```
@BugReport(severity=10, assignedTo="Harry")
```

与前一个注解相同。

如果未指定元素值，则使用声明中的默认值。例如，考虑注解

```
@BugReport(severity=10)
```

assignedTo 元素的值是字符串 "[none]"。

> **警告：** 默认值不会与注解一起存储；相反，它们是动态计算的。例如，如果将 assignedTo 元素的默认值改为 "" 并重新编译 BugReport 接口，则注解 `@BugReport(severity=10)` 将使用新的默认值，即使在默认值更改之前已经编译的类文件中也是如此。

两个特殊快捷方式可以简化注解。

如果未指定任何元素（要么因为注解没有任何元素，要么因为所有元素都使用默认值），则不需要使用括号。例如，

```java
@BugReport
```

等同于

```java
@BugReport(assignedTo="[none]", severity=0)
```

这种注解称为*标记注解*。

另一个快捷方式是*单值注解*。如果某个元素具有特殊名称 `value`，并且未指定其他元素，则可以省略元素名称和 `=` 符号。例如，如果我们把上一节的 ActionListenerFor 注解接口定义为

```java
public @interface ActionListenerFor
{
    String value();
}
```

那么这些注解可以写成

```java
@ActionListenerFor("yellowButton")
```

而不是

```java
@ActionListenerFor(value="yellowButton")
```

一个项可以有多个注解：

```java
@Test
@BugReport(showStopper=true, reportedBy="Joe")
public void checkRandomInsertions()
```

如果注解的作者将其声明为可重复的，则可以多次重复同一个注解：

```java
@BugReport(showStopper=true, reportedBy="Joe")
@BugReport(reportedBy={"Harry", "Carl"})
public void checkRandomInsertions()
```

> **注意：** 由于注解由编译器求值，所有元素值都必须是编译时常量。例如，

```java
@BugReport(showStopper=true, assignedTo="Harry", testCase=MyTestCase.class,
           status=BugReport.Status.CONFIRMED, ...)
```

> **警告：** 注解元素永远不能设置为 `null`。甚至不允许默认值为 `null`。这在实践中可能相当不方便。你需要寻找其他默认值，例如 `""` 或 `Void.class`。

如果元素值是数组，则将其值括在花括号中：

```
@BugReport(. . . , reportedBy={"Harry", "Carl"})
```

如果元素只有一个值，则可以省略花括号：

```
@BugReport(. . . , reportedBy="Joe") // OK, same as {"Joe"}
```

由于注解元素可以是另一个注解，因此可以构建任意复杂的注解。例如，

```
@BugReport(ref=@Reference(id="3352627"), . . .)
```

> **注意：** 在注解中引入循环依赖是错误的。例如，`BugReport` 有一个注解类型为 `Reference` 的元素，因此 `Reference` 不能有一个类型为 `BugReport` 的元素。

### 8.4.3 注解声明

注解可以出现在许多地方。它们分为两类：*声明和类型使用*。声明注解可以出现在以下声明处：

- 包
- 类（包括 `enum`）
- 接口（包括注解接口）
- 方法
- 构造器
- 实例字段（包括 `enum` 常量）
- 局部变量
- 参数变量
- 类型参数

对于类和接口，将注解放在 `class` 或 `interface` 关键字之前：

```
@Entity public class User { . . . }
```

对于变量，将它们放在类型之前：

```java
@SuppressWarnings("unchecked") List<User> users = . . . ;
public User getUser(@Param("id") String userid)
```

