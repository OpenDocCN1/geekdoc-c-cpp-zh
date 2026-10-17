
```java
interface Set {
    int red = 1;
    int blue = 2;
    int green = 3;
}
class SetImpl implements Set {
    void select(int colour) {
        switch(colour) {
            case red: System.out.println("RED IS SELECTED");
                break;
            case blue: System.out.println("BLUE IS SELECTED");
                break;
            case green: System.out.println("GREEN IS SELECTED");
                break;
        }
    }
}
public class Itest {
    public static void main(String[] s[]) {
        SetImpl ob = new SetImpl();
        ob.select(1);
        ob.select(2);
        ob.select(3);
    }
}
```

在列表 11 中，声明了一个包含一组整数的接口，最后一个实现此接口的类在 `switch` 语句内部逐个使用了这些整数。整数的值被传递给 `main()` 方法调用的方法参数。图 12 显示了 `Itest.java` 类的执行：

## 实现包和接口

![](img/d3faa73f55d3d314bb5bfb277886900d_184_0.png)

▲ 图 12：显示 `Itest.java` 的输出

图 12 显示了执行 `Itest` 类时的输出，该类实现了 `Set` 接口的变量。到此本章已结束，让我们总结一下在本章中学到的概念。

## 总结

本章介绍了接口的引用变量。你可以创建一个类似于类引用变量的接口引用变量。此外，通过使用引用变量，你可以轻松地访问实现接口的类中的方法。本章介绍了使用 `extends` 关键字扩展接口。与不允许多重继承的类实现不同，接口可以扩展多个接口。在继承层次结构中，通过扩展接口而形成的接口被称为子接口，被扩展的接口被称为超接口。本章介绍了访问接口变量。类似于在其他编程语言中声明头文件一样，Java 也允许在接口内部声明一组常量，这些常量可以像普通变量一样被任何字段或方法访问。本章介绍了实现包和接口。

## 复习题

判断以下陈述对错：

1. `protected` 访问修饰符。

2. `import` 语句必须在类定义之前。

3. 在 Java 中，`Object` 类是所有类的基类。

4. 接口内部可以声明一组静态常量。

5. 接口可以定义抽象方法和非抽象方法。

6. 如果一个类实现多个接口，它们必须用逗号隔开。

7. `java.lang` 包中的 `Number` 类是抽象类。

8. 在 Java 中，`Runtime` 类提供了访问运行时的方法。

9. 接口可以有抽象方法，但抽象类只能有抽象方法。

10. 导入包允许使用包中的类。

单选题

回答以下单选题：

1. 哪一个类是 Java 中所有类的基类？

a. `Object` 类

b. `Class` 类

c. `Runtime` 类

d. `Number` 类

答案：a

2. 哪一个类提供了访问运行时的方法？

a. `Object` 类

b. `Class` 类

c. `Runtime` 类

d. `Number` 类

答案：c

3. 哪一个类是 `java.lang` 包中的抽象类？

a. `Object` 类

b. `Class` 类

c. `Runtime` 类

d. `Number` 类

答案：a

4. 哪一个包提供了许多输入输出流，用于读写数据文件、字符串和其他源？

a. `java.lang`

b. `java.io`

c. `java.util`

d. `java.awt`

答案：b

5. 哪一个包会自动导入到每个 Java 程序中？

a. `java.lang`

b. `java.io`

c. `java.util`

d. `java.awt`

答案：a

6. 哪一个包包含了创建用户界面并绘制图形、图像、窗口、对话框、按钮、复选框、列表、菜单、滚动条和文本框的所有类？

a. `java.lang`

b. `java.io`

c. `java.util`

d. `java.awt`

答案：d

7. `Class` 的哪一个方法将当前对象转换为字符串？

a. `getName()`

b. `getInstance()`

c. `get()`

d. `toString()`

答案：d

8. `Hashtable` 的哪一个方法将指定的键插入到当前哈希表中？

a. `public synchronized Object remove(Object key)`

b. `public synchronized Object put(Object key, Object value)`

c. `public synchronized clone()`

d. `public synchronized String toString()`

答案：b

# 实现包与接口 173

Q9. `Random` 类的下列哪个方法可以从当前随机数生成器的序列中获取布尔型随机数？

答. 选项 a 正确。

Q10. 下列方法中哪一个可以使当前线程进入等待状态，直到另一个线程解锁当前对象？

答. 选项 c 正确。

## 简答题

Q1. Java API 包含许多类和接口，它们根据相似的功能以包的形式进行排列。这些是 Java API 的内置包。

Q2. 列出 Java API 中的包。

答. Java API 中可用的包：

- `java.lang`

- `java.io`

- `java.util`

- `java.net`

- `java.awt`

- `java.applet`

Q3. 接口中的常量是什么？

