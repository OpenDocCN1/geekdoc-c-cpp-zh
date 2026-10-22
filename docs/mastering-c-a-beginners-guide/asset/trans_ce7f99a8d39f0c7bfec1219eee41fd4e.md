

当需要创建自己的新函数时，能够构建自己的函数可能会很有用。例如，你可以创建一些不属于 Math 类、但又必须使用的数学函数。其中一些函数如下：

```
asinh(x) = log(x + sqrt(x^2 + 1))
acosh(x) = log(x + sqrt(x^2 - 1))
atanh(x) = (log(1+x) - log(1-x))/2
```

## 函数运算

你还可以在表达式中对函数（委托）进行加法或减法运算。如果添加两个函数值，当调用所得到的函数变量时，两个函数都会被执行。这就是所谓的多播委托。你也可以从多播委托中移除某些函数。在下面的示例中，我们添加了两个与 `Action<string>` 类型匹配的函数：

```
static void Hello(string s)
{
System.Console.WriteLine("Hello, {0}!", s);
}
static void Goodbye(string s)
{
System.Console.WriteLine("Goodbye, {0}!", s);
}
```

这些方法接受一个字符串参数，并且不返回任何内容。下面的代码演示了如何应用委托运算来操作多播委托：

```
Action<string> action = Console.WriteLine;
Action<string> hello = Hello;
Action<string> goodbye = Goodbye;
action += Hello;
action += (x) => { Console.WriteLine(" Greeting {0} from lambda expression", x); };
action("First");  // called WriteLine, Hello, and lambda expression

action -= hello;
action("Second"); // called WriteLine, and lambda expression

action = Console.WriteLine + goodbye
    + delegate(string x) {
Console.WriteLine("  Greeting {0} from delegate", x);
    };
action("Third");  // called WriteLine, Goodbye, and delegate

(action - Goodbye)("Fourth"); // called WriteLine and delegate
```

首先，我们创建了三个委托，分别指向函数 WriteLine、Hello 和 Goodbye。然后，我们将函数 Hello 和新的 lambda 表达式添加到第一个委托上。运算符 `+=` 用于附加将由多播委托调用的新函数。最终，它会

创建一个多播委托，一旦被调用，就会依次调用这三个函数。最后，你会看到如何创建表达式并执行它。在最后一条语句中，表达式 `action – goodbye` 的结果是一个在 action 中不含 Goodbye 函数的函数组合。

## C# 函数式编程

现在，我们可以继续看一些函数式编程的示例。函数可以作为参数传递，这一事实使我们能够构建非常通用的结构。例如，假设你想创建一个泛型函数，用来统计数组中满足某些条件的对象数量。下面的例子展示了这个函数的实现方式：

```
public static int Count<T>(T[] arr,
Predicate<T> condition)
{
    int counter = 0;
    for (int i = 0; i < arr.Length; i++)
        if (condition(arr[i]))

counter++;
    return counter;
}
```

在这个函数中，我们统计数组中满足条件的元素数量。决定条件是否满足的代码并不是硬编码在函数中的，而是作为参数（谓词）传入。这个函数

可以用在各种场景中，例如统计书名超过十个字符的图书数量、价格低于二十的图书数量，或者统计数组中的负数个数。

此外，你还可以使用函数式编程来替换一些标准的 C# 结构。一个典型的例子是使用下面代码块中展示的 using 块：

```
using (obj)
{
obj.DoAction();
}
```

using 块用于可释放对象。在 using 块内，你可以操作该对象、调用某些方法等。当 using 块结束时，该对象会被直接释放。或者，你也可以不直接使用 using 块，而是创建自己的函数来封装要应用于该对象的操作：

```
public static void Use<T>(this T obj,
Action<T> action) where T : IDisposable
{
    using (obj)
    {
action(obj);
    }
}
```

## 高阶函数

将函数作为普通对象使用，使我们可以把它们用作其他函数的参数和返回值。管理其他函数的函数被称为高阶函数。

在使用 LINQ 库时，高阶函数非常常见。例如，如果你想使用某个函数将一个序列转换为新的序列，你会使用类似 Select LINQ 函数的方法：

```
// Apply a function f T1 -> T2 to each
element of data using a List
public static IEnumerable<T2> MySelect<T1,
T2>(this IEnumerable<T1> data, Func<T1,
T2> f)
{
    List<T2> retVal= new List<T2>();
    foreach (T1 x in data) retVal.
Add(f(x));
    return retVal;
}
```

在这个示例中，函数遍历列表，将函数 f 应用于每个元素，把结果放入新列表，然后返回这个集合。通过修改函数 f，你可以使用同一个泛型高阶函数对原始序列进行各种变换。

## 异步函数

函数的重要特性之一是它们可以异步调用，这意味着你可以启动一个函数，继续其他工作，然后在需要结果时等待函数结束。C# 中的每个函数对象都有以下方法：

- **BeginInvoke**：启动函数执行，但不会等待函数完成。
- **IsCompleted**：检查执行是否已完成。
- **EndInvoke**：阻塞当前线程的执行，直到函数完成为止。

下面是一个异步执行函数的示例：

```
Func<int, int, int> f = Klass.SlowFunction;
//Start execution
IAsyncResult async = f.BeginInvoke(5, 3,
null, null); //calls function with
arguments (5,3)
//Check is function completed
if(async.IsCompleted) {
    int result = f.EndInvoke(async);
}
//Finally - demand result
int sum = f.EndInvoke(async);
```

在这个示例中，变量 f 提供了一个对某个计算两数之和的慢速函数的引用。你也可以分别启动调用并传入参数，检查计算是否完成，再显式地获取结果。下面代码块中展示了这类函数的一个示例：

```
public class Klass{
    public static int SlowFunction(int x,
int y){
Thread.Sleep(10000);

return x+y;
    }
}
```

## 带回调的异步函数

在前面的示例中，你已经看到参数被传递给函数，但还有一些额外的参数被设置为 null。这些参数是：

- 回调函数，当函数完成时会被调用。
- 一些会被传递给回调函数的对象。

这样，你就不需要显式检查函数是否已执行——只需传入一个回调函数，它会在函数执行完成时被调用。下面代码演示了一个带回调的调用示例：

```
Func<int, int, int> f = Klass.SlowFunction;
//Start execution
f.BeginInvoke(5, 3, async =>
{
    string arguments = (string)async.AsyncState;
    var ar = (AsyncResult)async;
    var fn = (Func<int, int, int>)ar.AsyncDelegate;
```

> https://hownot2code.com/2016/12/14/functional-programming-in-csharp/
hownot2code

```
int result
    = fn.EndInvoke(async);

Console.WriteLine("f({0}) = {1}",
    arguments, result);

"5,3"
);
```

回调函数（在本例中是 lambda 表达式）接收一个参数 async，其中包含有关异步调用的信息。当你将 lambda 表达式的参数转换为 AsyncResults 时，可以找到原始函数并调用其 EndInvoke 方法。最后，你可以在控制台窗口中将其打印出来。

此外，无需在主代码中显式检查函数是否已完成——只需让它知道函数完成时应该做什么。

## 元组

元组是动态形成所需数据结构的一种绝佳方式。你可以通过将一组属于元组的字段传递给 Tuple 来创建元组。下面展示了一个使用元组的函数示例：

```
Random rnd = new Random();
Tuple<double, double> CreateRandomPoint()
{
    var x = rnd.NextDouble() * 10;
    var y = rnd.NextDouble() * 10;
    return Tuple.Create(x, y);
}
```

该函数会在 10x10 的区域内创建一个随机的 2D 点。

