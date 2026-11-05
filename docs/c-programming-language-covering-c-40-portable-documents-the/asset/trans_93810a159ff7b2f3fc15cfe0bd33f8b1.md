
当表达式引用一个只读字段时，该字段的值要到运行时才会被获取。请考虑一个由两个独立程序组成的应用程序：

```csharp
using System;
namespace Program1
{
    public class Utils
    {
        public static readonly int X = 1;
    }
}

namespace Program2
{
    class Test
    {
        static void Main() {
            Console.WriteLine(Program1.Utils.X);
        }
    }
}
```

Program1 和 Program2 命名空间表示两个分别编译的程序。由于 Program1.Utils.X 被声明为静态只读字段，Console.WriteLine 语句输出的值在编译时是未知的，而是在运行时获取。因此，如果 X 的值被更改并且 Program1 被重新编译，即使 Program2 未被重新编译，Console.WriteLine 语句也会输出新值。然而，如果 X 是一个常量，则 X 的值会在 Program2 编译时获取，并且在 Program2 重新编译之前不会受到 Program1 更改的影响。

> **BILL WAGNER** 这一讨论证明了为何只读字段通常应优先于 const。

> **JON SKEET** 我 largely 同意 Bill 的观点，即只读字段通常应优先使用，但在某些情况下 const 也有好处。由常量构成的表达式可以在编译时求值，而不是在每次访问时重新计算。对于计算字符串常量的情况，这种做法还可以避免每次求值表达式时都创建新的字符串。有些数字确实是自然常量，例如一秒中的毫秒数，或 int 的最小值。例如。当绝对没有值会 ever 改变的可能时，const 才有意义。当有任何疑问时，只读更安全。

## 10.5.3 易失字段

当字段声明包含 volatile 修饰符时，该声明引入的字段为易失字段。

对于非易失字段，重新排序指令的优化技术可能导致在多线程程序中出现意外且不可预测的结果，这些程序在没有同步的情况下访问字段，例如 lock 语句 (§8.12) 提供的同步。这些优化可以由编译器、运行时系统或硬件执行。对于易失字段，此类重新排序优化受到限制：

- 对易失字段的读取称为易失读取。易失读取具有“获取语义”；也就是说，它保证在指令序列中其后出现的任何内存引用之前发生。
- 对易失字段的写入称为易失写入。易失写入具有“释放语义”；也就是说，它保证在指令序列中写入指令之前的任何内存引用之后发生。

这些限制确保所有线程都会按执行顺序观察任何其他线程执行的易失写入。符合规范的实现不需要为所有执行线程所见的易失写入提供单一的总排序。易失字段的类型必须是以下之一：

- 引用类型。
- 类型 byte、sbyte、short、ushort、int、uint、char、float、bool、System.IntPtr 或 System.UIntPtr。
- 枚举类型，其枚举基类型为 byte、sbyte、short、ushort、int 或 uint。

示例

```csharp
using System;
using System.Threading;
class Test
{
    public static int result;
    public static volatile bool finished;
    static void Thread2() {
        result = 143;
        finished = true;
    }
    static void Main() {
        finished = false;
        // Run Thread2() in a new thread
        new Thread(new ThreadStart(Thread2)).Start();
    }
}
```

```
// Wait for Thread2 to signal that it has a
// result by setting finished to true
for (;;) {
    if (finished) {
        Console.WriteLine("result = {0}", result);
        return;
    }
}
}
```

产生以下输出：

result = 143

在此示例中，方法 Main 启动一个新线程运行方法 Thread2。此方法将值存储到名为 result 的非易失字段中，然后将 true 存储到易失字段 finished 中。主线程等待字段 finished 被设置为 true，然后读取字段 result。由于 finished 已被声明为易失，因此主线程必须从字段 result 读取值 143。如果字段 finished 未被声明为易失，则允许对 result 的存储在主线程中对 finished 的存储之后才可见，从而导致主线程从字段 result 读取值 0。将 finished 声明为易失字段可防止任何此类不一致。

> JOSEPH ALBAHARI 始终在 lock 语句 (§8.12) 内访问的字段无需使用 volatile 关键字声明。因此，运行时必须确保 Monitor.Enter 和 Monitor.Exit 之间使用的字段的任何排序优化不会扩展到这些语句的范围之外。

> JON SKEET 无锁并发代码很难写对。易失性的精确保证很难推理，使得在阅读代码时很难明显看出代码是否真正正确。我倾向于将低级无锁代码的细节留给专家，而更喜欢基于专家编写的高级库构建。当然，规范详细说明行为对这些专家是有益的。

## 10.5.4 字段初始化

字段的初始值，无论是静态字段还是实例字段，都是该字段类型默认值 (§5.2)。在该默认初始化发生之前，不可能观察到字段的值；因此字段永远不会“未初始化”。示例

```csharp
using System;

class Test
{
    static bool b;
    int i;

    static void Main() {
        Test t = new Test();
        Console.WriteLine("b = {0}, i = {1}", b, t.i);
    }
}
```

产生输出

```
b = False, i = 0
```

因为 b 和 i 都自动初始化为默认值。

## 10.5.5 变量初始化器

字段声明可以包含变量初始化器。对于静态字段，变量初始化器对应于在类初始化期间执行的赋值语句。对于实例字段，变量初始化器对应于在创建类的实例时执行的赋值语句。

示例

```csharp
using System;

class Test
{
    static double x = Math.Sqrt(2.0);
    int i = 100;
    string s = "Hello";

    static void Main() {
        Test a = new Test();
        Console.WriteLine("x = {0}, i = {1}, s = {2}", x, a.i, a.s);
    }
}
```

产生输出

```
x = 1.4142135623731, i = 100, s = Hello
```

因为当静态字段初始化器执行时会对 x 进行赋值，而当实例字段初始化器执行时会对 i 和 s 进行赋值。

§10.5.4 中描述的默认值初始化适用于所有字段，包括具有变量初始化器的字段。因此，在类初始化时，该类中的所有静态字段首先初始化为其默认值，然后按文本顺序执行静态字段初始化器。同样，在创建类的实例时，该实例中的所有实例字段首先初始化为其默认值，然后按文本顺序执行实例字段初始化器。

可以观察到具有变量初始化器的静态字段处于其默认值状态，但这作为风格强烈不鼓励。示例

```csharp
using System;
class Test
{
    static int a = b + 1;
    static int b = a + 1;
    static void Main() {
        Console.WriteLine("a = {0}, b = {1}", a, b);
    }
}
```

表现出这种行为。尽管 a 和 b 的定义是循环的，但程序是有效的。它产生输出

```
a = 1, b = 2
```

因为在执行其初始化器之前，静态字段 a 和 b 被初始化为 0（int 的默认值）。当 a 的初始化器运行时，b 的值为零，因此 a 被初始化为 1。当 b 的初始化器运行时，a 的值已经是 1，因此 b 被初始化为 2。

> BILL WAGNER  当静态变量在多个源单元的部分类中声明时，此情况更容易理解。此外，由于您不知道源单元的包含顺序，因此您无法知道哪个变量会先初始化。

### 10.5.5.1 静态字段初始化

类的静态字段变量初始化器对应于按其在类声明中出现的文本顺序执行的赋值序列。如果类中存在静态构造函数 (§10.12)，则静态字段初始化器的执行发生在执行该静态构造函数之前。否则，静态字段初始化器是
