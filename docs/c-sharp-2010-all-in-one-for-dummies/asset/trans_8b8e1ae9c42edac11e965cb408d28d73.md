
如果`newCourse`返回的对象没有`Schedule`方法会怎样？你会遇到运行时错误。但运行时错误可以用try/catch块来处理。没有`dynamic`关键字，什么都无法让它编译通过。

长期使用Visual Basic的读者，甚至较新的VB.NET程序员，都会意识到在Visual Basic中你可以动态地处理这种情况——而且一直都能。长期以来，我一直建议在遗留系统上工作的程序员使用Visual Basic编写新代码，原因就在于此。

为了语言对等，现在C#也能做到这一点了。总体而言，这是好事，因为许多组织在用VB编写遗留代码，用C#编写新代码——在实战中这可能会变得相当混乱。这一改变让代码库更加精简。

## 使用 Dynamic

当C#遇到一个动态类型的变量（比如我们之前创建的变量）时，它会把该变量所涉及的一切变成动态操作。这种动态转换意味着，当你在表达式中使用动态类型对象时，整个操作都是动态的。

## 经典示例

这里有六个示例说明其工作原理。假设我们有一个动态变量`dynaVariable`。由于这个动态变量会贯穿全部六个示例，它们都将由C#编译器动态调度。以下就是这些示例，感谢Daniel Ng。

- `dynamicVariable.someMethod("a", "b", "c");`：编译器在运行时绑定方法`someMethod`，因为`dynaVariable`是动态的。毫不意外。
- `dynamicVariable.someProperty = 42;`：编译器像第一个方法中那样绑定属性`someProperty`。
- `var newVar = dynamicVariable + 42;`：编译器查找任何重载的"+"运算符（类型为`dynamic`）。如果没有找到，它就输出一个动态类型。
- `int newNumber = dynamicVariable;`：这是对`int`的隐式转换。运行时确定是否可以进行到`int`的转换。如果不能，则抛出类型不匹配错误。
- `int newString = (int) dynamicVariable;`：这是对`int`的显式转换。编译器将其编码为强制转换——这里实际上改变了类型。
- `Console.WriteLine(dynamicVariable);`：由于没有接受`dynamic`类型的`WriteLine`重载，整个方法调用被动态调度。

### 让静态操作动态化

如果编译器选择将静态操作动态化——就像上一节第6条那样——编译器会即时重新构建代码，以便处理动态变量。这对你来说意味着什么？问得好。

让我们看第6条：`Console.WriteLine(dynamicVariable);`。这段代码迫使编译器构建中间代码，在运行时检查变量类型，以找到可写入控制台的内容。编译后的代码首先检查输入是否为其已知的静态类型。接下来，它检查程序中存在的类型。然后它只是尝试几种可能有效的方法。如果什么也没找到，就会因错误而失败。

如果必须这样做，那也没问题。但请记住，它慢得离谱。这就是为什么`Variant`在经典Visual Basic中声名狼藉。Dynamic是你直到需要时才使用的东西。它会给运行程序的机器带来巨大压力，尤其是当所有变量都是动态的时候。

### 了解表象之下发生了什么

让我们直接看一个来自MSDN的示例。微软给出了这个简单的方法：

```csharp
class C
{
    public dynamic MyMethod(dynamic d)
    {
        return d.Foo();
    }
}
```

这相当直白——一个接受`dynamic`类并返回该类型的`Foo`方法结果的方法。没什么大不了的。

以下是编译后的C#代码：

```csharp
class C
{
    [return: Dynamic]
    public object MyMethod([Dynamic] object d)
    {
        if (MyMethodo__SiteContainer0.p__Site1 == null)
        {
            MyMethodo__SiteContainer0.p__Site1 =
            CallSite<Func<CallSite, object, object>>
            .Create(new CSharpCallPayload(
            typeof(object), null, new CSharpArgumentInfo[] {
            new CSharpArgumentInfo(CSharpArgumentInfoFlags.None,
            null) }));
        }
        return MyMethodo__SiteContainer0.p__Site1
            .Target(MyMethodo__SiteContainer0.p__Site1, d);
    }

    [CompilerGenerated]
    private static class MyMethodo__SiteContainer0
    {
        public static CallSite<Func<CallSite, object,
        object>> p__Site1;
    }
}
```

是的，我也这么说。我甚至不打算开始尝试分解这段代码——幸运的是，我们也不必这么做。这就是我们拥有编译器的原因，对吧？

## 了解动态语言运行时

动态语言不仅仅有动态类型。你可以做一些强大的事情。但就像所有力量一样，你必须小心不要误用。

动态语言运行时（Dynamic Language Runtime，见图1-1）是添加到.NET Framework中的一个库，专门用于将动态语言（如Ruby）添加到Visual Studio阵营中（如IRONRuby），或者为现有的静态语言（如C# 4.0）添加动态语言特性。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_802_0.png)

图1-1：动态语言运行时。

该运行时帮助编译器在编译后的程序集中构建代码，以便在运行时做出许多动态选择。上一节末尾的代码块就是最简单类型的一个示例。

DLR协助创建了IRONRuby，使人们可以直接在Visual Studio中使用Ruby（当前热门的动态语言）进行编码。当然，由于DLR使C#能够具备动态语言特性，你在Ruby中能做到的许多事情，现在也可以在C#中做到。

## 动态Ruby

Ruby在其对Trabb Pardo-Knuth算法的实现中利用了其动态根源。不要被这个名字吓到——这只是一个可以用计算机代码解决的简单问题。

程序需要从输入设备读取11个数字——在我们的例子中，使用控制台的`ReadLine`方法。它将数字存储在一个数组中。然后，它用某个函数从后往前处理数组——从最后输入的值开始。如果该值不超过某个任意阈值，就打印结果。

该程序在Ruby中如下所示：

```
class TPK
  def f( x )
    return Math.sqrt(x.abs) + 5*x **3
  end
```

```
def main
  Array.new(11) { gets.to_i }.reverse.each do |x|
    y = f(x)
    puts "#{x} #{(y>400) ? 'TOO LARGE' : y}"
  end
end
```

这不是一本Ruby书，这一点我很清楚。尽管如此，这是我用来举例的最佳动态语言——无可匹敌。

定义了两个函数：`f`和`main`。`main`从控制台接受11个数字，然后将它们转换为整数数组（这就是`gets.to_i`的作用）。对于数组中的每个值，它将`y`设为`f(x)`，然后检查它是否高于我们的任意值。如果是，就打印"TOO LARGE"；否则打印该数字。

动态特性对这个算法为什么重要？其实并不重要。你可以完全使用静态类型来实现。不过，动态部分确实有影响。

首先，`f(x)`不关心`x`是什么。程序假定输入的内容会在`gets.to_i`处转换为整数，但函数本身不关心具体的输入是什么类型。这有好有坏，因为如果我们恰好给它一个字符串或其他类型，它就会失败。

数组本身也没有类型。这可能带来好处，因为如果你知道自己只是要把值写到屏幕上，就可以把不同类型的值放进去。

## 动态C#

当然，C#现在也有类似的功能，对吧？我们应该能做同样的事情！是的，事实上我们确实可以。代码如下：

```
static dynamic f(dynamic x)
{
    return (Math.Sqrt(x) + 5.0 * Math.Pow(x, 3.0));
}
static void Main(string[] args)
{
    dynamic[] array = new Array[11];
    for (int i = 0; i < 11; i++)
    {
        array[i] = Console.ReadLine();
    }
    for (int i = 10; i >=0; i--)
    {
```
