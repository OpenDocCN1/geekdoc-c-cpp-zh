

![](img/bdd7d3d10cc8dfc1d71aaaf7003fc32b_462_0.png)

Taylor & Francis
Taylor & Francis Group
http://taylorandfrancis.com

## 附录 B：保留标识符定义

### abstract

abstract 是一个用于声明泛型类的修饰符。抽象类不能被实例化，也不能使用 sealed 或 static 修饰符进行修改。只有抽象类可以使用抽象方法和访问器，但从这些类派生的所有非抽象类必须包含这些引用的实现。抽象方法也是隐式虚拟的，其继承的属性可以被重写（参见示例 B.1）。

### 示例 B.1.

```
public abstract class Area {}
class Appendix_B {
    static void Main() {}
}
```

### as

as 是一个用于将表达式转换为数据类型的二进制运算符。它也是在尝试避免异常时非常有用的工具，因为如果转换失败，它会返回 null（参见示例 B.2）。

### 示例 B.2.

```
public class Appendix_B {
    public static void Main() {
        object MyString = new object();
        string s = MyString as string;
    }
}
```

### base

base 是在继承类引用中用于访问基类成员的关键字。它使用关键字 base 后跟该特定成员的定义来区分。一个基类可以作为构造函数、实例和/或使用覆盖修饰符进行访问，但它们不能与 static 修饰符一起使用（参见示例 B.3）。

### byte

byte 是一种无符号 8 位整数数据类型，用于存储范围从 0 到 255 的整数（参见示例 B.6）。

### 示例 B.6.

```
class Appendix_B {
    static void Main() {
        byte Number = 100;
    }
}
```

### case

关键字 case 在 switch 语句内部被多次编写和使用。每个 case 语句保存一个用于比较的数值或字符值。如果 case 语句保存的值与 switch 语句读取的值匹配，则该 case 语句之后的所有内容都将被执行（参见示例 B.7）。

### 示例 B.7.

```
class Appendix_B {
    static void Main() {
        char test = 'A';
        switch (test) {
            case 'A':
                break;
        }
    }
}
```

### catch

catch 语句是 try 块的一部分，用于字面意义上捕获程序在抛出异常时然后可能修复程序。其子句可以包括系统异常、用户定义材料和/或空白或通用 catch。请注意，try 块通常包含多个 catch 语句，其中最具体的语句列在最前面，而空白或通用语句放在最远的位置。如果未按该顺序列出 catch，可能会导致执行较不具体的 catch。也可以在 catch 语句内部重新抛出异常（参见示例 B.8）。

### 示例 B.8.

```
public class Appendix_B {
    static void Main() {
        try {}
        catch {}
    }
}
```

### char

字符引用（char）用于声明 16 位 unicode 字符，其范围从 U+0000 到 U+ffff。Unicode 字符是 16 位字符，用于表示几乎所有已知语言以及大多数，如果不是全部，传统数学和文学符号。char 也用于表示组合值，例如十六进制代码和转义序列（参见示例 B.9）。

### 示例 B.9.

```
class Appendix_B {
    static void Main() {
        char Symbol = 'A';
    }
}
```

### checked

checked 用于监控运算符和语句在整数类型算术运算和转换中发生的数值溢出错误（参见示例 B.10）。

### 示例 B.10.

```
class Appendix_B {
    static void Main() {
        byte Max255 = 254;
        checked{Max255++;}
    }
}
```

### class

类是一种高级数据类型，比简单的字节高出几个层次，但并不太不同。它们类似于数组，但能够保存任务和多种数据类型（更正式地称为标签、字段、方法等）。它们被调用为实例（也可以被视为变量），保存多个信息位。类受修饰符限制和/或增强，并且可以被继承（参见示例 B.11）。

### 示例 B.11.

```
class Appendix_B {
    static void Main() {}
}
```

### const

关键字 constant（const）通知编译器其不变的性质并允许其优化适当的值（参见示例 B.12）。

