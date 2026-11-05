
```csharp
if(collection != null)
{
    item = collection[index];
}
```

### 第 8.3 节：避免 NullReferenceException

```csharp
var person = new Person
{
    Address = null,
};
var city = person.Address.City; //throws a NullReferenceException
var nullableCity = person.Address?.City; //returns the value of null
```

此效果可以链接在一起：

```csharp
var person = new Person
{
    Address = new Address
    {
        State = new State
        {
            Country = null
        }
    }
};
// this will always return a value of at least "null" to be stored instead
// of throwing a NullReferenceException
var countryName = person?.Address?.State?.Country?.Name;
```

### 第 8.4 节：空条件运算符可与扩展方法一起使用

扩展方法可以在空引用上工作，但你仍然可以使用 ?. 进行空值检查。

```csharp
public class Person
{
    public string Name { get; set; }
}
```

```csharp
public static class PersonExtensions
{
    public static int GetNameLength(this Person person)
    {
        return person == null ? -1 : person.Name.Length;
    }
}
```

通常，该方法会在空引用上触发，并返回 -1：

```csharp
Person person = null;
int nameLength = person.GetNameLength(); // returns -1
```

使用 ?. 该方法不会在空引用上触发，且类型为 int？：

```csharp
Person person = null;
int? nameLength = person?.GetNameLength(); // nameLength is null.
```

这种行为实际上是 ?. 运算符的工作方式所期望的：它会避免对空实例进行实例方法调用，以避免 NullReferenceException。然而，相同的逻辑也适用于扩展方法，尽管方法的声明方式不同。

有关第一个示例中为何调用扩展方法的更多信息，请参阅 Extension methods - null checking 文档。

## 第 9 章：nameof 运算符

nameof 运算符允许你以字符串形式获取变量、类型或成员的名称，而无需将其硬编码为字面量。

该操作在编译时求值，这意味着你可以使用 IDE 的重命名功能重命名引用的标识符，名称字符串也会随之更新。

### 第 9.1 节：基本用法：打印变量名

nameof 运算符允许你以字符串形式获取变量、类型或成员的名称，而无需将其硬编码为字面量。该操作在编译时求值，这意味着你可以使用 IDE 的重命名功能重命名引用的标识符，名称字符串也会随之更新。

```csharp
var myString = "String Contents";
Console.WriteLine(nameof(myString));
```

会输出

myString

因为变量的名称是 "myString"。重构变量名会改变该字符串。

如果在引用类型上调用，nameof 运算符返回当前引用的名称，而不是底层对象的名称或类型名称。例如：

```csharp
string greeting = "Hello!";
Object mailMessageBody = greeting;

Console.WriteLine(nameof(greeting)); // Returns "greeting"
Console.WriteLine(nameof(mailMessageBody)); // Returns "mailMessageBody", NOT "greeting"!
```

### 第 9.2 节：引发 PropertyChanged 事件

### 代码片段

```csharp
public class Person : INotifyPropertyChanged
{
    private string _address;

    public event PropertyChangedEventHandler PropertyChanged;

    private void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }

    public string Address
    {
        get { return _address; }
        set
        {
            if (_address == value)
            {
                return;
            }

            _address = value;
            OnPropertyChanged(nameof(Address));
        }
    }
}
...
var person = new Person();
person.PropertyChanged += (s,e) => Console.WriteLine(e.PropertyName);
person.Address = "123 Fake Street";
```

### 控制台输出

Address

### 第 9.3 节：参数检查和保护子句

优先使用

```csharp
public class Order
{
    public OrderLine AddOrderLine(OrderLine orderLine)
    {
        if (orderLine == null) throw new ArgumentNullException(nameof(orderLine));
        ...
    }
}
```

而不是

```csharp
public class Order
{
    public OrderLine AddOrderLine(OrderLine orderLine)
    {
        if (orderLine == null) throw new ArgumentNullException("orderLine");
        ...
    }
}
```

使用 nameof 功能使重构方法参数变得更容易。