答. 接口可以包含常量，这些常量通过以 `public`、`static` 或 `final` 成员的形式定义的字段定义来定义。它们在接口声明期间以及通过实现接口的类进行初始化。

Q4. 简述解释访问修饰符？

答. 类的成员在同一个类或其他类中具有可访问性。类成员如何以及在何处访问由访问修饰符决定。以下是访问修饰符：

- `public` 访问修饰符：指定当使用 `public` 修饰符声明类时，可以从程序的任何地方访问。

- `protected` 访问修饰符：指定当使用 `protected` 修饰符声明类时，可以在方法和字段所属的类内部、其子类内部以及相同包的类中访问，但不能从其他包访问。

- `private` 访问修饰符：指定当你将方法或字段声明为 `private` 时。它对子类不可见，且不会被子类继承。

- 默认 `default` 访问修饰符：表示如果在声明类、方法或字段时没有指定任何访问修饰符，则它们被视为默认访问修饰符。注意，类成员对于关联类以及相同包内的子类仍然是可见的。

# 174 第 5 章

Q5. 在 Java 中定义包 `Package`？

答. Java API 包含多个类和接口，它们根据相似的功能以包的形式进行排列。这些是 Java API 的内置包，与其使用这些内置包：你也可以在应用程序中创建自己的包。

Q6. 简述讨论包的重要分类？

答. 在 Java 中，包分为以下几类：

- 内置包：提供你可以在程序中使用的某些内置功能。这些功能是以类和接口的形式编码的。

- 用户自定义包：允许用户创建一个包以执行某些特定任务。这些包也可以像内置包一样的方式被导入和使用。

Q7. 在 Java 中定义接口 `Interface`？

答. 在 Java 中，接口类似于抽象类。接口不提供任何方法的实现；因此它们在本质上是抽象的。抽象类可以同时定义抽象方法和非抽象方法，而接口只有抽象方法。

Q8. 写下接口的语法？

答. 接口的语法如代码段所示：

Q9. 讨论声明接口的规则如下：

答. 声明接口的规则是：

- 接口只声明常量：而不是声明实例变量。

- 接口中声明的变量必须是隐式的 `static`、`public` 和 `final`。

- 接口方法不能是 `static`、`native` 或 `final`。

- 接口可以扩展另一个类或接口。

- 接口不能实现另一个类或接口。

Q10. 简述解释如何在 Java 中导入包？

答. 在任何应用程序中导入包允许你利用存储在这些包中的类所带来的优势。你可以在应用程序中导入所需的任意数量包。此外，你还可以导入用户自定义包。

Q7. 编写一个程序，同时使用 `pack` 包中的 `Addition` 和 `Subtraction` 类。

Ans.

```java
import pack.Addition;
import pack.Subtraction;
class Use {
    public static void main(String args[]) {
        // 创建 Addition 类对象
        Addition obj = new Addition(10, 15.5);

        // 调用 sum() 方法
        obj.sum();

        // 调用 sub() 方法并传递值
        double res = Subtraction.sub(10, 15.5);
        System.out.println("Result=" + res);
    }
}
```

Output:

Sum= 25.5

Result=-5.5

Q8. 编写一个程序，创建一个带有单一方法的接口，用于显示系统日期。

Ans.

```java
// 在 mypack 包中创建 MyDate 接口
package mypack;
public interface MyDate {
    void showDate();
}
```

Q9. 编写一个程序，为 `MyDate` 接口创建一个名为 `DateImpl` 的实现类，并将其存储在相同的包 `mypack` 中。

Ans.

```java
package mypack; // 将 DateImpl 类存储在 mypack 中
import mypack.MyDate;
import java.util.*;
public class DateImpl implements MyDate {
    public void showDate() {
        // Date 对象默认存储系统日期时间
        Date d = new Date();
        System.out.println(d);
    }
}
```

Q10. 编写一个程序，展示如何使用 `MyDate` 接口的实现类 `DateImpl`。

Ans.

```java
// 使用 mypack 中的 DateImpl
import mypack.DateImpl;
class DateDisplay
{
    public static void main(String args[])
{
        // 创建 DateImpl 对象
        DateImpl obj = new DateImpl();
        // 调用 ShowDate()
        obj.showdate();
    }
}
```

Output:

Fri Nov 11 11:57:11 IST 2011

# 06 字符串处理

## 目标

- 学习字符串构造函数

- 学习如何查找字符串的长度

- 探索特殊的字符串操作

- 研究字符提取

- 学习如何修改字符串

- 学习如何搜索和比较字符串

字符串在 Java 中非常重要，它们可以通过构造函数来创建。在 Java 中，字符串是不可变的，一旦创建，其值就不能更改。此外，Java 提供了许多方法来处理字符串，例如拼接、截取、替换、比较等。

