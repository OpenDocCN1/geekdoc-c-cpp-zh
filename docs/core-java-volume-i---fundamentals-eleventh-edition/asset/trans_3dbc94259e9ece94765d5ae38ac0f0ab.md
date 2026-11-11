
这就留下了 `otherObject` 可能属于某个子类的可能性。然而，这种做法可能会让你陷入麻烦。原因如下。Java 语言规范要求 `equals` 方法具有以下性质：

- 1. 它是*自反的*：对于任何非空引用 x，x.equals(x) 应返回 true。
- 2. 它是*对称的*：对于任何引用 x 和 y，当且仅当 y.equals(x) 返回 true 时，x.equals(y) 才应返回 true。
- 3. 它是*传递的*：对于任何引用 x、y 和 z，如果 x.equals(y) 返回 true 且 y.equals(z) 返回 true，那么 x.equals(z) 应返回 true。
- 4. 它是*一致的*：如果 x 和 y 所引用的对象没有发生变化，那么重复调用 x.equals(y) 应返回相同的值。
- 5. 对于任何非空引用 x，x.equals(null) 应返回 false。

这些规则当然合理。你不会希望库实现者在数据结构中定位元素时，还要纠结是调用 x.equals(y) 还是 y.equals(x)。

然而，当参数属于不同类时，对称规则会产生微妙的后果。考虑以下调用

```java
e.equals(m)
```

其中 e 是 Employee 对象，m 是 Manager 对象，二者恰好具有相同的姓名、工资和受雇日期。如果 Employee.equals 使用 instanceof 测试，则该调用返回 true。但这意味着反向调用

```java
m.equals(e)
```

也必须返回 true——对称规则不允许它返回 false 或抛出异常。

这就让 Manager 类陷入困境。它的 equals 方法必须愿意将自身与任何 Employee 比较，而不考虑 Manager 特有的信息！突然之间，instanceof 测试看起来就没那么有吸引力了。

一些作者公开表示 getClass 测试是错误的，因为它违反了替换原则。一个常被引用的例子是 AbstractSet 类中的 equals 方法，它测试两个集合是否具有相同元素。AbstractSet 类有两个具体子类 TreeSet 和 HashSet，它们使用不同的算法定位集合元素。你确实希望能够比较任意两个集合，无论它们如何实现。

然而，集合示例相当特殊。将 AbstractSet.equals 声明为 final 是有道理的，因为没有人应该重新定义集合相等的语义。（该方法实际上并不是 final。这允许子类实现更高效的相等性测试算法。）

在我们看来，有两种不同的情形：

- 如果子类可以有自己的相等性概念，那么对称性要求迫使你使用 `getClass` 测试。
- 如果相等性概念在超类中固定，那么你可以使用 `instanceof` 测试，并允许不同子类的对象彼此相等。

在员工和经理的示例中，当两个对象具有匹配的字段时，我们认为它们相等。如果我们有两个 Manager 对象，姓名、工资和受雇日期相同，但奖金不同，我们希望它们不同。因此，我们使用 `getClass` 测试。

但假设我们使用员工 ID 进行相等性测试。这种相等性概念对所有子类都适用。那么我们就可以使用 `instanceof` 测试，并且应该将 `Employee.equals` 声明为 final。

> **注意。** 标准 Java 库包含 150 多个 equals 方法实现，混杂着使用 `instanceof`、调用 `getClass`、捕获 `ClassCastException`，或者什么都不做。查看 `java.sql.Timestamp` 类的 API 文档，其中实现者有些尴尬地指出，他们已把自己逼入死角。`Timestamp` 类继承自 `java.util.Date`，后者的 equals 方法使用 `instanceof` 测试，因此不可能将 equals 重写为既对称又准确。

以下是编写完美 equals 方法的步骤：

- 1. 将显式参数命名为 `otherObject`——稍后，你需要将它强制转换为另一个变量，该变量应命名为 `other`。
- 2. 测试 this 是否恰好与 `otherObject` 相同：

  ```java
  if (this == otherObject) return true;
  ```

  这条语句只是一种优化。在实践中，这是一种常见情况。检查是否为同一对象比比较字段要廉价得多。
- 3. 测试 `otherObject` 是否为 null，如果是则返回 false。此测试是必需的。

  ```java
  if (otherObject == null) return false;
  ```
- 4. 比较 this 和 `otherObject` 的类。如果 equals 的语义可能在子类中改变，请使用 `getClass` 测试：

  ```java
  if (getClass() != otherObject.getClass()) return false;
  ```

  如果相同的语义适用于*所有*子类，你可以使用 instanceof 测试：

  ```java
  if (!(otherObject instanceof ClassName)) return false;
  ```