### 第 9.4 节：强类型 MVC 动作链接

而不是通常的弱类型：

```csharp
@Html.ActionLink("Log in", "UserController", "LogIn")
```

你现在可以使动作链接强类型化：

```csharp
@Html.ActionLink("Log in", @typeof(UserController), @nameof(UserController.LogIn))
```

现在，如果你想重构代码并将 UserController.LogIn 方法重命名为 UserController.SignIn，你无需担心搜索所有字符串出现的位置。编译器会完成这项工作。

### 第 9.5 节：处理 PropertyChanged 事件

### 代码片段

```csharp
public class BugReport : INotifyPropertyChanged
{
    public string Title { ... }
    public BugStatus Status { ... }
}

...

private void BugReport_PropertyChanged(object sender, PropertyChangedEventArgs e)
{
    var bugReport = (BugReport)sender;

    switch (e.PropertyName)
    {
        case nameof(bugReport.Title):
            Console.WriteLine("{0} changed to {1}", e.PropertyName, bugReport.Title);
            break;

        case nameof(bugReport.Status):
            Console.WriteLine("{0} changed to {1}", e.PropertyName, bugReport.Status);
            break;
    }
}
...

var report = new BugReport();
report.PropertyChanged += BugReport_PropertyChanged;

report.Title = "Everything is on fire and broken";
report.Status = BugStatus.ShowStopper;
```

### 控制台输出

> Title changed to Everything is on fire and broken
> 
> Status changed to ShowStopper

### 第 9.6 节：应用于泛型类型参数

### 代码片段

```csharp
public class SomeClass<TItem>
{
    public void PrintTypeName()
    {
        Console.WriteLine(nameof(TItem));
    }
}
```

```csharp
var myClass = new SomeClass<int>();
myClass.PrintTypeName();

Console.WriteLine(nameof(SomeClass<int>));
```

### 控制台输出

TItem
SomeClass

### 第 9.7 节：打印参数名

### 代码片段

```csharp
public void DoSomething(int paramValue)
{
    Console.WriteLine(nameof(paramValue));
}

...

int myValue = 10;
DoSomething(myValue);
```

### 控制台输出

paramValue

### 第 9.8 节：应用于限定标识符

### 代码片段

```csharp
Console.WriteLine(nameof(CompanyNamespace.MyNamespace));
Console.WriteLine(nameof(MyClass));
Console.WriteLine(nameof(MyClass.MyNestedClass));
Console.WriteLine(nameof(MyNamespace.MyClass.MyNestedClass.MyStaticProperty));
```

### 控制台输出

MyNamespace
MyClass
MyNestedClass
MyStaticProperty

## 第 10 章：逐字字符串

### 第 10.1 节：插值逐字字符串

逐字字符串可以与 C#6 中找到的新字符串插值功能结合使用。

```csharp
Console.WriteLine($@"Testing \n 1 2 {5 - 2}
New line");
```

**输出：**

Testing \n 1 2 3
New line

在 .NET Fiddle 上实时演示

正如逐字字符串所期望的，反斜杠被忽略为转义字符。正如插值字符串所期望的，花括号内的任何表达式在插入到该位置的字符串之前都会被求值。

### 第 10.2 节：转义双引号

逐字字符串中的双引号可以通过使用 2 个连续的双引号 "" 来转义，以在结果字符串中表示一个双引号 "。

```csharp
var str = @"""I don't think so,"" he said.";
Console.WriteLine(str);
```

**输出：**

"I don't think so," he said.

在 .NET Fiddle 上实时演示

### 第 10.3 节：逐字字符串指示编译器不使用字符转义

在普通字符串中，反斜杠字符是转义字符，它指示编译器查看下一个字符以确定字符串中的实际字符。（字符转义的完整列表）

在逐字字符串中，没有字符转义（除了 "" 会被转换为 "）。要使用逐字字符串，只需在起始引号前加上 @ 即可。

这个逐字字符串

```csharp
var filename = @"c:\temp\newfile.txt"
```

**输出：**