## 6.1 字符串构造函数

在 Java 中，字符串构造函数用于创建字符串对象。字符串位于 `java.lang` 包中。以下是常用的字符串构造函数：

# 表 1 字符串类的构造函数

| 构造函数 | 描述 |
| :--- | :--- |
| `String ()` | 创建一个空字符串对象。 |
| `String (String str)` | 使用指定的字符串创建一个新的字符串对象。 |
| `String (char[] value)` | 使用指定的字符数组创建一个字符串对象。 |
| `String (char[] value, int offset, int count)` | 使用字符数组的特定部分创建字符串对象。 |
| `String (byte[] bytes)` | 使用字节数组创建一个字符串对象。 |
| `String (byte[] bytes, int offset, int count)` | 使用字节数组的特定部分创建字符串对象。 |

除了使用构造函数创建和初始化字符串对象外，你还可以使用以下代码片段来创建和初始化字符串：

```java
String str="Hello";
```

上述代码创建了一个字符串对象 `str`，并将其初始化为 `Hello`。你也可以将一个字符串对象的值赋值另一个字符串对象。考虑以下代码片段，将字符串对象的值赋值另一个字符串对象：

```java
String str1="Now";
str2="Are";
str1=str2; // 现在 str1 包含 Are
```

# 184 第 6 章

```java
teamArray[2] = "Mahtab";
teamArray[3] = "Shivam", "vikash";
teamArray[4] = "vikash";
```

在前面的代码段中，每个数组索引都是单独初始化的，即分别创建并初始化。在这段代码中，以这种方式初始化数组是一个耗时且枯燥的过程。为了节省时间，您可以使用以下代码段在创建时初始化数组：

```java
String [] teamArray = {"Niraj", "Umar", "Mahtab", "Shivam", "vikash"};
```

列表 2 显示了 String 数组的实现（您可以在 CD 中 `Code/Chapter6` 文件夹下找到 `StrArray.java` 文件）：

## 列表 2：使用字符串数组

```java
class StrArray
{
    public static void main(String[] args) {
        String [] teamArray = {"Niraj", "Umar", "Mahtab", "Shivam", "vikash"};
        for(int i = 0; i<teamArray.length;i++) {
            System.out.print("Value at Index " + i + " is: ");
            System.out.println(teamArray[i]);
        }
    }
}
```

在列表 2 中，创建了一个名为 `teamArray` 的数组并用 5 个字符串值进行了初始化。这些值存储在数组中，然后通过循环进行访问。图 2 显示了存储在数组 `teamArray` 中的值：

![](img/d3faa73f55d3d314bb5bfb277886900d_197_0.png)

> 图 2：显示 `StrArray` 类的输出

## 6.3 字符串长度

可以使用 `length()` 方法计算字符串的长度。它计算包含在 " " 内的所有字符、符号和数字。该方法返回一个整数值。列表 3 显示了 `StrLen` 的代码（您可以在 CD 中 `Code/Chapter6` 文件夹下找到 `StrLen.java` 文件）：

## 列表 3：在 `StrLen` 类中使用 `length()` 方法

```java
public class StrLen{
    public static void main(String args[]) {
    String str="length";
    int x = str.length();
    System.out.println("Length of the string is " + x);
    }
}
```

在列表 3 中，一个 `String` 对象 `str` 被初始化为值 `length`。然后对 `str` 应用 `length()` 方法以计算其长度。

图 3 显示了列表 3 的输出：

![](img/d3faa73f55d3d314bb5bfb277886900d_198_0.png)

图 3：显示 `StrLen` 类的输出

让我们在下一节中学习一些特殊的字符串操作。

## 特殊字符串操作

Java 提供了对各种字符串操作的支持。这些操作包括字符串拼接和字符串转换。`concat()` 方法用于字符串拼接，而 `toString()` 方法用于字符串转换。在本节中，我们将讨论 `concat()` 和 `toString()` 方法。

- 实现 `concat()` 方法

`concat()` 方法将一个字符串附加到另一个字符串的末尾。该方法在拼接后返回一个字符串。在 Java 中，您可以通过两种方式拼接字符串：使用拼接运算符 `+` 或使用 `concat()` 方法。

列表 4 显示了 `Concat` 类的代码（您可以在 CD 的 `Chapter6` 文件夹中找到 `Concat.java` 文件）：

- 列表 4：在 `Concat` 类中使用 `concat()` 方法

```java
public class Concat{
    public static void main(String args[]) {
    String str = "Hello";
    String str1 = "Java";
    System.out.print(str.concat(str1));
    }
}
```

在列表 4 中，创建了两个 `String` 对象 `str` 和 `str1`，并分别初始化为 `Hello` 和 `Java`。然后使用 `concat()` 方法对这些 `String` 对象进行拼接。
