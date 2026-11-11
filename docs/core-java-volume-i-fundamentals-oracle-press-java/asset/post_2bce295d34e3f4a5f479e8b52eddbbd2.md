
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
  returns true if this object represents an array type.

- `Class<?> getComponentType()`
  `Class<?> componentType()` 12
  returns the `Class` describing the component type if this object represents an array type, or null otherwise.

- `Class<?> arrayType()` 12
  returns the `Class` describing the array type whose component type is represented by this object.

## java.lang.reflect.Array 1.1

- `static Object get(Object array, int index)`

- `static xxx getXxx(Object array, int index)`
  (`xxx` is one of the primitive types boolean, byte, char, double, float, int, long, or short.) These methods return the value of the given array that is stored at the given index.

- `static void set(Object array, int index, Object newValue)`

- `static void setXxx(Object array, int index, xxx newValue)`
  (`xxx` is one of the primitive types boolean, byte, char, double, float, int, long, or short.) These methods store a new value into the given array at the given index.

- `static int getLength(Object array)`
  returns the length of the given array.

- `static Object newInstance(Class componentType, int length)`

- `static Object newInstance(Class componentType, int[] lengths)`
  returns a new array of the given component type with the given dimensions.

## 5.9.7 Invoking Arbitrary Methods and Constructors

In C and C++, you can execute an arbitrary function through a function pointer. On the surface, Java does not have method pointers—that is, ways of giving the location of a method to another method, so that the second method can invoke it later. In fact, the designers of Java have said that method pointers are dangerous and error-prone, and that Java interfaces and lambda expressions (discussed in the next chapter) are a superior solution. However, the reflection mechanism allows you to call arbitrary methods.

Recall that you can inspect a field of an object with the get method of the `Field` class. Similarly, the `Method` class has an invoke method that lets you call the method that is wrapped in the current `Method` object. The signature for the invoke method is

```java
Object invoke(Object obj, Object... args)
```

The first parameter is the implicit parameter, and the remaining objects provide the explicit parameters.

For a static method, the first parameter is ignored—you can set it to `null`.

For example, if `m1` represents the getName method of the `Employee` class, the following code shows how you can call it:

```java
String n = (String) m1.invoke(harry);
```

If the return type is a primitive type, the invoke method will return the wrapper type instead. For example, suppose that `m2` represents the getSalary method of the `Employee` class. Then, the returned object is actually a `Double`, and you must cast it accordingly. Use automatic unboxing to turn it into a double:

```java
double s = (Double) m2.invoke(harry);
```

How do you obtain a Method object? You can, of course, call getDeclaredMethods and search through the returned array of Method objects until you find the method you want. Or, you can call the getMethod method of the class Class. This is similar to the getField method that takes a string with the field name and returns a Field object. However, there may be several methods with the same name, so you need to be careful that you get the right one. For that reason, you must also supply the parameter types of the desired method. The signature of getMethod is

```java
Method getMethod(String name, Class... parameterTypes)
```

For example, here is how you can get method pointers to the getName and raiseSalary methods of the Employee class:

```java
Method m1 = Employee.class.getMethod("getName");
Method m2 = Employee.class.getMethod("raiseSalary", double.class);
```

Use a similar approach for invoking arbitrary constructors. Supply the constructor's parameter types to the class.getConstructor method, and supply the parameter values to the Constructor.newInstance method:

```java
Class cl = Random.class; // or any other class with a constructor that
                // accepts a long parameter
Constructor cons = cl.getConstructor(long.class);
Object obj = cons.newInstance(42L);
```

> **NOTE:**
>
> The Method and Constructor classes extend the Executable class. As of Java 17, the Executable class is sealed, permitting only Method and Constructor as subclasses.

Now that you have seen the rules for using Method objects, let’s put them to work. Listing 5.19 is a program that prints a table of values for a mathematical function such as `Math.sqrt` or `Math.sin`. The printout looks like this:

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

The code for printing a table is, of course, independent of the actual function that is being tabulated.

```java
double dx = (to - from) / (n - 1);
for (double x = from; x <= to; x += dx)
{
    double y = (Double) f.invoke(null, x);
    System.out.printf("%10.4f | %10.4f%n", x, y);
}
```

Here, f is an object of type Method. The first parameter of invoke is null because we are calling a static method.

To tabulate the `Math.sqrt` function, we set $f$ to

```java
Math.class.getMethod("sqrt", double.class)
```

That is the method of the `Math` class that has the name `sqrt` and a single parameter of type `double`.

[Listing 5.19](#) shows the complete code of the generic tabulator and a couple of test runs.

### **Listing 5.19** methods/MethodTableTest.java

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