### 示例 B.12.

```
class Appendix_B {
    static void Main() {
        const int OurVariable = 1;
    }
}
```

### continue

continue 与 break 类似，会缩短其迭代，但而不是结束循环，它只是将循环带回顶部。循环继续进行新的迭代，其他一切也相应继续（参见示例 B.13）。

### 示例 B.13.

```
class Appendix_B {
    static void Main() {
        while (true) {
            continue;
        }
    }
}
```

### decimal

decimal 是一种 128 位数据类型，用于存储有理数和无理数，其范围列为 1.0 × 10<sup>-28</sup> 到 7.9 × 10<sup>28</sup>。其精度水平在 28–29 位有效数字之间，这使其适用于几乎所有货币计算（参见示例 B.14）。

### 示例 B.14.

~~~csharp
class Appendix_B {
    static void Main() {
        decimal Number1, Number2;
        Number1 = 1.0M;
        Number2 = 1.1m;
    }
}
~~~

### default

default 通常放在 switch 语句的末尾，从而允许基于它们与之前任何值都不匹配这一事实来执行所选语句（参见示例 B.15）。

### 示例 B.15.

~~~csharp
using System;
class Appendix_B {
    static void Main() {
        int byNumber = Console.Read();
        switch (byNumber) {
            default:
                break;
        }
    }
}
~~~

### delegate

委托的定义包括公共访问引用、关键字 delegate、委托的标识（也遵循标准命名规则）、数据类型引用及其参数集。委托最常用于处理事件（参见示例 B.16）。

### 示例 B.16.

```
public delegate void TryDelegate();
public class Appendix_B {
    static void Main() {
        TryDelegate();
    }
    public static void TryDelegate() {}
}
```

### do

do 作为 do-while 组合的一部分，允许执行一组语句或块。该块将无限执行，仅在找到 false 表达式时终止。do-while 循环首先执行其块，然后测试并重复，保证在过程终止前至少执行一次（参见示例 B.17）。

### 示例 B.17.

```
class Appendix_B {
    static void Main() {
        do {}
        while (true);
    }
}
```

### double

double 是一种 64 位数据类型，用于存储范围从 ±5.0 × 10³²⁴ 到 ±1.7 × 10³⁰⁸ 的浮点值，其精度水平为 15–16 位数字（参见示例 B.18）。

### 示例 B.18.

```
class Appendix_B {
    static void Main() {
        double Number1, Number2;
        Number1 = 1.0;
        Number2 = 1.1;
    }
}
```

### else

else 是对提问 if 语句的第一个逻辑扩展：它增加了额外的推理行和程序可以遵循的额外路径。else 不能独立使用，但它很容易链接到 if 语句的尾部（参见示例 B.19）。

### 示例 B.19.

```
using System;
class Appendix_B {
    static void Main() {
        double Answer = double.Parse(Console.ReadLine());
        if (Answer == 5)
            Console.WriteLine ("\n That is correct!\n");
        else
            Console.WriteLine("\n Wrong!!!\n");
    }
}
```

### enum

枚举器（enum）是一种基本聚合类型，促进简单的引用操作。它还允许一些独特的引用，例如用户定义的数据结构和对这些声明的赋值列表。初始结构使用关键字 enum 声明，其值实例被声明和分配，就像它们是类引用一样。如果未为这些引用分配值，则初始点为零，每个新组件将自动递增一。然而，我们也可以通过从任意点开始或单独声明每个值来缩短此过程（参见示例 B.20）。

### 示例 B.20.

```
class Appendix_B {
    public enum Months {Jan = 1, Feb, Mar, Apr,
        May, Jun, Jul, Aug, Sep, Oct, Nov, Dec}
    public enum Day {AprilFools = 1, Birthday = 16,
        XMas = 25, Feb29 = 29, NYeve = 31}
    public enum Year {Year2 = 2002, Year3, LeapYear}
    static void Main() {}
}
```
