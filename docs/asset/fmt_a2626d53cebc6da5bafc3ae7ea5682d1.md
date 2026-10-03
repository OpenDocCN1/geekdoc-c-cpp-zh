
这方便地为我们提供了一个机会，选择一个枚举并观察`Debug.Log()`向控制台（Console）面板发送不同的字符串。

```csharp
public MyCases cases;
void Update ()
{
    switch (cases)
    {
        case MyCases.first:
            Debug.Log("first case");
            break;
        case MyCases.second:
            Debug.Log("second case");
            break;
    }
}
```

请注意`switch`语句参数中使用了哪个变量，这很重要。常见的错误是在`switch(MyCases)`中在参数里使用了类型（类型名）。这显然无法按预期方式工作。在这里我们会得到以下错误：

`Assets/SwitchStatements.cs(21,25): error CS0119: Expression denotes a 'type', where a 'variable', 'value' or 'method group' was expected`

每个`case`语句在下一个`case`出现之前必须有一个`break;`。你可以在`case`和`break`之间放置任意数量的语句，但必须在结束处进行`break`。这可以防止每个`case`相互流向下一个。如果你忘记在第一个`case`语句后添加`break`，你就会得到以下错误：

`Assets/SwitchStatements.cs(21,17): error CS0163: Control cannot fall through of one case to another`

添加这些`break`很容易，但至少它会告知我们漏掉了一个。然而，它会将我们引向`switch`语句的开头。确保每个`case`的末尾都有`break`语句取决于你。在`default` case之后也是必须的。

通常情况下，`default`标签是系列`case`标签末尾最后一个`case`。但并不是强制要求的。你可以在`switch`语句的任何地方编写`default`标签。风格指南通常要求你将`default`放在`switch`的最末。如果不这样做，如果程序员看到位置不当的`default`标签，可能会招来一些严厉的批评。

## 6.7.3 我们学到了什么

`switch`语句是一种常见的组合。每个标签都非常清晰，`switch`的参数也非常清晰。我们知道自己期望什么，也显然知道在什么条件下写`case`。

```csharp
enum cases {
    firstCase,
    secondCase,
    thirdCase
}
cases MyCases;
```

上面的枚举可能相当刻意，但我们知道如果在`switch`中使用它，需要多少个标签。显而易见，我们的第一个`case`标签应该看起来像`case cases.firstCase:`，并且我们应该顺序填充剩余的`case`语句。`switch`语句限制于选择不同类型的数据。

```csharp
float f = 2.0f;
switch (f)
{
    case f < 1.0f:
        Debug.Log("less than 1.0f");
        break;
    case f > 3.0f:
        Debug.Log("more than 3.0f");
        break;
    default:
        Debug.Log("neither case");
        break;
}
```

上面的代码看起来可能有效，但我们会得到以下错误：

`Assets/Test.cs(15,1): error CS0151: A switch expression of type 'float' cannot be converted to an integral type, bool, char, string, enum or nullable type`

`switch`仅允许使用“整型、`bool`、`char`、`string`、`enum`或可空”类型的数据。我们尚未涵盖其中一些不同的数据类型，但至少我们知道什么是数据类型。我们知道可以使用`int`和`enum`。在大多数情况下，这应该足够了。

当根据参数需要发生且仅发生至少一件事时，应该使用`switch`语句。

```csharp
int a = 0;
int b = 1;
switch (a)
{
    case 0:
        switch (b)
        {
            case 1:
                Debug.Log("might not be worth it");
                break;
        }
        break;
}
```

在另一个`switch`语句的某个`case`中嵌套`switch`语句并不常见。虽然没有什么真正能阻止你这样做，但寻找一个优雅的解决方案可能更好。

```csharp
void Update ()
{
    int a = 0;
    switch (a)
    {
        case 0:
            FirstFunction();
            break;
        case 1:
            SecondFunction();
            break;
    }
}

void FirstFunction()
{
    Debug.Log("first case");
}

void SecondFunction()
{
    Debug.Log("second case");
}
```

在每个`case`中使用函数是保持整洁的简单方法，尽管并不总是清楚里面写了什么。任何阅读代码的人都被迫在`switch`和不同函数之间来回跳转。然而，这意味着你可能可以在每个函数内部创建`switch` case。

```csharp
void Update ()
{
    int a = 0;
    switch (a)
    {
        case 0:
            FirstFunction();
            break;
        case 1:
            SecondFunction();
            break;
    }
}

void FirstFunction(int a)
{
    switch (a)
    {
        case 0:
            Debug.Log("first case");
            break;
        case 1:
            Debug.Log("second case");
            break;
    }
}

void SecondFunction()
{
    Debug.Log("second case");
}
```

在上面的示例中，我们的第一个条件在第二个条件之前可能会有一些额外的代码。这在视觉上可能是有意义的跳转到第一个条件，执行某些指令，贯穿到下一个`case`，执行更多指令，然后跳出。然而，这种行为在 C# 中是不允许的。为了实现描述的内容，我们需要更加显式。

## 6.7.5 goto Case

```cs
switch (condition)
{
    case first_condition:
        //位置不当的代码
        goto case second_condition;
    case second_condition:
        //做其他事情
        break;
    case third_condition:
        //做另一件事情
        break;
}
```

使用`goto`关键字允许我们从`switch`语句中的一个`case`跳到另一个。这允许实现预期的类似贯穿（fall-through）的行为，同时也赋予了跳转到`switch`语句内部任何其他`case`的额外功能。

```cs
switch (condition)
{
    case first_condition:
        //先做一些事情
        goto case third_condition;
    case second_condition:
        //做其他事情
        break;
    case third_condition:
        //做另一件事情
        goto case second_condition;
}
```

上述语句的实用性是有待商榷。虽然语句是有效的，但它几乎不是任何程序员想要阅读的内容。撇开坏习惯不谈，你会在别人的代码中看到这个，它很可能是不熟悉原始代码的人编写的一种变通方案。

除了笨拙和奇怪的逻辑外，确保`switch` case最终指向`break`是重要的，否则我们会被无限地留在`switch`语句中。调试这样的语句很困难，因此最好避免在`switch`语句中停留的时间超过所需的长度。

在`switch`内部工作时，奇怪且不常见的做法并不常见，因为`switch`语句的常规用法非常简单。如果你需要执行一些更巧妙的操作，最好让`switch`语句指向一个带有额外逻辑的函数，以处理更特定的条件集。

## 6.7.6 局限性

`switch`语句仅限于整数类型（integral types），也就是说，我们只能使用定义明确的类型。这些是整数类型，而`float`或`double`不是整数类型。
