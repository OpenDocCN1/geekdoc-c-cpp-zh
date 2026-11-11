
我们为什么可能需要这种控制？考虑以下代码：

```java
JSONValue v = . . .;
if (v instanceof JSONArray a) . . .
else if (v instanceof JSONNumber n) . . .
else if (v instanceof JSONString s) . . .
else if (v instanceof JSONBoolean b) . . .
else if (v instanceof JSONObject o) . . .
else . . . // Must be JSONNull
```

在这里，控制流意味着我们知道 `JSONValue` 的所有直接子类。这不是一个开放式的层次结构。JSON 标准不会改变；如果它改变了，作为库实现者的我们会添加第七个子类。我们不希望其他任何人乱动这个类层次结构。

在 Java 中，*密封*类控制哪些类可以继承它。密封类在 Java 15 中作为预览特性加入，并在 Java 17 中最终确定。

下面说明如何将 JSONValue 类声明为密封类：

```java
public abstract sealed class JSONValue
    permits JSONArray, JSONNumber, JSONString, JSONBoolean,
JSONObject, JSONNull
{
    . . .
}
```

定义未被允许的子类是错误的：

```java
public class JSONComment extends JSONValue { . . . } // Error
```

这也没什么问题，因为 JSON 不允许注释。因此，密封类允许对领域约束进行准确建模。

密封类的允许子类必须可访问。它们不能是嵌套在另一个类中的私有类，也不能是来自另一个包的包可见类。

对于 public 的允许子类，规则更严格。它们必须与密封类位于同一个包中。但是，如果你使用模块（见第 II 卷第 9 章），那么它们必须只位于同一个模块中。

![](img/0e7b74ef51a065c077b42cd87b362288_405_0.png)

**注意：**

密封类可以在没有 permits 子句的情况下声明。此时，它的所有直接子类都必须声明在同一个文件中。无法访问该文件的程序员不能形成子类。

一个文件最多只能有一个 public 类，因此这种安排似乎只有在子类不供公众使用时才有用。

不过，正如你将在下一章看到的，你可以使用内部类作为 public 子类。

密封类的一个重要动机是编译时检查。考虑 JSONValue 类的这个方法，它使用带模式匹配的 switch 表达式（Java 17 中的预览特性）：

```java
public String type()
{
    return switch (this)
    {
        case JSONArray j -> "array";
        case JSONNumber j -> "number";
        case JSONString j -> "string";
        case JSONBoolean j -> "boolean";
        case JSONObject j -> "object";
        case JSONNull j -> "null";
        // No default needed here
    };
}
```

编译器可以检查出不需要 `default` 子句，因为 `JSONValue` 的所有直接子类都作为 case 出现。

> **注意：**
>
> 前面的 `type` 方法看起来不太面向对象。让六个类各自提供自己的 `type` 方法、依靠多态而不是 switch，会更符合 OOP 的精神。对于开放式层次结构，这是一种好方法。但当类集合固定时，把所有备选情况放在一个方法中通常更方便。

乍一看，密封类的子类似乎必须是 final。但对于穷尽性检查，我们只需要知道所有直接子类。这些类是否还有更多子类并不是问题。例如，我们可以像图 5.3 所示那样重新组织 JSON 层次结构。

![](img/0e7b74ef51a065c077b42cd87b362288_406_0.png)

**图 5.3** 用于表示 JSON 值的完整类层次结构

在这个层次结构中，`JSONValue` 允许三个子类：

```java
public abstract sealed class JSONValue permits JSONObject,
JSONArray, JSONPrimitive
{
  . . .
}
```

JSONPrimitive 类也是密封的：

```java
public abstract sealed class JSONPrimitive extends JSONValue
    permits JSONString, JSONNumber, JSONBoolean, JSONNull
{
  . . .
}
```

密封类的子类必须指定它是 sealed、final，还是开放以供子类化。在后一种情况下，必须将其声明为 non-sealed。

![](img/0e7b74ef51a065c077b42cd87b362288_407_0.png)

**注意：**

non-sealed 关键字是第一个带连字符的 Java 关键字。这很可能是一种未来趋势。向语言添加关键字总是伴随风险。现有代码可能无法再编译。因此，sealed 是一个“上下文”关键字。你仍然可以声明名为 sealed 的变量或方法：

```java
int sealed = 1; // OK to use contextual keyword as identifier
```

对于带连字符的关键字，人们不必担心这一点。唯一的歧义在于减法：

```java
int non = 0;
non = non-sealed; // Subtraction, not keyword
```

```java
import java.util.*;

sealed interface JSONValue permits JSONArray, JSONObject, JSONPrimitive
{
    public default String type()
    {
        if (this instanceof JSONArray) return "array";
        else if (this instanceof JSONObject) return "object";
        else if (this instanceof JSONNumber) return "number";
        else if (this instanceof JSONString) return "string";
        else if (this instanceof JSONBoolean) return "boolean";
        else return "null";
    }
}

final class JSONArray extends ArrayList<JSONValue> implements
JSONValue {}

final class JSONObject extends HashMap<String, JSONValue>
implements JSONValue
{
    public String toString()
    {
        StringBuilder result = new StringBuilder();
        result.append("{");
        for (Map.Entry<String, JSONValue> entry : entrySet())
        {
            if (result.length() > 1) result.append(",");
            result.append("\"");
            result.append(entry.getKey());
            result.append("\": ");
            result.append(entry.getValue());
        }
        result.append(" }");
        return result.toString();
    }
}
```

```java
sealed interface JSONPrimitive extends JSONValue
        permits JSONNumber, JSONString, JSONBoolean, JSONNull
{
}

final record JSONNumber(double value) implements JSONPrimitive
{
    public String toString() { return "" + value; }
}

final record JSONString(String value) implements JSONPrimitive
{
    public String toString() { return "\"" +
value.translateEscapes() + "\""; }
}

enum JSONBoolean implements JSONPrimitive
{
    FALSE, TRUE;
    public String toString() { return
super.toString().toLowerCase(); }
}

enum JSONNull implements JSONPrimitive
{
    INSTANCE;
    public String toString() { return "null"; }
}

public class SealedTest
{
    public static void main(String[] args)
    {
        JSONObject obj = new JSONObject();
        obj.put("name", new JSONString("Harry"));
        obj.put("salary", new JSONNumber(90000));
        obj.put("married", JSONBoolean.FALSE);
        JSONArray arr = new JSONArray();
        arr.add(new JSONNumber(13));
```

信息被虚拟机用来选择要执行的正确方法。

然而，你也可以通过使用一个特殊的 Java 类来访问这些信息。保存这些信息的类叫作 `Class`，这个名字有点令人困惑。`Object` 类中的 `getClass()` 方法返回一个 `Class` 类型的实例。

```java
Employee e; . . .
Class cl = e.getClass();
```

正如 `Employee` 对象描述某个特定员工的属性一样，`Class` 对象描述某个特定类的属性。`Class` 最常用的方法大概是 `getName`。它返回类的名称。例如，下面的语句

```java
System.out.println(e.getClass().getName() + " " + e.getName());
```

会打印

```
Employee Harry Hacker
```

如果 e 是员工，或者

```
Manager Harry Hacker
```

如果 e 是经理。

如果类位于某个包中，则包名是类名的一部分：

```java
var generator = new Random();
Class cl = generator.getClass();
String name = cl.getName(); // name is set to
"java.util.Random"
```