- 5. 将 `otherObject` 强制转换为你的类类型的变量：

  ```java
  ClassName other = (ClassName) otherObject;
  ```
- 6. 现在根据你的相等性概念的要求比较字段。对基本类型字段使用 `==`，对对象字段使用 `Objects.equals`。如果所有字段都匹配，则返回 true，否则返回 false。

  ```java
  return field1 == other.field1
      && Objects.equals(field2, other.field2)
      && ...;
  ```

如果在子类中重新定义 equals，请包含对 `super.equals(other)` 的调用。

> **提示：** 如果有数组类型的字段，可以使用静态 `Arrays.equals` 方法检查对应数组元素是否相等。

> **警告：** 下面是实现 equals 方法时的一个常见错误。你能看出问题所在吗？

```java
public class Employee
{
    public boolean equals(Employee other)
    {
        return other != null
            && getClass() == other.getClass()
            && Objects.equals(name, other.name)
            && salary == other.salary
            && Objects.equals(hireDay, other.hireDay);
    }
    . . .
}
```

该方法将显式参数类型声明为 `Employee`。因此，它并没有重写 `Object` 类的 equals 方法，而是定义了一个完全不相关的方法。

你可以通过用 `@Override` 标记打算重写超类方法的方法，来防止此类错误：

```java
@Override public boolean equals(Object other)
```

如果你犯了错误，定义了一个新方法，编译器会报告错误。例如，假设你将以下声明添加到 Employee 类中：

```java
@Override public boolean equals(Employee other)
```

编译器会报告错误，因为此方法没有重写 Object 超类中的任何方法。

- **java.util.Arrays** 1.2
  - `static boolean equals(xxx[] a, xxx[] b)` 5  
    如果数组长度相等且对应位置上的元素相等，则返回 true。数组的组件类型 `xxx` 可以是 `Object`、`int`、`long`、`short`、`char`、`byte`、`boolean`、`float` 或 `double`。
- **java.util.Objects** 7
  - `static boolean equals(Object a, Object b)`  
    如果 `a` 和 `b` 都为 null，则返回 true；如果其中恰好一个为 null，则返回 false；否则返回 `a.equals(b)`。

## 5.2.4 hashCode 方法

散列码是从对象派生出的一个整数。散列码应当是杂乱无章的——如果 `x` 和 `y` 是两个不同的对象，那么 `x.hashCode()` 和 `y.hashCode()` 有很大概率不同。表 5.1 列出了由 `String` 类的 `hashCode` 方法生成的一些散列码示例。

**表 5.1** 由 `hashCode` 方法生成的散列码

| 字符串 | 散列码 |
| --- | --- |
| Hello | 69609650 |
| Harry | 69496448 |
| Hacker | -2141031506 |

`String` 类使用以下算法计算散列码：

```java
int hash = 0;
for (int i = 0; i < length(); i++)
    hash = 31 * hash + charAt(i);
```

hashCode 方法定义在 Object 类中。因此，每个对象都有一个默认散列码。该散列码派生自对象的内存地址。考虑以下示例：

```java
var s = "Ok";
var sb = new StringBuilder(s);
System.out.println(s.hashCode() + " " + sb.hashCode());
var t = new String("Ok");
var tb = new StringBuilder(t);
System.out.println(t.hashCode() + " " + tb.hashCode());
```

表 5.2 显示了结果。

**表 5.2** 字符串和 StringBuilder 的散列码

| 对象 | 散列码 | 对象 | 散列码 |
|---|---:|---|---:|
| s | 2556 | t | 2556 |
| sb | 20526976 | tb | 20527144 |

注意，字符串 s 和 t 具有相同的散列码，因为对于字符串，散列码派生自其内容。字符串构建器 sb 和 tb 具有不同的散列码，因为 StringBuilder 类没有定义 hashCode 方法，而 Object 类中的默认 hashCode 方法从对象的内存地址派生散列码。

如果重新定义 equals 方法，你还需要为用户可能插入散列表的对象重新定义 hashCode 方法。（我们将在第 9 章讨论散列表。）

hashCode 方法应返回一个整数（可以为负数）。只需组合实例字段的散列码，使不同对象的散列码很可能广泛分散。

例如，下面是 Employee 类的 hashCode 方法：

```java
public class Employee
{
    public int hashCode()
    {
        return 7 * name.hashCode()
             + 11 * new Double(salary).hashCode()
             + 13 * hireDay.hashCode();
    }
    . . . .
}
```
