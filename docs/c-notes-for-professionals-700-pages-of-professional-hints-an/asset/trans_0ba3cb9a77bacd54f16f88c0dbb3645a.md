
// Both of these return false
var predicateReturnsFalse = predicate("xyz");
var funcReturnsFalse = func("xyz");

选择使用 Predicate<T> 还是 Func<T, bool> 其实更多是个人偏好问题。Predicate<T> 可以更明确地表达作者的意图，而 Func<T, bool> 可能对更大比例的 C# 开发者来说更为熟悉。

此外，在某些情况下只有其中一个选项可用，尤其是在与其他 API 交互时。例如，List<T> 和 Array<T> 通常在其方法中使用 Predicate<T>，而大多数 LINQ 扩展仅接受 Func<T, bool>。

## Section 96.3: 组合委托（多播委托）

加法 + 和减法 - 操作可用于组合委托实例。委托包含已分配委托的列表。

```
using System;
using System.Reflection;
using System.Reflection.Emit;

namespace DelegatesExample {
    class MainClass {
        private delegate void MyDelegate(int a);
        private static void PrintInt(int a) {
            Console.WriteLine(a);
        }

        private static void PrintType<T>(T a) {
            Console.WriteLine(a.GetType());
        }

        public static void Main (string[] args)
        {
            MyDelegate d1 = PrintInt;
            MyDelegate d2 = PrintType;

            // Output:
            // 1
            d1(1);

            // Output:
            // System.Int32
            d2(1);

            MyDelegate d3 = d1 + d2;
            // Output:
            // 1
            // System.Int32
            d3(1);

            MyDelegate d4 = d3 - d2;
            // Output:
            // 1
            d4(1);

            // Output:
            // True
            Console.WriteLine(d1 == d4);
        }
    }
}
```

在此示例中，d3 是 d1 和 d2 委托的组合，因此调用时程序会同时输出 1 和 System.Int32 字符串。

### 具有非 void 返回类型的委托组合：

如果多播委托具有非 void 返回类型，调用者将收到最后被调用方法的返回值。之前的方法仍会被调用，但其返回值会被丢弃。

```
class Program
{
    public delegate int Transformer(int x);

    static void Main(string[] args)
    {
        Transformer t = Square;
        t += Cube;
        Console.WriteLine(t(2));  // O/P 8
    }

    static int Square(int x) { return x * x; }

    static int Cube(int x) { return x*x*x; }
}
```

t(2) 会先调用 Square 然后调用 Cube。Square 的返回值会被丢弃，而最后方法即 Cube 的返回值会被保留。

## Section 96.4: 安全调用多播委托

是否曾想调用一个多播委托，但希望即使链中任一处发生异常，整个调用列表仍会被调用？那你运气不错，我创建了一个扩展方法正好实现这一点，仅在整个列表执行完成后才抛出 AggregateException：

```
public static class DelegateExtensions
{
    public static void SafeInvoke(this Delegate del, params object[] args)
    {
        var exceptions = new List<Exception>();

        foreach (var handler in del.GetInvocationList())
        {
            try
            {
                handler.Method.Invoke(handler.Target, args);
            }
            catch (Exception ex)
            {
                exceptions.Add(ex);
            }
        }

        if(exceptions.Any())
        {
            throw new AggregateException(exceptions);
        }
    }
}
```

```
public class Test
{
    public delegate void SampleDelegate();

    public void Run()
    {
        SampleDelegate delegateInstance = this.Target2;
        delegateInstance += this.Target1;

        try
        {
            delegateInstance.SafeInvoke();
        }
        catch(AggregateException ex)
        {
            // Do any exception handling here
        }
    }

    private void Target1()
    {
        Console.WriteLine("Target 1 executed");
    }

    private void Target2()
    {
        Console.WriteLine("Target 2 executed");
        throw new Exception();
    }
}
```

输出如下：

```
Target 2 executed
Target 1 executed
```

