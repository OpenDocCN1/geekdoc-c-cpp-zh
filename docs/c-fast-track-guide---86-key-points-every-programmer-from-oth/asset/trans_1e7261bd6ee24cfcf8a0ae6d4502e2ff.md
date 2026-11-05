
## 34. 使用元组返回多个值

元组允许你从一个方法中返回多个值，而无需创建类或结构体。它们轻量、灵活且可读。

此示例展示如何使用元组返回多个值，以及如何访问这些值。

[代码示例]

```csharp
using System;

class Program
{
    // A method returning a tuple with two values
    static (string name, int age) GetPerson()
    {
        return ("Bob", 28);
    }

    static void Main()
    {
        // Receiving the tuple result
        var person = GetPerson();
        // Accessing tuple values by name
        Console.WriteLine($"Name: {person.name}, Age: {person.age}");
    }
}
```

[执行结果]

Name: Bob, Age: 28

方法 GetPerson() 返回一个 (string name, int age) 元组。这比仅仅为了返回两个值而创建自定义类要简洁得多。

需要了解的关键点：

- 你可以为字段命名（name、age）以提高可读性。
- 元组是可变的，不像匿名类型。创建后可以更改其字段。
- 你可以像这样使用元组解构：

  ```csharp
  var (n, a) = GetPerson();
  Console.WriteLine($"Deconstructed: {n}, {a}");
  ```

C# 元组不同于早期版本引入的 System.Tuple<>——现代 (T1, T2) 语法更强大、更可读。

[补充]

元组是值类型（结构体），因此除非被装箱，否则它们存储在栈上。

你可以从方法返回元组、将它们作为参数传递，并在模式匹配中使用它们。

如果你需要语义含义或方法，请考虑使用 record 或类，而不是元组。

## 35. 理解用于不可变数据结构的 C# record

C# 中的 record 是一种引用对象类型，旨在以不可变方式存储数据。一旦创建，其数据就不能更改。

下面是一个使用 C# record 表示人的基本示例，展示了数据在创建后如何保持不变。

[代码示例]

```csharp
// Define a record type with two properties
public record Person(string FirstName, string LastName);

class Program
{
    static void Main()
    {
        // Create a new record instance
        var person1 = new Person("Alice", "Smith");
        // Use 'with' expression to create a new record with one changed property
        var person2 = person1 with { LastName = "Johnson" };
        Console.WriteLine(person1); // Output: Person { FirstName = Alice, LastName = Smith }
        Console.WriteLine(person2); // Output: Person { FirstName = Alice, LastName = Johnson }
    }
}
```

[执行结果]

Person { FirstName = Alice, LastName = Smith }

Person { FirstName = Alice, LastName = Johnson }

C# 中的 record 类型是在 C# 9 中引入的。

它们默认不可变，这意味着其值在创建后不能更改。

你可以使用 with 表达式创建带有修改值的副本。

与类不同，record 提供基于值的相等性——两个数据相同的 record 被视为相等。

这非常适合 DTO（数据传输对象）、配置或事件数据等场景。

与类比较：

- class：引用相等性——内存中的同一对象。
- record：值相等性——相同的数据内容。

为什么不可变性很重要：

- 避免因数据的意外更改而导致的错误。
- 在多线程环境中更容易推理。

[补充]

record 也可以有方法、构造函数和继承。

你可以使用属性声明定义 record（record Person { string FirstName; string LastName; }），但使用位置语法（如上所示）更简洁。

尽管 record 在许多方面表现得像值类型，但它在底层仍然是引用类型。

## 36. 使用索引器让对象像数组一样工作

索引器允许类或结构体公开类似数组的语法，以访问其内部数据。

这个简单示例展示如何实现索引器，以使用方括号语法访问类似集合的类的元素。

[代码示例]

