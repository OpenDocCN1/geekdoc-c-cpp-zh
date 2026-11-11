

```java
people[1] = new Student(. . .);
```

然后，我们打印这些对象的名称和描述：

```java
for (Person p : people)
   System.out.println(p.getName() + ", " + p.getDescription());
```

有些人对下面这个调用感到困惑：

```java
p.getDescription()
```

这不是对未定义方法的调用吗？请记住，变量 p 从不引用 Person 对象，因为不可能构造抽象类 Person 的对象。变量 p 总是引用具体子类的对象，例如 Employee 或 Student。对于这些对象，getDescription 方法是已定义的。

你能否从 Person 超类中完全省略这个抽象方法，只在 Employee 和 Student 子类中定义 getDescription 方法？如果那样做，你就无法在变量 p 上调用 getDescription 方法。编译器确保你只调用类中声明的方法。

抽象方法是 Java 编程语言中的一个重要概念。你最常会在*接口*中遇到它们。有关接口的更多信息，请参阅[第 6 章](#)。

### 清单 5.8 `abstractClasses/PersonTest.java`

```java
1  package abstractClasses;
2
3  /**
4   * This program demonstrates abstract classes.
5   * @version 1.01 2004-02-21
6   * @author Cay Horstmann
7   */
8  public class PersonTest
{
    public static void main(String[] args)
    {
        var people = new Person[2];

        // fill the people array with Student and Employee objects
        people[0] = new Employee("Harry Hacker", 50000, 1989, 10, 1);
        people[1] = new Student("Maria Morris", "computer science");

        // print out names and descriptions of all Person objects
        for (Person p : people)
            System.out.println(p.getName() + ", " + p.getDescription());
    }
}
```

### 清单 5.9 `abstractClasses/Person.java`

```java
package abstractClasses;

public abstract class Person
{
    public abstract String getDescription();
    private String name;

    public Person(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
16    }
17 }
```

### **清单 5.10** `abstractClasses/Employee.java`

```java
1  package abstractClasses;
2
3  import java.time.*;
4
5  public class Employee extends Person
6  {
7      private double salary;
8      private LocalDate hireDay;
9
10     public Employee(String name, double salary, int year, int
   month, int day)
11     {
12         super(name);
13         this.salary = salary;
14         hireDay = LocalDate.of(year, month, day);
15     }
16
17     public double getSalary()
18     {
19         return salary;
20     }
21
22     public LocalDate getHireDay()
23     {
24         return hireDay;
25     }
26
27     public String getDescription()
28     {
29         return "an employee with a salary of
   $%.2f".formatted(salary);
30     }
31
    public void raiseSalary(double byPercent)
    {
        double raise = salary * byPercent / 100;
        salary += raise;
    }
}
```

### **清单 5.11** `abstractClasses/Student.java`

```java
package abstractClasses;

public class Student extends Person
{
    private String major;

    /**
     * @param name the student's name
     * @param major the student's major
     */
    public Student(String name, String major)
    {
        // pass name to superclass constructor
        super(name);
        this.major = major;
    }

    public String getDescription()
    {
        return "a student majoring in " + major;
    }
}
```

## 5.7 枚举类

你在[第 3 章](#)中看到了如何定义枚举类型。下面是一个典型示例：

```java
public enum Size { SMALL, MEDIUM, LARGE, EXTRA_LARGE }
```

这个声明定义的类型实际上是一个类。该类恰好有四个实例——不可能构造新对象。

因此，对于枚举类型的值，你永远不需要使用 `equals`。只需使用 `==` 来比较它们。

如果你愿意，可以向枚举类型添加构造器、方法和字段。当然，构造器只在构造枚举常量时被调用。下面是一个示例：

```java
public enum Size
{
    SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");
    private String abbreviation;
    Size(String abbreviation) { this.abbreviation =
    abbreviation; }
        // automatically private
    public String getAbbreviation() { return abbreviation; }
}
```

枚举的构造器总是私有的。你可以像前面的示例那样省略 `private` 修饰符。将枚举构造器声明为 `public` 或 `protected` 是语法错误。

所有枚举类型都是抽象类 `Enum` 的子类。它们从该类继承了许多方法。最有用的一个是 `toString`，它返回枚举常量的名称。例如，`Size.SMALL.toString()` 返回字符串 `"SMALL"`。

`toString` 的反操作是静态 `valueOf` 方法。例如，语句

```java
Size s = Enum.valueOf(Size.class, "SMALL");
```

将 `s` 设置为 `Size.SMALL`。

每个枚举类型都有一个静态 values 方法，它返回该枚举所有值的数组。例如，调用

```java
Size[] values = Size.values();
```

返回包含元素 `Size.SMALL`、`Size.MEDIUM`、`Size.LARGE` 和 `Size.EXTRA_LARGE` 的数组。

ordinal 方法给出枚举常量在枚举声明中的位置，从零开始计数。例如，`Size.MEDIUM.ordinal()` 返回 1。

[清单 5.12](#) 中的简短程序演示了如何使用枚举类型。

> **注意：**
>
> `Enum` 类有一个类型参数，为简单起见我忽略了它。例如，枚举类型 `Size` 实际上扩展了 `Enum<Size>`。该类型参数用于 `compareTo` 方法。我在第 6 章讨论 `compareTo` 方法，并在第 8 章讨论类型参数。

### **清单 5.12** `enums/EnumTest.java`

```java
1  package enums;
2
3  import java.util.*;
4
5  /**
6   * This program demonstrates enumerated types.
7   * @version 1.0 2004-05-24
8   * @author Cay Horstmann
9   */
10 public class EnumTest
11 {
12  public static void main(String[] args)
13  {
14      var in = new Scanner(System.in);
15      System.out.print("Enter a size: (SMALL, MEDIUM, LARGE,
    EXTRA_LARGE) ");
16      String input = in.next().toUpperCase();
17      Size size = Enum.valueOf(Size.class, input);
18      System.out.println("size=" + size);
19      System.out.println("abbreviation=" +
    size.getAbbreviation());
20      if (size == Size.EXTRA_LARGE)
21          System.out.println("Good job--you paid attention to
    the __");
22  }
23 }

25 enum Size
26 {
27     SMALL("S"), MEDIUM("M"), LARGE("L"), EXTRA_LARGE("XL");

29     private Size(String abbreviation) { this.abbreviation =
    abbreviation; }
30     public String getAbbreviation() { return abbreviation; }

32     private String abbreviation;
33 }
```

### java.lang.Enum&lt;E&gt; 5

- `static Enum valueOf(Class enumClass, String name)`：返回给定类中具有给定名称的枚举常量。
- `String toString()`：返回此枚举常量的名称。
- `int ordinal()`：返回此枚举常量在枚举声明中从零开始的位置。
- `int compareTo(E other)`：如果此枚举常量位于 other 之前，则返回负整数；如果 this == other，则返回 0；否则返回正整数。常量的顺序由枚举声明给出。

## 5.8 密封类

除非一个类被声明为 final，否则任何人都可以创建它的子类。如果你想要更多控制权呢？例如，假设你需要编写自己的 JSON 库，因为现有库没有一个能完全满足你的需求。

JSON 标准规定，JSON 值是一个数组、数字、字符串、布尔值、对象或 null。一种显而易见的做法是用扩展抽象类 `JSONValue` 的 `JSONArray`、`JSONNumber` 等类来建模：

```java
public abstract class JSONValue
{
    // Methods that apply to all JSON values
}
public final class JSONArray extends JSONValue
{
    . . .
}
public final class JSONNumber extends JSONValue
{
    . . .
}
```

通过将 `JSONArray`、`JSONNumber` 等类声明为 `final`，我们可以确保没有人创建子类。但我们无法阻止任何人创建 `JSONValue` 的另一个子类。

