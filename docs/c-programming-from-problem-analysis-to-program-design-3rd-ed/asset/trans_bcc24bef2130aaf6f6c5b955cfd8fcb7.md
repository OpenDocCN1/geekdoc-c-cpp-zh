

或者

```csharp
ClassName objectName;
objectName = new ClassName(argumentList);
```

更常见的做法是像前面所示那样，在一条语句中调用构造函数。

示例 4-11 创建三个对象，并调用示例 4-4 中定义的三个不同构造函数方法。

### 示例 4-11

```csharp
CarpetCalculator plush = new CarpetCalculator( );
CarpetCalculator pile =
        new CarpetCalculator(37.90, 17.95);
CarpetCalculator berber = new CarpetCalculator(17.95);
```

前面的每条语句都做两件事：

- 声明特定类的对象
- 调用构造函数以创建该类的实例

关键字 `new` 用作调用构造函数方法的运算符。示例 4-11 的第一行是对 `CarpetCalculator` 类默认构造函数的调用。创建了一个名为 plush 的对象。pricePerSqYard 和 NoOfSqYards 都被设置为 0.0。使用 double 的系统默认值来初始化这些实例变量。表 4-1 显示了在未向成员数据传递参数时，赋给变量的值类型的默认值。

### 表 4-1 值类型默认值

| 值类型 | 默认值 |
|---|---|
| bool | false |
| byte | 0 |
| char | '\0' (null) |
| decimal | 0.0M |
| double | 0.0D |
| float | 0.0F |
| int | 0 |
| long | 0L |
| short | 0 |
| uint | 0 |
| ulong | 0 |
| ushort | 0 |

![](img/e33ae760e23d89eac66541252ad65de8_232_0.png)

在 C# 中，不允许向未初始化的变量添加值。

第二次调用构造函数传递两个参数。创建了一个名为 pile 的对象，并使用第三个构造函数创建了一个名为 berber 的对象。实际参数 17.95 用于初始化私有成员 pricePerSqYard。

## 调用访问器方法和修改器方法

访问器和修改器都是实例方法。所有实例方法的调用方式与类方法完全相同，但有一个例外。如果该方法是从另一个已实例化该类对象的类中调用，则方法名前面要加上对象名。如果是同一个类中的另一个成员使用该方法，则只需方法名即可。绝不能像调用静态类方法那样，在实例方法前面加上类名。为了在另一个类中调用该方法，必须将特定对象与其关联。

CarpetCalculator 类的方法之一是 SetNoOfSqYards( )。另一个名为 CarpetCalculatorApp 的类，通过使用前面示例 4-4 中展示的单参数构造函数，实例化了 CarpetCalculator 类的一个对象。下面再次展示用于实例化 berber 对象的构造函数调用：

```csharp
CarpetCalculator berber = new CarpetCalculator(17.95);
```

调用 `SetNoOfSqYards( )` 方法需要对象名、一个点和方法名，如下代码所示。这是一个无返回值的方法。它是一个修改器方法。

```csharp
berber.SetNoOfSqYards(27.83);
```

如果方法像访问器那样返回值，则必须有用于接收返回值的位置。同样，通过键入 objectName、一个点和 methodName 来调用该方法。示例 4-12 展示了对访问器方法的调用，该调用有返回值。

### 示例 4-12

```csharp
Console.WriteLine("{0:N2}",
                 berber.GetNoOfSqYards( ));
```

表示平方码数的值会在从访问器方法 `return` 时打印出来。

成员属性通常以 `public` 访问权限定义。要引用 `set` 成员属性，可以在赋值语句中使用属性字段名，如下所示

```csharp
PropertyName = value;
```

可以像引用实例变量一样引用属性的 `get` 部分。示例 4-13 中的第 2 行展示了如何使用示例 4-8 中声明的属性 Price。

### 示例 4-13

```csharp
Line 1    Console.Write("Total Cost at {0:C} ",
Line 2                   berber.Price);
Line 3    Console.WriteLine(" per Square Yard: {0:C}",
Line 4                   berber.DetermineTotalCost( ));
```

注意，第 2 行中属性的使用与方法调用不同。属性不使用括号。

## 调用其他实例方法

