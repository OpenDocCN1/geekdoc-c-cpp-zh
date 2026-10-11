
```csharp
// 将元素推入栈；如果失败，抛出 FullStackException

public void Push(T pushValue)
{
    if (top == elements.Length - 1) // 栈满了
    {
        throw new FullStackException("Stack is full, cannot push");
    }
    top++; // 栈顶增
    elements[top] = pushValue; // 将 pushValue 放在栈上
}
```

**图 2.5** 泛型类 `Stack`。（2 部分的第一部分。）

```csharp
// 如果栈不空则返回栈顶元素，否则抛出 EmptyElementException
public T Pop()
{
    if (top == -1) // 栈为空
    {
        throw new EmptyElementException("Stack is empty, cannot pop");
    }
    top--; // 栈顶减
    return elements[top + 1]; // 返回栈顶值
}
```

![](img/57ed2319be0bb1b5f986748f2711_867_0.png)

当泛型方法被编译型时，编译器会对类的参数进行类型检查，以确保它们可以与泛型类中的代码配合使用。对于值类型，编译器为每个唯一的值类型生成该类的自定义版本；对于引用类型，编译器将生成一个额外的 `Stack`。约束决定了可以在类型参数上执行的操作。对于引用类型，运行时会将类型参数替换为实际类型。对于 `Stack` 来说，没有指定任何类型约束，因此使用了默认的类型约束。泛型类中类型的生存范围是整个类。

## Stack 构造函数

`Stack` 类有两个构造函数。无参数构造函数（第 11–15 行）将默认栈大小（10）传递给单参数构造函数，并使用该语法（第 12 行）来调用同一类中的另一个构造函数。单参数构造函数（第 18–27 行）验证 `stackSize` 参数，并创建一个指定 `stackSize` 的数组（如果大于 0），否则抛出异常。

## Stack Push

`Push` 方法（第 31–41 行）首先确定是否尝试向栈推入一个元素。如果第 35–36 行抛出 `FullStackException`（声明在图 20.6 中），如果栈未满，第 39 行增加计数器以指示新的栈顶位置，第 40 行将参数放置在数组元素的位置。

## Stack Pop

`Pop` 方法（第 45–54 行）首先确定是否尝试从空栈中弹出元素。如果第 49 行抛出 `EmptyStackException`（声明在图 20.7 中）。否则，第 52 行减少计数器以指示新的栈顶位置，第 53 行返回栈的原始栈顶元素。

## FullStackException 和 EmptyStackException 类

`FullStackException`（图 20.6）和 `EmptyStackException`（图 20.7）提供无参数构造函数、一个异常类的单参数构造函数（如第 13.8 节所述）以及一个用于从现有异常创建新异常的双参数构造函数。无参数构造函数设置默认错误消息，而两个构造函数则设置自定义错误消息。

```csharp
// Fig.20.6: FullStackException.cs
// FullStackException 表示栈已满。
using System;
public class FullStackException : Exception
{
    // 无参数构造函数
    public FullStackException() : base("Stack is full")
    {
        // 空构造函数
    }
    // 单参数构造函数
    public FullStackException(string exception) : base(exception)
    {
        // 空构造函数
    }
    // 双参数构造函数
    public FullStackException(string exception, Exception inner) : base(exception)
    {
        // 空构造函数
    }
}
```

**图 20.6** | `FullStackException` 表示栈已满。

```csharp
// Fig.20.7: EmptyStack.cs
// EmptyStack 表示栈为空。
using System;
public class EmptyStack : Exception
{
    // 无参数构造函数
    public EmptyStack() : base("Stack is empty")
    {
        // 空构造函数
    }
    // 单参数构造函数
    public EmptyStack(string exception) : base(exception)
    {
        // 空构造函数
    }
    // 双参数构造函数
    public EmptyStack(string exception, Exception inner) : base(exception)
    {
        // 空构造函数
    }
}
```

**图 20.7** | `EmptyStack` 表示栈为空。

### 演示 Stack 类

现在，让我们考虑一个使用数组的栈（图 20.8）。

```csharp
// Fig.20.8: StackTest.cs
// 测试泛型类。
using System;

class StackTest
{
    // double 类型的数组
    private static double[] doubleElements = { 1.1, 2.2, 3.3, 4.4, 5.5 };
    private static int[] intElements = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

    static void Main()
    {
        Stack<double> doubleStack = new Stack<double>(5);
        Stack<int> intStack = new Stack<int>(10);

        TestPushDouble();
        TestPopDouble();
        TestPushInt();
        TestPopInt();
    }

    // 测试 doubleStack 的 push 方法
    private static void TestPushDouble()
    {
        try {
            Console.WriteLine("\nPushing elements onto doubleStack");
            // 将元素推入栈
            foreach (var element in doubleElements) {
                Console.Write($" {element:F}");
                doubleStack.Push(element); // 推入 doubleStack
            }
        } catch (FullStackException exception) {
            Console.Error.WriteLine("\nmessage: {exception.Message}");
            Console.Error.WriteLine(exception.StackTrace);
        }
    }

    // 测试 doubleStack 的 Pop 方法
    private static void TestPopDouble()
    {
        // 从栈中移除所有元素
        try {
            Console.WriteLine("\nPopping elements from doubleStack");
            double popValue; // 存储从栈移除的元素
            popValue = doubleStack.Pop(); // 从 doubleStack 弹出
            Console.WriteLine($"{popValue:F}");
        } catch (EmptyStackException exception) {
            Console.Error.WriteLine("\nmessage: {exception.Message}");
            Console.Error.WriteLine(exception.StackTrace);
        }
    }

    // 测试 intStack 的 push 方法
    private static void TestPushInt()
    {
        try {
            Console.WriteLine("\nPushing elements onto intStack");
            // 将元素推入栈
            foreach (var element in intElements) {
                Console.Write($" {element}");
                intStack.Push(element); // 推入 intStack
            }
        } catch (FullStackException exception) {
            Console.Error.WriteLine("\nmessage: {exception.Message}");
            Console.Error.WriteLine(exception.StackTrace);
        }
    }

    // 测试 intStack 的 Pop 方法
    private static void TestPopInt()
    {
        // 从栈中移除所有元素
        try {
            Console.WriteLine("\nPopping elements from intStack");
            int popValue; // 存储从栈移除的元素
            popValue = intStack.Pop(); // 从 intStack 弹出
            Console.WriteLine($"{popValue}");
        } catch (EmptyStackException exception) {
            Console.Error.WriteLine("\nmessage: {exception.Message}");
            Console.Error.WriteLine(exception.StackTrace);
        }
    }
}
```

