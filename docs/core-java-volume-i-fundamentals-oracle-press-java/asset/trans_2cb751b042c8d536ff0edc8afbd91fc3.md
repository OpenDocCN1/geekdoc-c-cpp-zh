

未来的库可能会使用*变量句柄*而不是反射来读写字段。`VarHandle` 类似于 `Field`。你可以用它读取或写入特定类的任何实例的特定字段。然而，要获得 `VarHandle`，库代码需要一个 `Lookup` 对象：

```java
public Object getFieldValue(Object obj, String fieldName,
                             Lookup lookup)
        throws NoSuchFieldException, IllegalAccessException
{
    Class<?> cl = obj.getClass();
    Field field = cl.getDeclaredField(fieldName);
    VarHandle handle = MethodHandles.privateLookupIn(cl, lookup)
        .unreflectVarHandle(field);
    return handle.get(obj);
}
```

只要 `Lookup` 对象是在有权访问该字段的模块中生成的，这种方法就可行。该模块中的某个方法只需调用 `MethodHandles.lookup()`，就会生成一个封装了调用方访问权限的对象。通过这种方式，一个模块可以授予另一个模块访问私有成员的权限。实际问题在于，如何以最少的麻烦授予这些权限。

虽然我们仍然可以这样做，但让我们看看一个适用于任何类的泛型 `toString` 方法（参见[代码清单 5.16]）。这个泛型 `toString` 方法使用 `getDeclaredFields` 获取所有实例字段，并使用 setAccessible 便捷方法使所有字段可访问。对于每个字段，它获取名称和值。每个值都通过递归调用 `toString` 转换为字符串。

泛型 `toString` 方法需要处理几个复杂问题。引用循环可能导致无限递归。因此，`ObjectAnalyzer` 会跟踪已经访问过的对象。此外，要查看数组内部，需要使用不同的方法。你将在下一节了解详细信息。

```java
57            }
58        }
59        r += "]";
60        cl = cl.getSuperclass();
61      }
62      while (cl != null);
63
64      return r;
65   }
66 }
```

## java.lang.reflect.AccessibleObject 1.2

- `void setAccessible(boolean flag)`  
  设置或清除此可访问对象的可访问性标志；如果访问被拒绝，则抛出 `IllegalAccessException`。
- `boolean trySetAccessible()`⁹  
  设置此可访问对象的可访问性标志；如果访问被拒绝，则返回 `false`。
- `boolean canAccess(Object obj)`⁹  
  检查调用方能否通过此字段、方法或构造器对象访问 `obj`。对于静态字段或方法，或者对于构造器，请传入 `null`。
- `static void setAccessible(AccessibleObject[] array, boolean flag)`  
  是一个便捷方法，用于为一组对象设置可访问性标志。

## java.lang.Class 1.1

- `Field getField(String name)`
- `Field[] getFields()`  
  获取具有给定名称的公共字段，或获取所有字段的数组。
- `Field getDeclaredField(String name)`
- `Field[] getDeclaredFields()`  
  获取在此类中声明的具有给定名称的字段，或获取所有字段的数组。

## java.lang.reflect.Field 1.1

- `Object get(Object obj)`  
  获取此 Field 对象所描述的字段在对象 obj 中的值。
- `void set(Object obj, Object newValue)`  
  将此 Field 对象所描述的字段在对象 obj 中设置为新值。

## 5.9.6 使用反射编写泛型数组代码

java.lang.reflect 包中的 Array 类允许你动态创建数组。例如，Arrays 类中 copyOf 方法的实现就使用了这一功能。回想一下，这个方法如何用于扩充一个已经满了的数组。

```java
var a = new Employee[100];
. . .
// array is full
a = Arrays.copyOf(a, 2 * a.length);
```

如何编写这样一个泛型方法？`Employee[]` 数组可以转换为 `Object[]` 数组，这很有帮助。听起来很有希望。下面是第一次尝试：