```csharp
using System;

class Week
{
    private string[] days = { "Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" };

    // Indexer declaration
    public string this[int index]
    {
        get { return days[index]; }
        set { days[index] = value; }
    }
}

class Program
{
    static void Main()
    {
        Week week = new Week();
        Console.WriteLine(week[0]); // Access like an array: Sunday
        week[0] = "Funday"; // Modify value using indexer
        Console.WriteLine(week[0]); // Now: Funday
    }
}
```

[执行结果]

Sunday

Funday

- 索引器让你可以在对象上使用数组语法（[]），使对象感觉更直观。
- 你在类内部使用 this 关键字定义它们。
- 它们可以是只读、只写或读/写。
- 当你构建管理集合的类或想要更简洁的 API 时很有用。

语法：

```csharp
public returnType this[parameter]
{
    get { ... }
    set { ... }
}
```

在幕后，索引器只是特殊方法（get_Item、set_Item），但对用户而言，它们的行为像数组。

[补充]

你可以重载索引器——例如，this[string name] 和 this[int index] 可以共存。

## 37. 使用重载自定义运算符行为

运算符重载允许开发人员重新定义标准运算符（如 +、-、==）对自定义类的行为。

以下代码演示如何为简单的 Point 类重载 + 运算符，以便直观地将两个点相加。

[代码示例]

```csharp
using System;

class Point
{
    public int X, Y;

    public Point(int x, int y)
    {
        X = x;
        Y = y;
    }

    // Overload the + operator to add two Point objects
    public static Point operator +(Point a, Point b)
    {
        return new Point(a.X + b.X, a.Y + b.Y);
    }

    public override string ToString()
    {
        return $"({X}, {Y})";
    }
}

class Program
{
    static void Main()
    {
        Point p1 = new Point(3, 4);
        Point p2 = new Point(1, 2);
        Point result = p1 + p2; // This uses our overloaded + operator
        Console.WriteLine(result); // Output: (4, 6)
    }
}
```

[执行结果]

(4, 6)

在 C# 中，运算符重载允许你定义当运算符与用户定义类的实例一起使用时的行为。在上面的示例中：

Point 是一个具有两个整数字段 X 和 Y 的类。

静态方法 operator + 接受两个 Point 实例，并返回一个坐标相加的新 Point。

这使得 p1 + p2 成为可能，就像使用基元类型一样。

重载运算符使你的自定义类型更易于使用、更直观，尤其是当该类型表示数学或逻辑对象（如向量、复数等）时。

重要规则：

- 并非所有运算符都可以重载（例如，&&、|| 必须与 true 和 false 一起重载）。
- 重载的运算符必须是 public static。
- 它可以提高代码可读性，但不应过度使用，否则可能会让其他开发人员困惑。

## 38. 使用显式和隐式运算符自定义类型转换

显式和隐式转换运算符允许开发人员定义如何将一种自定义类型转换为另一种类型，或反之。

以下代码演示 Celsius 类和 Fahrenheit 类之间的显式和隐式转换。

[代码示例]

```csharp
using System;

class Celsius
{
    public double Degrees;

    public Celsius(double degrees)
    {
        Degrees = degrees;
    }

    // Implicit conversion from double to Celsius
    public static implicit operator Celsius(double d)
    {
        return new Celsius(d);
    }

    // Explicit conversion from Celsius to Fahrenheit
    public static explicit operator Fahrenheit(Celsius c)
    {
        return new Fahrenheit(c.Degrees * 9 / 5 + 32);
    }

    public override string ToString()
    {
        return $"{Degrees} °C";
    }
}

class Fahrenheit
{
    public double Degrees;

    public Fahrenheit(double degrees)
    {
        Degrees = degrees;
    }

    public override string ToString()
    {
        return $"{Degrees} °F";
    }
}

class Program
{
    static void Main()
    {
        Celsius c = 25.0; // implicit conversion from double to Celsius
        Fahrenheit f = (Fahrenheit)c; // explicit conversion from Celsius to Fahrenheit
        Console.WriteLine(c); // Output: 25 °C
        Console.WriteLine(f); // Output: 77 °F
    }
}
```

[执行结果]

25 °C

77 °F