## 20.6 通用类

```csharp
// 将元素推入栈
foreach (var element in intElements)
{
    Console.Write($"{element}");
    intStack.Push(element); // 推入 intStack
}
catch (FullStackException exception)
{
    Console.Error.WriteLine($"\nmessage: {exception.Message}");
    Console.Error.WriteLine(exception.StackTrace);
}
```

```csharp
// 测试 intStack 的 Pop 方法
private static void TestPopInt()
{
    // 从栈中弹出元素
    Console.Error.WriteLine("\npopping elements from intStack");
    int popValue; // 存储从栈中移除的元素
    // 从栈中移除所有元素
    while (true)
    {
        popValue = intStack.Pop(); // 从 intStack 弹出
        Console.Write($"popValue:{popValue}");
    }
}
catch (EmptyStackException exception)
{
    Console.Error.WriteLine("\nmessage: {exception.Message}");
    Console.Error.WriteLine(exception.StackTrace);
}
```

向 `doubleStack` 推入元素

1.1 2.2 3.3 4.4 5.5 6.6

Message: 栈满，无法推入 6.6

At `Stack!1.Push(T pushValue)` in `C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_05_08\Stack\Stack\Test.cs:line 35`

At `Test.TestPopDouble(C)` in `C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_05_08\Stack\Stack\Test.cs:line 39`

从 `doubleStack` 弹出元素

5.5 4.4 3.3 2.2 1.1

Message: 栈为空，无法弹出

At `Stack!1.Pop()` in `C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_05_08\Stack\Stack\Test.cs:line 49`

At `Test.TestPopDouble(C)` in `C:\Users\PaulDeitel\Documents\examples\ch20\Fig20_05_08\Stack\Stack\Test.cs:line 62`

图20.8 | 测试通用类。（4部分中的第部分）

向 `intStack` 推入元素

1 2 3 4 5 6 7 8 9 10 11

Message: 栈满，无法推入 11

at at `Stack.Push(T pushValue)` in `C:\Users\PaulDeitel\Documents\examples\ch20_20_05_08\Stack\Stack.cs:line 35`

at `StackTest.PushInt()` in `C:\Users\PaulDeitel\Documents\examples\ch20_20_05_08\Stack\StackTest.cs:line 85`

从 `intStack` 弹出元素

10 9 8 7 6 5 4 3 2 1

Message: 栈为空，无法弹出

at at `Stack.Pop()` in `C:\Users\PaulDeitel\Documents\examples\ch20_20_05_08\Stack\Stack.cs:line 49`

at `StackTest.PopInt()` in `C:\Users\PaulDeitel\Documents\examples\ch20_20_05_08\Stack\StackTest.cs:line 109`

图 20.8 测试通用栈。（4部分中的第4部分）。

## 方法 TestPushDouble

方法 `PushDouble`（第 28–47 行）调用方法 `Push`，将双精度值 1.1, 2.2, 3.3, 4.4 和 5.5 放入 `doubleElements` 数组中。当程序尝试向 double 推入第6 个值时，语句终止（因为 `doubleStack` 只能存储五个元素）。此时，方法抛出 `FullStackException` (20.6) 表示栈已满。图20.8 的第 42–46 行捕获了该异常并显示消息和堆栈跟踪。堆栈跟踪识别了发生的异常，并显示 `Stack.cs` 的第 35 行由 `Stack` 方法生成了异常。堆栈跟踪还显示 `StackTest.cs` 的第 39 行由 `TestPushDouble` 调用了方法。由于程序捕获了该异常，运行时环境认为异常已处理，程序可以继续执行。

## 方法 TestPopDouble

方法 `Pop`（图20.8，第 50–71 行）使用无限循环从栈中移除所有值。注意输出中，值是按后进先出的顺序弹出的——这是栈的定义特征。当程序尝试弹出第6 个值时，`doubleStack` 为空，因此 `Pop` 方法抛出 `EmptyStackException`。这导致程序进入第 66–70 行的 `catch` 块处理异常，以便程序继续执行。

## 方法 TestPushInt 和 TestPopInt

方法 `PushInt`（第 74–93 行）调用方法 `Push` 将值推入 `intStack` 直到栈满。`PopInt`（第 96–117 行）调用方法 `Pop` 从 `intStack` 移除值直到栈为空。再次，值按后进先出的顺序弹出。

## 创建通用方法到 Stack<T>
