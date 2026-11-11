

```java
 * array and
29 * copying all elements.
30 * @param a the array to grow
31 * @param newLength the new length
32 * @return a larger array that contains all elements of a. However, the returned
33 * array has type Object[], not the same type as a
34 */
35 public static Object[] badCopyOf(Object[] a, int newLength) // not useful
36 {
37     var newArray = new Object[newLength];
38     System.arraycopy(a, 0, newArray, 0, Math.min(a.length, newLength));
39     return newArray;
40 }
41
42 /**
43 * This method grows an array by allocating a new array of the same type and
44 * copying all elements.
45 * @param a the array to grow. This can be an object array or a primitive
46 * type array
47 * @return a larger array that contains all elements of a.
48 */
49 public static Object goodCopyOf(Object a, int newLength)
50 {
51     Class cl = a.getClass();
52     if (!cl.isArray()) return null;
53     Class componentType = cl.getComponentType();
54     int length = Array.getLength(a);
55     Object newArray = Array.newInstance(componentType, newLength);
56     System.arraycopy(a, 0, newArray, 0, Math.min(length, newLength));
57     return newArray;
58 }
59 }
```

## java.lang.Class 1.1

- `boolean isArray()`
  如果此对象表示数组类型，则返回 true。

- `Class<?> getComponentType()`
  `Class<?> componentType()` 12
  如果此对象表示数组类型，则返回描述组件类型的 `Class`，否则返回 null。

- `Class<?> arrayType()` 12
  返回描述数组类型的 `Class`，该数组类型的组件类型由当前对象表示。

## java.lang.reflect.Array 1.1

- `static Object get(Object array, int index)`

- `static xxx getXxx(Object array, int index)`
  （`xxx` 是基本类型 boolean、byte、char、double、float、int、long 或 short 之一。）这些方法返回给定数组中存储在给定索引处的值。

- `static void set(Object array, int index, Object newValue)`

- `static void setXxx(Object array, int index, xxx newValue)`
  （`xxx` 是基本类型 boolean、byte、char、double、float、int、long 或 short 之一。）这些方法将新值存储到给定数组的给定索引处。

- `static int getLength(Object array)`
  返回给定数组的长度。

- `static Object newInstance(Class componentType, int length)`

- `static Object newInstance(Class componentType, int[] lengths)`
  返回具有给定组件类型和给定维度的新数组。

## 5.9.7 调用任意方法和构造函数

在 C 和 C++ 中，可以通过函数指针执行任意函数。表面上看，Java 没有方法指针——也就是没有把方法的位置传给另一个方法、以便第二个方法稍后调用它的方式。事实上，Java 的设计者曾表示，方法指针危险且容易出错，而 Java 接口和 lambda 表达式（将在下一章讨论）是更好的解决方案。不过，反射机制允许你调用任意方法。

回想一下，可以使用 `Field` 类的 get 方法查看对象的字段。类似地，`Method` 类有一个 invoke 方法，可用于调用当前 `Method` 对象中包装的方法。invoke 方法的签名是

```java
Object invoke(Object obj, Object... args)
```

第一个参数是隐式参数，其余对象提供显式参数。

对于静态方法，第一个参数会被忽略——可以将其设为 `null`。

例如，如果 `m1` 表示 `Employee` 类的 getName 方法，以下代码展示了如何调用它：

```java
String n = (String) m1.invoke(harry);
```

如果返回类型是基本类型，invoke 方法将改为返回包装类型。例如，假设 `m2` 表示 `Employee` 类的 getSalary 方法。那么，返回的对象实际上是 `Double`，必须进行相应的强制类型转换。使用自动拆箱将其转换为 double：

```java
double s = (Double) m2.invoke(harry);
```

如何获得 Method 对象？当然，可以调用 getDeclaredMethods，并在返回的 Method 对象数组中搜索，直到找到所需的方法。或者，可以调用 Class 类的 getMethod 方法。这类似于 getField 方法：它接收包含字段名的字符串并返回 Field 对象。但是，可能有多个方法具有相同名称，因此需要小心获取正确的方法。为此，还必须提供所需方法的参数类型。getMethod 的签名是

