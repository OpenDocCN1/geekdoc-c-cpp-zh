
方法声明首先说明了方法的访问级别。在这里，我们将方法声明为 `public`，以便该方法在程序的任何处都是可访问的（而不仅仅是在 `Staff` 类内部）。

接下来，我们指定方法的返回类型。方法在执行任务后可能会返回特定的结果。如果方法不返回任何结果，我们像示例中那样使用 `void` 关键字。

最后，我们指定方法的名称（示例中为 `PrintMessage`）。

方法名后的括号 `()` 是我们包含方法参数的地方。参数是传递给方法以执行其任务的数据的命名数据。如果方法不需要数据（如示例所示），我们只需要在方法名后添加一对空括号即可。

声明方法后，我们在随后的大括号内定义它的功能。这被称为实现方法 `implementing the method`。在我们的示例中，`PrintMessage()` 方法简单地打印行“Calculating Pay...”

这就是 `PrintMessage()` 方法的全部内容。

接下来，让我们转向一个更复杂的方法。此方法计算每个员工的工资并返回计算结果。在 `Staff` 中添加以下代码：

```csharp
public int CalculatePay()
{
    PrintMessage();
    int staffPay;
    staffPay = hworked * hourlyRate;
    if (hworked > 0)
        return staffPay;
    else
        return 0;
}
```

该方法声明为 `public int CalculatePay()`。`int` 关键字表示此方法返回一个 `int` 类型的值。

在大括号内部，我们有语句 `PrintMessage();`。这被称为调用 `PrintMessage()` 方法。当程序运行到这条语句时，它将首先执行 `PrintMessage()` 方法并打印行“Calculating Pay...”

接下来，我们声明一个局部变量 `staffPay`，并将 `hworked` 和 `hourlyRate` 的乘积赋值给它。方法可以访问类中声明的所有字段和属性。此外，它还可以声明自己的变量。这些被称为局部变量，仅存在于方法内部。示例中的 `staffPay` 就是一个例子。

在分配 `staffPay` 后，我们使用 `if` 语句来确定方法应该返回什么结果。方法通常至少有一个 return 语句。`return` 是一个用于从方法返回答案的关键字。方法中可以有多个 return 语句。然而，一旦方法执行了 return 语句，方法就会退出。

在我们的示例中，如果 `hworked` 大于零，程序将执行语句：

```csharp
return staffPay;
```

并退出方法。这个返回值可以赋值给变量。例如，如果 `hworked` 是 10 且 `hourlyRate` 是 20，我们可以使用语句：

```csharp
int pay = CalculatePay();
```

将 `CalculatePay()` 的结果赋值给变量 `pay`。此时 `pay` 的值将为 200。

另一方面，如果 `hworked` 小于等于零，程序将执行语句：

```csharp
return 0;
```

并退出方法。`pay` 的值将为 0。

## 重载 Overloading

在 C#（以及大多数其他语言）中，只要签名不同，你就可以创建同名的方法。这被称为重载。方法的签名指的是方法的名称以及它拥有的参数。

在 `CalculatePay()` 方法下方添加以下方法：

```csharp
public int CalculatePay(int bonus, int allowance)
{
    PrintMessage();
    if (hworked > 0)
        return hworked * hourlyRate + bonus + allowance;
    else
        return 0;
}
```

第一个方法的签名是 `CalculatePay()`，而第二个方法的签名是 `CalculatePay(int bonus, int allowance)`。

第二个方法有两个参数——`bonus` 和 `allowance`。它通过将这两个参数的值加到 `hworked` 和 `hourlyRate` 的乘积上来计算员工的工资。

## ToString() 方法

最后，在进入下一个节之前，我们需要再写一个方法 - `ToString()` 方法。

`ToString()` 方法是一个特殊的方法，它返回一个表示当前类的字符串。在 C# 中，所有类都带有一个预定义的 `ToString()` 方法。然而，按照惯例（这是我们被我们的），我们会重写这个方法。重写此方法简单意味着编写我们自己的方法版本。

通常，我们编写的 `ToString()` 方法会显示类的字段和属性的值。将以下代码添加到 `staff` 类中：

```csharp
public override string ToString()
{
    return "Name of Staff " + nameOfStaff + ", hourlyRate = " + hourlyRate + ", " + hWorked;
}
```

