
### 示例 B.47.

```csharp
public class Appendix_B {
    public static void Params(params string[] list) {
    }
    public static void Main() {
    }
}
```

## private、protected 和 public

Private、protected 和 public 是类或结构成员，它们允许根据专门为这些值编写的用户定义方法，对访问进行限制或限定。这些用户定义方法被声明为该类内部结构的一部分（见示例 B.48–B.50）。

### 示例 B.48.

```csharp
namespace Appendix_B {
    class BankAccount {
        private string first_name;
        private void ReadFiles(ref BankAccount acc) {}
        static void Main() {}
    }
}
```

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_484_0.png)

> 注意：虽然 private 是默认设置，但许多程序员选择显式重申该命令以消除任何歧义。

### 示例 B.49.

```csharp
namespace Appendix_B {
    class BankAccount {
        protected string first_name;
        protected void ReadFiles(ref BankAccount acc) {}
        static void Main() {}
    }
}
```

### 示例 B.50.

```
namespace Appendix_B {
    class BankAccount {
        public string first_name;
        public void ReadFiles(ref BankAccount acc) {}
        static void Main() {}
    }
}
```

## readonly

readonly 是一种常量数据类型，用作声明为字段的类引用的一部分。它在程序中只能在一个位置赋值，之后便充当常量（见示例 B.51）。

### 示例 B.51.

```
class Appendix_B {
    public readonly double variable2 = 3.14159;
    static void Main() {}
}
```

## ref

关键字 ref 用于将变量的控制权反射回原始参数，从而使主调体或调用体能够知道方法（或函数）所做的更改（见示例 B.52）。

### 示例 B.52.

```
class Appendix_B {
    static void Main() {
        int iNumber1 = 0;
        TheRace(ref iNumber1);
    }
    static void TheRace(ref int Num) {}
}
```

## return

关键字 return 用于将单个值传回调用函数。所涉及的值必须是相应类型；在返回类型为 void 的情况下，可以省略。所有非 void 的用户定义函数和方法都需要 return 语句（见示例 B.53）。

### 示例 B.53.

```csharp
using System;
class Appendix_B {
    static void Main() {
        RandomNumber();
    }

    static int RandomNumber() {
        return(0);
    }
}
```

## sbyte

关键字 sbyte 是 8 位整数，用于存储 -128 到 127 范围内的值（见示例 B.54）。

### 示例 B.54.

```csharp
class Appendix_B {
    static void Main() {
        sbyte Number1 = 1;
    }
}
```

## sealed

类一旦被密封，就不能再被继承，因此不能以任何其他方式重写或更改。同理，我们不能将 sealed 与 abstract 修饰符一起使用（见示例 B.55）。

### 示例 B.55.

```csharp
sealed class Appendix_B {
    static void Main() { }
}
```

## short

关键字 short 是 16 位整数数据类型，用于存储 -32,768 到 32,767 范围内的值（见示例 B.56）。

### 示例 B.56.

```csharp
class Appendix_B {
    static void Main() {
        short Number1 = 1;
    }
}
```

## sizeof

sizeof 关键字用于收集与数据类型大小有关的信息。遗憾的是，这还需要使用辅助命令 unsafe，该命令用于标记该代码的不安全性质（见示例 B.57）。

### 示例 B.57.

```csharp
using System;
class Appendix_B {
    static unsafe void Main() {
        Console.WriteLine ("Byte = " + sizeof(byte));
    }
}
```

## stackalloc

关键字 stackalloc（堆栈分配）用于分配从堆栈引用的内存块。这些块的地址存储为指针，并且受到保护而不会被垃圾回收，因此它们不必被固定/钉住。注意：当方法终止时，所有块都会丢失（见示例 B.58）。

### 示例 B.58.

```csharp
class Appendix_B {
    public static unsafe void Main() {
        int* pointer1 = stackalloc int[3];
        pointer1[0] = 1;
    }
}
```

## static

关键字 static 用于修饰构造函数、字段、方法、运算符和属性。例如，静态构造函数会被自动调用，并用于在引用任何成员之前初始化类的其余部分。因此，静态字段不属于特定实例，而是作为单个内存地址被引用。

### 示例 B.59.

```
class Appendix_B {
    static void Main() {}
}
```

## string

字符串（string）是一种引用数据类型，包含较新开发的 Unicode 字符。这些字符可以使用简单的引号赋给字符串引用；这些表达式也可以通过先用 @ 符号标注而成为字面量（见示例 B.60）。

### 示例 B.60.

```
class Appendix_B {
    static void Main() {
        string MyDog = "Brownie";
    }
}
```

## struct

结构（struct）是用户定义的数据类型，允许将相似或相关但没有单一基础数据类型的数据分组。这些组可以包括所有基本值数据类型，以及用于操作这些值的方法列表。结构内声明的数据类型称为结构的成员（或字段），而它们的声明称为结构的实例。这些内部值与结构之间的关联通常由某种共同主题或目的引导。结构由关键字 struct、结构的标记（或名称）、字段列表（写成已声明的成员）以及可能用于操作该数据的方法列表组成。结构通常包含在置于引用命名空间内的单个块中，但如示例 B.61 所示，它们也可以用来调用 main 方法。

请注意，虽然允许使用 C++ 风格的终止分号，但在使用 C# 时并不要求这样做。

### 示例 B.61.

```
struct Appendix_B {
    static void Main() {}
}
```

## switch

switch 语句与 if 和 else-if 语句一样，用于执行与变量值相匹配的语句或语句组。然而，与 if 和 else-if 语句不同，switch 语句不使用比较运算符；相反，它只读取变量的值，并尝试将程序引导到正确的通道。此过程中还会使用第二个关键字 case。关键字 case 在 switch 语句中会被多次编写和使用。每个 case 语句都包含一个用于比较的数值或字符值。如果某个 case 语句持有的值与 switch 语句读取的值匹配，则将执行该 case 语句之后的所有内容。

### 示例 B.62.

```
class Appendix_B {
    static void Main() {
        int Grades = 1;
        switch (Grades) {
            case 1:
                break;
            default:
                break;
        }
    }
}
```

## this

关键字 this 是一种专用引用签名，用于指示所传递类的引用对象；换句话说，它是原本缩写的成员的长写版本。虽然 this 引用是隐含的，但其定义可能会变得含糊，因此应显式包含它以防止此错误（见示例 B.63）。

### 示例 B.63.

```csharp
class Appendix_B {
    protected short pin_number;
    private void ReadFiles() {
        this.pin_number = 1;
    }
    static void Main() {}
}
```

## throw

除了能够捕获一般异常和特定异常之外，我们还可以学习抛出一些自己的异常。对于本书的上下文来说，这通常不是必需的，但该技术有助于澄清一些原本令人困惑的错误的定义（见示例 B.64）。

### 示例 B.64.

```csharp
using System;
public class Appendix_B {
    static void Main() {
        int Y = 0;
        if (Y == 0) {
            throw new DivideByZeroException("\nProgram Error!");
        }
    }
}
```

## true

一种返回 true 值的用户定义布尔类型运算符（见示例 B.65）。

### 示例 B.65.

```csharp
class Appendix_B {
    static void Main() {
        bool Variable1 = true;
    }
}
```

## try

就用户输入而言，我们永远无法保证结果，因此需要提前考虑并规划可能的错误。try 块场景是一种测试应用程序，用于