```java
Method getMethod(String name, Class... parameterTypes)
```

例如，下面展示了如何获取 Employee 类的 getName 和 raiseSalary 方法的“方法指针”：

```java
Method m1 = Employee.class.getMethod("getName");
Method m2 = Employee.class.getMethod("raiseSalary", double.class);
```

调用任意构造函数时可采用类似方法。将构造函数的参数类型提供给 class.getConstructor 方法，并将参数值提供给 Constructor.newInstance 方法：

```java
Class cl = Random.class; // or any other class with a constructor that
                // accepts a long parameter
Constructor cons = cl.getConstructor(long.class);
Object obj = cons.newInstance(42L);
```

> **注意：**
>
> Method 和 Constructor 类继承自 Executable 类。从 Java 17 开始，Executable 类是密封类，仅允许 Method 和 Constructor 作为子类。

现在你已经了解了使用 Method 对象的规则，让我们把它们付诸实践。代码清单 5.19 是一个程序，用于打印数学函数（如 `Math.sqrt` 或 `Math.sin`）的值表。输出如下所示：

```
public static native double java.lang.Math.sqrt(double)
1.0000  |  1.0000
2.0000  |  1.4142
3.0000  |  1.7321
4.0000  |  2.0000
5.0000  |  2.2361
6.0000  |  2.4495
7.0000  |  2.6458
8.0000  |  2.8284
9.0000  |  3.0000
10.0000 |  3.1623
```

当然，打印表格的代码与被制表的实际函数无关。

```java
double dx = (to - from) / (n - 1);
for (double x = from; x <= to; x += dx)
{
    double y = (Double) f.invoke(null, x);
    System.out.printf("%10.4f | %10.4f%n", x, y);
}
```

这里，f 是 Method 类型的对象。invoke 的第一个参数为 null，因为我们调用的是静态方法。

要对 `Math.sqrt` 函数制表，我们将 $f$ 设置为

```java
Math.class.getMethod("sqrt", double.class)
```

这就是 `Math` 类中名称为 `sqrt`、且只有一个 `double` 类型参数的方法。

[代码清单 5.19](#) 展示了通用制表程序的完整代码以及几次测试运行。

### **代码清单 5.19** methods/MethodTableTest.java

```java
package methods;

import java.lang.reflect.*;

/**
 * This program shows how to invoke methods through reflection.
 * @version 1.2 2012-05-04
 * @author Cay Horstmann
 */
public class MethodTableTest
{
   public static void main(String[] args)
         throws ReflectiveOperationException
   {
      // get method pointers to the square and sqrt methods
      Method square =
         MethodTableTest.class.getMethod("square", double.class);
      Method sqrt = Math.class.getMethod("sqrt", double.class);

      // print tables of x- and y-values
      printTable(1, 10, 10, square);
      printTable(1, 10, 10, sqrt);
   }
}
```

## 2024 年度业绩快报

报告期内，公司实现营业总收入 1,234.56 亿元，同比增长 12.34%；实现归属于上市公司股东的净利润 89.01 亿元，同比增长 8.76%。

截至 2024 年 12 月 31 日，公司总资产 2,345.67 亿元，较期初增长 6.45%；归属于上市公司股东的所有者权益 567.89 亿元，较期初增长 5.23%。

| 项目 | 2024年 | 2023年 | 变动幅度 |
| --- | --- | --- | --- |
| 营业总收入（亿元） | 1,234.56 | 1,098.76 | 12.34% |
| 归属于上市公司股东的净利润（亿元） | 89.01 | 81.82 | 8.76% |
| 基本每股收益（元/股） | 1.25 | 1.15 | 8.70% |
| 加权平均净资产收益率 | 16.52% | 15.87% | 0.65个百分点 |

注：本公告所载 2024 年度主要财务数据为初步核算数据，未经会计师事务所审计，最终数据以公司 2024 年年度报告为准。

> 敬请广大投资者注意投资风险。

特此公告。