直接调用，而不使用 SafeInvoke，则只会执行 Target 2。

## Section 96.5: 委托相等性

对委托调用 .Equals() 时按引用相等进行比较：

```
Action action1 = () => Console.WriteLine("Hello delegates");
Action action2 = () => Console.WriteLine("Hello delegates");
Action action1Again = action1;

Console.WriteLine(action1.Equals(action1)) // True
Console.WriteLine(action1.Equals(action2)) // False
Console.WriteLine(action1Again.Equals(action1)) // True
```

这些规则在对多播委托执行 += 或 -= 时同样适用，例如在订阅和取消订阅事件时。

## Section 96.6: 命名方法的底层引用

### delegates

将命名方法分配给委托时，如果满足以下条件，它们将引用同一个底层对象：

- 它们是同一个类实例上的同一个实例方法
- 它们是类上的同一个静态方法

```
~~~csharp
public class Greeter
{
    public void WriteInstance()
    {
        Console.WriteLine("Instance");
    }

    public static void WriteStatic()
    {
        Console.WriteLine("Static");
    }
}

// ...

Greeter greeter1 = new Greeter();
Greeter greeter2 = new Greeter();

Action instance1 = greeter1.WriteInstance;
Action instance2 = greeter2.WriteInstance;
Action instance1Again = greeter1.WriteInstance;

Console.WriteLine(instance1.Equals(instance2)); // False
Console.WriteLine(instance1.Equals(instance1Again)); // True

Action @static = Greeter.WriteStatic;
Action staticAgain = Greeter.WriteStatic;

Console.WriteLine(@static.Equals(staticAgain)); // True
~~~
```

## Section 96.7: 将命名方法分配给委托

命名方法可以分配给具有匹配签名的委托：

```
~~~csharp
public static class Example
{
    public static int AddOne(int input)
    {
        return input + 1;
    }
}
~~~
```

```
`Func<int, int> addOne = Example.AddOne`
```

Example.AddOne 接受一个 `int` 并返回一个 `int`，其签名与委托 `Func<int, int>` 匹配。由于签名匹配，Example.AddOne 可以直接分配给 addOne。

## Section 96.8: 通过 lambda 为委托赋值

Lambda 表达式可用于创建匿名方法以分配给委托：

```
Func<int,int> addOne = x => x+1;
```

请注意，以这种方式创建变量时需要显式声明类型：

```
var addOne = x => x+1; // Does not work
```

## Section 96.9: 在 func 中封装转换

```
public class MyObject{
    public DateTime? TestDate { get; set; }

    public Func<MyObject, bool> DateIsValid = myObject => myObject.TestDate.HasValue &&
myObject.TestDate > DateTime.Now;

    public void DoSomething(){
        //We can do this:
        if(this.TestDate.HasValue && this.TestDate > DateTime.Now){
            CallAnotherMethod();
        }

        //or this:
        if(DateIsValid(this)){
            CallAnotherMethod();
        }
    }
}
```

秉承整洁代码的精神，将如上所示的检查和转换封装为 Func 可以使代码更易于阅读和理解。虽然上面的示例非常简单，如果存在多个 DateTime 属性，每个属性都有各自不同的验证规则，而我们想要检查不同的组合怎么办？简单的一行 Func，每个都有确定的返回逻辑，既可读又能降低代码的表面复杂性。请考虑下面的 Func 调用，并想象方法中会多出多少杂乱的代码：

```
public void CheckForIntegrity(){
    if(ShipDateIsValid(this) && TestResultsHaveBeenIssued(this) && !TestResultsFail(this)){
        SendPassingTestNotification();
    }
}
```

## Section 96.10: 将委托作为参数传递

委托可作为类型化的函数指针使用：

```
class FuncAsParameters
{
    public void Run()
    {
        DoSomething(ErrorHandler1);
        DoSomething(ErrorHandler2);
    }

    public bool ErrorHandler1(string message)
    {
