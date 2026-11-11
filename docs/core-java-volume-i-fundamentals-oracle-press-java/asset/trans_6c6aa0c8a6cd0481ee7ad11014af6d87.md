
`hashCode` 方法应返回一个整数（可以是负数）。只需将各实例字段的哈希码组合起来，使不同对象的哈希码尽可能广泛分散。

例如，下面是 `Employee` 类的 `hashCode` 方法：

```java
public class Employee
{
   public int hashCode()
   {
      return 7 * name.hashCode()
         + 11 * Double.valueOf(salary).hashCode()
         + 13 * hireDay.hashCode();
   }
   . . .
}
```

不过，还可以做得更好。首先，使用空值安全的 `Objects.hashCode` 方法。如果其参数为 `null`，则返回 `0`；否则返回对该参数调用 `hashCode` 的结果。另外，使用静态的 `Double.hashCode` 方法以避免创建 `Double` 对象：

```java
public int hashCode()
{
   return 7 * Objects.hashCode(name)
      + 11 * Double.hashCode(salary)
      + 13 * Objects.hashCode(hireDay);
}
```

更好的是，当需要组合多个哈希值时，用所有这些值调用 `Objects.hash`。它会为每个参数调用 `Objects.hashCode` 并组合这些值。这样，`Employee.hashCode` 方法就简化为

```java
public int hashCode()
{
   return Objects.hash(name, salary, hireDay);
}
```

你对 equals 和 hashCode 的定义必须兼容：如果 x.equals(y) 为 true，那么 x.hashCode() 必须返回与 y.hashCode() 相同的值。例如，如果你定义 `Employee.equals` 来比较员工 ID，那么 `hashCode` 方法需要对 ID 进行哈希，而不是对员工姓名或内存地址进行哈希。

**提示：**

如果字段是数组类型，可以使用静态的 `Arrays.hashCode` 方法计算一个由数组各元素的哈希码组成的哈希码。

**注意：**

记录类型会自动提供 `hashCode` 方法，该方法根据字段值的哈希码推导出哈希码。

**警告：**

如果实例变量的可能取值范围很小，你需要获得尽可能多的不同哈希码。考虑对日历日期进行哈希。计算 7 * year + 11 * month + 13 * day 会产生很多冲突。相比之下，31 * 12 * year + 31 * month + day 是一个“完美哈希函数”。假设年份范围合理，没有两个日期会有相同的哈希码。（`LocalDate` 类的实际 `hashCode` 方法支持 ±999,999,999 年的范围，要稍微复杂一些。）

### java.lang.Object 1.0

- `int hashCode()` 返回此对象的哈希码。哈希码可以是任意整数，正数或负数。相等的对象需要返回相同的哈希码。

### java.util.Objects 7

- `static int hash(Object... objects)` 返回一个由所有提供的对象的哈希码组合而成的哈希码。

- `static int hashCode(Object a)` 如果 a 为 null，则返回 0；否则返回 `a.hashCode()`。

### java.lang.(Integer|Long|Short|Byte|Double|Float|Character|Boolean) 1.0

- `static int hashCode(xxx value)` 8 返回给定值的哈希码。这里的 `xxx` 是对应于给定包装类型的基本类型。

### java.util.Arrays 1.2

- `static int hashCode(xxx[] a)` 5 计算数组 a 的哈希码。数组的组件类型 xxx 可以是 Object、int、long、short、char、byte、boolean、float 或 double。

### 5.2.5 toString 方法

`Object` 中另一个重要的方法是 `toString` 方法，它返回表示此对象值的字符串。下面是一个典型示例。`Point` 类的 `toString` 方法返回如下字符串：

```text
java.awt.Point[x=10,y=20]
```

大多数（但不是全部）`toString` 方法遵循这种格式：类名，然后是括在方括号中的字段值。下面是 `Employee` 类的 `toString` 方法的一个实现：

```java
public String toString()
{
    return "Employee[name=" + name
        + ",salary=" + salary
        + ",hireDay=" + hireDay
        + "]";
}
```

实际上，还可以做得稍好一些。不要在 `toString` 方法中硬编码类名，而是调用 `getClass().getName()` 来获得包含类名的字符串。