如你所见，`ToString()` 方法返回一个字符串类型。它包含的字符串包含了 staff 类的信息。方法声明中的 `override` 关键字表示此方法重写了默认方法。我们将在下一章讨论更多关于 `override` 关键字。

### 构造函数

现在，让我们来看构造函数。

构造函数是一个特殊的方法，用于从类模板“构造”对象。每当我们从类中创建对象时，它是第一个被调的方法。构造函数通常用于初始化类的字段。

构造函数的名称始终与类相同（在我们的案例中为 `Staff`），并且不返回任何值。声明构造函数时不需要使用 `void` 关键字。

将以下几行添加到我们的 `Staff` 类。

```csharp
public Staff(string name)
{
    nameOfStaff = name;
    Console.WriteLine("\n" + nameOfStaff);
    Console.WriteLine("-");
}
```

在这个构造函数中，我们首先用传递构造函数的字符串（`name`）初始化字段 `nameOfStaff`。然后我们在屏幕上显示 `nameOfStaff` 的值，并用一系列连字符对其加上下划线。

与其他方法一样，只要签名不同，我们就可以有多个构造函数。我们可以为类类添加另一个构造函数。

```csharp
public Staff(string firstName, string lastName)
{
    nameOfStaff = firstName + " " + lastName;
    Console.WriteLine("\n" + nameOfStaff);
    Console.WriteLine("--------------------");
}
```

这个构造函数有两个参数 - `firstName` 和 `lastName`。第一行将两个字符串连接起来并将结果字符串赋值给 `nameOfStaff`。接下来两行在屏幕上打印 `nameOfStaff` 并用一系列连字符对其加上下划线。

声明构造函数是可选的。如果你不声明自己的构造函数，C# 会自动为你创建一个。默认构造函数简单地将类中的所有字段初始化为默认值，通常对于数值字段为 0，对于字符串字段为空字符串。

## 实例化对象

现在我们已经知道如何创建类，让我们看看如何利用该类来创建对象。这个过程被称为实例化对象。对象也被称为实例。

回顾一下，我们的 `Staff` 类具有以下组件：

### 字段

```csharp
private const int hourlyRate
private string nameOfStaff
private int hWorked
```

### 属性

```csharp
public int HoursWorked
```

### 方法

```csharp
public void PrintMessage()
public int CalculatePay()
public int CalculatePay(int bonus, int allowance)
public override string toString()
```

### 构造函数

```csharp
public Staff(string name)
public Staff(string firstName, string lastName)
```

我们将在 `Program` 类的 `Main()` 方法中实例化一个 `Staff` 对象。

实例化对象的语法是：

`ClassName objectName = new ClassName(arguments);`

将以下几行添加到 `Program` 类的大括号内部。

`int pay;`

```csharp
staff1 = new Staff("Peter");
staff1.HoursWorked = 160;
pay = staff1.CalculatePay(1000, 400);
Console.WriteLine("Pay = {0}", pay);
```

在这里，我们使用第一个构造函数（带有一个参数）来创建我们的 `staff1` 对象。

一旦创建了对象，我们就可以使用对象名称后的点运算符（`.`）访问 `Staff` 类中的任何公共字段、属性或方法。注意，我们需要在这里使用点运算符，因为我们正尝试从 `Program` 类访问 `Staff` 类的成员。当我们想要从另一个类访问字段、属性或方法时，点运算符是必须的。

如果你正在访问同一个类的成员，则不需要使用点运算符。一个例子是我们之前从 `CalculatePay()` 方法中调用 `PrintMessage()` 方法。我们没有使用点运算符，因为这两个方法都来自同一个类。

创建我们的 `staff1` 对象后，下一行显示了我们如何使用公共 `EmployeeType` 属性来给 `worked` 字段赋值。

`staff1.HoursWorked = 160;`

如果我们尝试通过编写

`staff1.hworked = 160;`

直接访问私有字段 `hworked`，我们将得到一个错误，因为 `hworked` 是私有字段，因此只能在 `Staff` 类内部访问。

要调用 `CalculatePay()` 方法，我们写：

```csharp
staff1.CalculatePay(1000, 408);
```

由于我们在括号内有数字 1000 和 400，我们正在使用第二个 `CalculatePay()` 方法。我们把值 1000 和 400 分别传递给参数 `bonus` 和 `allowance`。我们传递的值被称为参数 `arguments`。程序随后使用这些值。

## Static 关键字