与数据关联的所有行为都作为类的方法成员包含在内。这些方法称为实例方法，与类方法相对——因为要调用该方法，需要类的一个实例或一个对象。

在 `Student` 类中，`CalculateAverage( )` 是一个实例方法。`CalculateAverage( )` 方法的方法体已在示例 4-7 中展示。为了调用此方法，必须先实例化一个对象。这是示例 4-14 中展示的第一条语句。

### 示例 4-14

```csharp
Student aStudentObject = new Student(1234, "Maria Smith", 97, 75, 87,
    "CS");
average = aStudentObject.CalculateAverage();
```

你可能想回顾一下示例 4-3。这里调用该示例中展示的六参数构造函数来实例化该类。new 运算符创建对象 aStudentObject。如示例 4-14 所示，一旦实例化了 Student 对象，现在就可以调用 CalculateAverage( )。点号分隔对象和实例方法名。

由于 CalculateAverage( ) 的返回类型为 double，因此必须有用于接收返回值的位置。它通过赋值语句返回。另一种选择是将其直接返回到输出语句中。不过，调用它的唯一方式是使用 Student 类的一个对象。示例 4-15 展示了使用接受一个参数的构造函数实例化另一个 Student 对象（回顾示例 4-3）。示例 4-15 还演示了使用其属性为分数赋值，然后用该对象调用实例方法。这一次，CalculateAverage( ) 方法的值被返回到 WriteLine( ) 方法。

### 示例 4-15

```csharp
Student anotherStudentObject = new Student(2345 );
anotherStudentObject.Score1 = 95;
anotherStudentObject.Score2 = 62;
anotherStudentObject.Score3 = 87;
Console.WriteLine("Student ID: " +
    anotherStudentObject.StudentNumber +
    "\nAverage: {0:f1}",
    anotherStudentObject.CalculateAverage());
```

注意，CalculateAverage( ) 方法不需要任何参数。这是因为 CalculateAverage( ) 是 Student 类的成员，并且可以完全访问 Student 类的所有数据成员。属性 Score1、Score2、Score3 具有 public 访问模式。它们用于为私有实例数据成员 score1、score2 和 score3 赋值。

![](img/e33ae760e23d89eac66541252ad65de8_234_0.png)

请记住，要清除控制台窗口并将光标重新定位到显示顶部，请调用 Console.Clear()。

## 测试新类

测试和使用你的类需要另一个类。如果你按之前的建议将你的类作为第二个类添加到应用程序中，那么你已经拥有那个另一个类。这个另一个类就是包含 Main( ) 的类。在这里的 Main( ) 中，你可以构造你的类的对象，使用属性来赋值和检索值，并使用你构造的对象调用实例方法。示例 4-16 演示了测试你的类。

### 示例 4-16

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace StudentApp
{
    class StudentApp
    {
        static void Main(string[] args)
        {
            Student firstStudentObject = new Student();
            firstStudentObject.StudentName = AskForStudentName();
            firstStudentObject.StudentNumber = AskForStudentNumber();
            firstStudentObject.Major =
                AskForMajor(firstStudentObject.StudentName);
            firstStudentObject.Score1 = AskForExamScore(1);
            firstStudentObject.Score2 = AskForExamScore(2);
            firstStudentObject.Score3 = AskForExamScore(3);

            Console.Clear();
            Console.WriteLine("First Student");
            Console.WriteLine(firstStudentObject.ToString());

            Student secondStudentObject = new Student(2345);
            secondStudentObject.Score1 = 95;
            secondStudentObject.Score2 = 62;
            secondStudentObject.Score3 = 87;
            Console.WriteLine("\n\nSecond Student");
            Console.WriteLine("Student Number: " +
                secondStudentObject.StudentNumber +
                "\nAverage: {0:f1}",
                secondStudentObject.CalculateAverage());

            Student thirdStudentObject = new Student(5432, "Randolph Wonder");
            thirdStudentObject.Major = "Math";
            thirdStudentObject.Score1 = 95;
            thirdStudentObject.Score2 = 87;
            thirdStudentObject.Score3 = 72;
            Console.WriteLine("\n\nThird Student");
            Console.WriteLine(thirdStudentObject);
        }
    }
}
```