```java
public String toString()
{
    return getClass().getName()
        + "[name=" + name
        + ",salary=" + salary
        + ",hireDay=" + hireDay
        + "]";
}
```

这样的 toString 方法对子类也同样有效。

当然，子类程序员应该定义自己的 toString 方法并添加子类字段。如果超类使用 getClass().getName()，那么子类可以简单地调用 super.toString()。例如，下面是 Manager 类的 toString 方法：

```java
public class Manager extends Employee
{
    . . .
    public String toString()
    {
        return super.toString()
            + "[bonus=" + bonus
            + "]";
    }
}
```

现在，一个 Manager 对象会打印为

```text
Manager[name=. . .,salary=. . .,hireDay=. . .][bonus=. . .]
```

toString 方法无处不在，原因很重要：每当对象通过“+”运算符与字符串连接时，Java 编译器都会自动调用 toString 方法以获得对象的字符串表示。例如：

```java
var p = new Point(10, 20);
String message = "The current position is " + p;
  // automatically invokes p.toString()
```

**提示：**

不必写 `x.toString()`，可以写 `"" + x`。这条语句将空字符串与 x 的字符串表示连接起来，而该表示恰好就是 `x.toString()`。与 `toString` 不同，即使 x 是基本类型，这条语句也能工作。

如果 x 是任意对象，并且你调用

```java
System.out.println(x);
```

那么 `println` 方法只是调用 `x.toString()` 并打印结果字符串。

`Object` 类定义的 toString 方法会打印类名和对象的哈希码。例如，调用

```java
System.out.println(System.out)
```

产生的输出类似下面这样：

```text
java.io.PrintStream@2f6684
```

原因是 `PrintStream` 类的实现者没有费心重写 `toString` 方法。

![](img/0e7b74ef51a065c077b42cd87b362288_364_0.png)

**警告：**

令人烦恼的是，数组从 Object 继承了 `toString` 方法，而且还多了一个奇怪之处：数组类型会以古老格式打印。例如，

```java
int[] luckyNumbers = { 2, 3, 5, 7, 11, 13 };
String s = "" + luckyNumbers;
```

## 第2章 卒中

卒中是由脑血管损伤引起的突发性神经功能缺损——要么由缺血（血流阻塞）引起，要么由出血（血液流入大脑）引起。

卒中的两大类别是缺血性和出血性，二者具有不同的病理生理机制和治疗方法。

大脑中动脉（MCA）是缺血性卒中中最常受累的血管，会导致对侧运动和感觉缺损，如果优势半球受累，还会导致失语症。

累及椎基底动脉系统的后循环卒中可引起脑干体征、视野缺损和共济失调，并且临床上通常更难诊断。

出血性卒中虽然比缺血性卒中少见，但早期死亡率更高，并且常与高血压、破裂动脉瘤或动静脉畸形相关。

代码清单 5.4 中的程序测试了 Employee 类（代码清单 5.5）和 Manager 类（代码清单 5.6）的 equals、hashCode 和 toString 方法。

### **代码清单 5.4** equals/EqualsTest.java

```java
 1  package equals;
 2
 3  /**
 4   * This program demonstrates the equals method.
 5   * @version 1.12 2012-01-26
 6   * @author Cay Horstmann
 7   */
 8  public class EqualsTest
 9  {
10     public static void main(String[] args)
11     {
12        var alice1 = new Employee("Alice Adams", 75000, 1987, 12, 15);
13        var alice2 = alice1;
14        var alice3 = new Employee("Alice Adams", 75000, 1987, 12, 15);
15        var bob = new Employee("Bob Brandson", 50000, 1989, 10, 1);
16
17        System.out.println("alice1 == alice2: " + (alice1 == alice2));
18
19        System.out.println("alice1 == alice3: " + (alice1 == alice3));
20
21        System.out.println("alice1.equals(alice3): " + alice1.equals(alice3));
22
23        System.out.println("alice1.equals(bob): " + alice1.equals(bob));
24
25        System.out.println("bob.toString(): " + bob);
26
27        var carl = new Manager("Carl Cracker", 80000, 1987, 12,
```