我们已经涵盖了一些非常好的概念。在本节中，我们将看看另一个在创建对象时有时使用的关键字。

以前，我们查看了如何创建 `staff1`、`staff2` 和 `staff3` 对象。然而，某些类或成员不需要创建对象就可以访问。这些被称为静态类或成员，并使用 `static` 关键字声明。

考虑以下类：

```csharp
class MyClass
{
    // 非静态成员
    public string message = "Hello World";
    public string Name { get; set; }
    public void DisplayName()
    {
        Console.WriteLine("Name = {0}", Name);
    }
    // 静态成员
    public static string greetings = "Good morning";
    public static int Age { get; set; }
    public static void DisplayAge()
    {
        Console.WriteLine("Age = {0}", Age);
    }
}
```

`MyClass` 包含一个非静态字段 `message`、一个非静态属性 `Name` 和一个非静态方法 `DisplayName()`。

它还包含一个静态字段 `greetings`、一个静态属性 `Age` 和一个静态方法 `DisplayAge()`。

要从另一个类访问 `MyClass` 的静态成员，我们需要像以前一样实例化对象：

```csharp
MyClass classA = new MyClass();
Console.WriteLine(classA.message);
classA.Name = "Jamie";
classA.DisplayAge();
```

然而，要访问静态成员，我们不需要创建任何对象。只需使用类名访问它们，如下所示：

```csharp
Console.WriteLine(MyClass.greetings);
MyClass.Age = 39;
MyClass.DisplayAge();
```

如果你运行上面的代码，将得到以下输出：

```
Hello World
Name = Jamie
Good morning
Age = 39
```

除了拥有静态方法、字段、属性和构造函数，我们还可以拥有静态类。静态类只能包含静态成员。示例所示：

```csharp
static class MyStaticClass
{
    public static int a = 0;
    public static int B{get; set;}
}
```

C# 中的一些预写类被声明明为静态类 `static classes`。例如 `Console` 类。在使用 `Console` 类中的方法时，我们不需要创建 `Console` 对象。我们只需要编写 `Console.WriteLine("Hello World");` 即可。

## 高级方法概念

现在你已经熟悉了类，让我们进入关于类中方法声明和使用的一些高级概念。这些概念更为复杂，可能需要阅读多次才能完全理解。

## 使用数组和列表

之前，我们学习了如何使用 `int` 和 `float` 等基本数据类型作为参数。除了使用基本数据类型外，我们还可以使用数组和列表。

要将数组作为参数，我们需要在方法声明的参数数据类型后面添加方括号 `[]`。示例如下：

```csharp
public void PrintFirstElement(int[] a)
{
    Console.WriteLine("The first element is {}.\n", a[0]);
}
```

要调用此方法，我们需要声明一个数组并将其作为参数传递给方法：

```csharp
int[] myArray = {1, 2, 3, 4, 5};
PrintFirstElement(myArray);
```

下一个示例显示了我们如何使用列表作为参数：

```csharp
public void PrintFirstElement(List<int> a)
{
    Console.WriteLine("The first list element is {}.\n", a[0]); own}
```

要调用此方法，我们需要声明一个列表并将其作为参数传递给方法。

```csharp
List<int> myList = new List<int>{1, 2, 3};
PrintFirstElement(myList);
```

除了将数组或列表作为方法的参数外，我们还可以从方法返回数组或列表。要从方法返回数组，我们需要在方法声明的返回类型后面添加方括号 `[]`。

```csharp
public int[] ReturnUserInput()
{
    int[] a = new int[3];
    for (int i = 0; i < a.length; i++) {
        Console.Write("Enter an integer: ");
        a[i] = Convert.ToInt32(Console.ReadLine());
        Console.WriteLine("Integer added to array.\n");
    }
    return a;
}
```

要使用此方法，我们需要声明一个数组并将方法的结果赋值给它。

```csharp
int[] myArray2 = ReturnUserInput();
```

要从方法返回列表，我们使用方法声明中使用 `List<>` 关键字作为返回类型。示例下：

```csharp
public List<int> ReturnUserInputList()
{
    List<int> a = new List<int>();
    int input;
    for (int i = 0; i < 3; i++) {
        Console.Write("Enter an integer: ");
        input = Convert.ToInt32(Console.ReadLine());
        Console.WriteLine("Integer added to list.\n");
        a.Add(input);
    }
    return a;
}
```
