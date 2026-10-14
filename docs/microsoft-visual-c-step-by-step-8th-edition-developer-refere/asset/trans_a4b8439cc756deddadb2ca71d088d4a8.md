

## Note

请注意，此赋值语句可能无法实现你所期望的效果。你将在第 8 章了解更多关于为对象变量赋值的知识。

匿名类的内容有相当多的限制。例如，匿名类只能包含 public 字段，字段必须全部初始化，它们不能是 static，并且你不能为它们定义任何方法。你将在本书中定期使用匿名类，并在使用过程中了解更多关于它们的信息。

## Summary

在本章中，你学习了如何定义新的类。你了解到默认情况下类的字段和方法是 private，对类外部的代码不可访问，但你可以使用 *public* 关键字将字段和方法暴露给外部世界。你学习了如何使用 *new* 关键字创建类的新实例，以及如何定义可以在创建时初始化类实例的构造函数。最后，你学习了如何实现 static 字段和方法，以提供与类的任何特定实例无关的数据和操作。

- 如果你想继续阅读下一章，请保持 Visual Studio 2015 运行并翻到第 8 章。
- 如果你现在想退出 Visual Studio 2015，请在 File 菜单上单击 Exit。如果出现 Save 对话框，请单击 Yes 并保存项目。

## Quick reference

| To | Do this |
|---|---|
| Declare a class | Write the keyword *class*, followed by the name of the class, followed by opening and closing braces. The methods and fields of the class are declared between the opening and closing braces. For example:
```
class Point
{
    ...
}
``` |
| Declare a constructor | Write a method whose name is the same as the name of the class and that has no return type (not even *void*). For example:
```
class Point
{
    public Point(int x, int y)
    {
        ...
    }
}
``` |
| Call a constructor | Use the *new* keyword and specify the constructor with an appropriate set of parameters. For example:
```
Point origin = new Point(0, 0);
``` |
| Declare a static method | Write the keyword *static* before the declaration of the method. For example:
```
class Point
{
    public static int ObjectCount()
    {
        ...
    }
}
``` |
| Call a static method | Write the name of the class, followed by a period, followed by the name of the method. For example:
```
int pointsCreatedSoFar = Point.ObjectCount();
``` |
| Declare a static field | Use the keyword *static* before the type of the field. For example:
```
class Point
{
    ...
    private static int objectCount;
}
``` |
| Declare a const field | Write the keyword *const* before the declaration of the field and omit the *static* keyword. For example:
```
class Math
{
    ...
    public const double PI = ...;
}
``` |
| Access a static field | Write the name of the class, followed by a period, followed by the name of the static field. For example:
```
double area = Math.PI * radius * radius;
``` |

## Chapter 8. Understanding values and references

完成本章后，你将能够：

- Explain the differences between a value type and a reference type.
- Modify the way in which arguments are passed as method parameters by using the ref and out keywords.
- Convert a value into a reference by using boxing.
- Convert a reference back to a value by using unboxing and casting.

第 7 章“Creating and managing classes and objects”演示了如何声明自己的类以及如何使用 new 关键字创建对象。该章还向你展示了如何使用构造函数初始化对象。在本章中，你将学习原始类型（如 int、double 和 char）的特性与类类型的特性有何不同。

## Copying value type variables and classes

C# 内置的大多数原始类型，如 int、float、double 和 char（但不包括 string，原因稍后会说明）统称为值类型。这些类型具有固定大小，当你将变量声明为值类型时，编译器会生成代码分配一块足够大的内存来保存相应的值。例如，声明一个 int 变量会导致编译器分配 4 字节内存（32 位）来保存整数值。将值（如 42）赋给 int 的语句会将该值复制到这块内存中。

像 Circle（在第 7 章中描述）这样的类类型则处理方式不同。当你声明一个 Circle 变量时，编译器不会生成分配一块足够大以容纳 Circle 的内存的代码；它只分配一小块内存，可以潜在地保存指向包含 Circle 的另一块内存的地址（或引用）。（地址指定了内存中某项的位置。）实际 Circle 对象的内存只有在使用 new 关键字创建对象时才会被分配。类是引用类型的一个例子。引用类型保存对内存块的引用。要编写充分利用 Microsoft .NET Framework 的有效 C# 程序，你需要理解值类型和引用类型之间的区别。

## Note

C# 中的 string 类型实际上是一个类。这是因为字符串没有标准大小（不同的字符串可以包含不同数量的字符），并且在程序运行时动态分配内存给字符串比在编译时静态分配要高效得多。本章中对类等引用类型的描述同样适用于 string 类型。事实上，C# 中的 string 关键字只是 System.String 类的别名。

考虑一种情况，你声明一个名为 i 的 int 变量并将其赋值为 42。如果声明另一个名为 copyi 的 int 变量然后将 i 赋给 copyi，copyi 将持有与 i 相同的值（42）。然而，即使 copyi 和 i 恰好持有相同的值，两个内存块中都包含值 42：一个块用于 i，另一个块用于 copyi。如果你修改 i 的值，copyi 的值不会改变。让我们在代码中看看这一点：

Click here to view code image

```
int i = 42;      // declare and initialize i
int copyi = i; /* copyi contains a copy of the data in i:
                  i and copyi both contain the value 42 */
i++;             /* incrementing i has no effect on copyi;
                  i now contains 43, but copyi still contains 42 */
```

声明一个类类型的变量 c，例如 Circle，其效果非常不同。当你将 c 声明为 Circle 时，c 可以引用一个 Circle 对象；c 所持有的实际值是内存中 Circle 对象的地址。如果你再声明一个名为 refc 的额外变量（同样是 Circle）并将 c 赋给 refc，refc 将拥有与 c 相同的地址的副本；换句话说，只有一个 Circle 对象，而 refc 和 c 现在都引用它。以下是代码示例：

```
Circle c = new Circle(42);
Circle refc = c;
```

下图显示了这两个示例。Circle 对象中的 at 符号（@）代表内存中的地址引用：

![](img/16f6e3fe08f01ddadb2741a92c392b0e_231_0.png)

![](img/16f6e3fe08f01ddadb2741a92c392b0e_231_1.png)

这种差异非常重要。特别是，这意味着方法参数的行为取决于它们是值类型还是引用类型。你将在下一个练习中探索这种差异。

## Copying reference types and data privacy

如果你实际上想将 Circle 对象 c 的内容复制到另一个 Circle 对象 refc 中，而不是仅仅复制引用，你必须使 refc 引用 Circle 类的新实例，然后逐字段地将数据从 c 复制到 refc，像这样：

Click here to view code image

```
Circle refc = new Circle();
refc.radius = c.radius;    // Don't try this
```

然而，如果 Circle 类的任何成员是 private（像 radius 字段），你将无法复制此数据。相反，你可以通过将它们公开为属性来使私有字段中的数据可访问，然后使用这些属性从 c 读取数据并将其复制到 refc。你将在第 15 章“Implementing properties to access fields”中学习如何做到这一点。

或者，一个类可以提供一个 Clone 方法，该方法返回同一类的另一个实例，但填充了相同的数据。Clone 方法可以访问对象中的私有数据，并可以直接将其复制到同一类的另一个实例。例如，