```java
public static Object[] badCopyOf(Object[] a, int newLength) // not useful
{
    var newArray = new Object[newLength];
    System.arraycopy(a, 0, newArray, 0, Math.min(a.length, newLength));
    return newArray;
}
```

然而，实际使用得到的数组时存在一个问题。这段代码返回的数组类型是*对象*数组（`Object[]`），因为我们使用下面这行代码创建了该数组

```java
new Object[newLength]
```

对象数组*不能*强制转换为员工数组（`Employee[]`）。虚拟机将在运行时生成 `ClassCastException`。关键在于，如前所述，Java 数组会记住其元素的类型——也就是创建它的 new 表达式中使用的元素类型。将 `Employee[]` 临时强制转换为 `Object[]` 数组，然后再转换回来是合法的，但一个最初作为 `Object[]` 数组创建的数组永远不能强制转换为 `Employee[]` 数组。要编写这种泛型数组代码，我们需要能够创建一个与原始数组*相同*类型的新数组。为此，我们需要 `java.lang.reflect` 包中 `Array` 类的方法。关键在于 `Array` 类的静态 `newInstance` 方法，它构造一个新数组。你必须向此方法提供元素的类型和所需长度作为参数。

```java
Object newArray = Array.newInstance(componentType, newLength);
```

要实际执行此操作，我们需要获取新数组的长度和组件类型。我们通过调用 `Array.getLength(a)` 获取长度。`Array` 类的静态 `getLength` 方法返回数组的长度。要获取新数组的组件类型：

- 1. 首先，获取 `a` 的类对象。
- 2. 确认它确实是一个数组。
- 3. 使用 `Class` 类的 `getComponentType` 方法（该方法仅为表示数组的类对象定义）来查找数组的正确类型。
- 4. 反过来，对于表示类 `C` 的任何 `Class` 对象，`arrayType` 方法会生成表示 `C[]` 的 `Class` 对象。

为什么 `getLength` 是 `Array` 的方法，而 `getComponentType` 是 `Class` 的方法？我不知道——反射方法的分布有时似乎有点随意。

代码如下：

```java
public static Object goodCopyOf(Object a, int newLength)
{
    Class cl = a.getClass();
    if (!cl.isArray()) return null;
    Class componentType = cl.getComponentType();
    int length = Array.getLength(a);
    Object newArray = Array.newInstance(componentType, newLength);
    System.arraycopy(a, 0, newArray, 0, Math.min(length, newLength));
    return newArray;
}
```

请注意，这个 `copyOf` 方法可用于扩充任何类型的数组，而不仅仅是对象数组。

```java
int[] a = { 1, 2, 3, 4, 5 };
a = (int[]) goodCopyOf(a, 10);
```

为了实现这一点，`goodCopyOf` 的参数被声明为 `Object` 类型，*而不是对象数组*（`Object[]`）。整数数组类型 `int[]` 可以转换为 `Object`，但不能转换为对象数组！

[代码清单 5.18](#) 展示了这两个方法的实际运行。请注意，对 `badCopyOf` 的返回值进行强制转换将抛出异常。

### **代码清单 5.18** arrays/CopyOfTest.java

```java
package arrays;

import java.lang.reflect.*;
import java.util.*;

/**
 * This program demonstrates the use of reflection for
 * manipulating arrays.
 * @version 1.2 2012-05-04
 * @author Cay Horstmann
 */
public class CopyOfTest
{
   public static void main(String[] args)
   {
      int[] a = { 1, 2, 3 };
      a = (int[]) goodCopyOf(a, 10);
      System.out.println(Arrays.toString(a));

      String[] b = { "Tom", "Dick", "Harry" };
      b = (String[]) goodCopyOf(b, 10);
      System.out.println(Arrays.toString(b));

      System.out.println("The following call will generate an exception.");
      b = (String[]) badCopyOf(b, 10);
   }

   /**
    * This method attempts to grow an array by allocating a new
```

