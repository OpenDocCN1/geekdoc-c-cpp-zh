

## 4.3 带有实例变量以及 Set 和 Get 方法的 Account 类

在 Account 对象中存储一个名称，并提供程序可以调用的 GetName 方法来从 Account 对象获取名称。

```cs
// 图 4.2: Account.cs
// 一个简单的 Account 类，包含一个私有实例
// 变量 name 和用于设置和获取 name 值的公共方法。
class Account {
    private string name; // 实例变量
    // 在对象中设置账户名称的方法
    public void SetName(string accountName) {
        name = accountName; // 存储账户名称
    }
    // 从对象中检索账户名称的方法
    public string GetName() {
        return name; // 将 name 的值返回给方法的调用者
    }
}
```

> 图 4.2 | 一个简单的 Account 类，包含一个私有变量 name 和用于设置和获取 name 值的公共方法。

### 4.3.2 关键字 class 和类体

类声明从第 5 行开始，内容为：

```
class Account
```

正如第 3 章提到的，每个类声明都包含关键字 `class`，后面紧跟类名——在本例中是 Account。此外，每个类声明通常存储在与类同名且以 .cs 文件扩展名结尾的文件中，因此我们将 Account 类放置在 Account.cs 文件中。类体括在括号内（图 4.2 的第 6 行和第 20 行）。

### 标识符和驼峰命名法（Camel-Case）

类、属性和方法的变量名都是标识标识符，按照惯例，它们都使用我们在第 3 章中讨论的命名方案：

- 类、属性和方法以大写字母开头（即 PascalCase 大驼峰命名）
- 变量名以小写字母开头（即 camel case 小驼峰命名）。

### 4.3.3 类型为 string 的实例变量 name

回顾 1.6 节，类具有属性，这些属性通过实例变量实现。类的对象在其生命周期内携带这些变量。每个对象都拥有类实例变量的副本。通常，类还包含方法和属性。这些内容操作属于该类的特定对象的实例变量。

实例变量位于类声明内部，但在类方法和属性体之外。第 7 行：

```
private string name; // instance variable
```

在 SetName 和 GetName 方法体之外声明了类型为 `string` 的实例变量。如果有许多 Account 对象，每个对象都有自己的 name。由于 `name` 是一个实例，它可以被类的每个方法和属性操作。Account 的调用者——即任何调用该类方法的代码（例如图 4.1 中 AccountTest 的 Main 方法——由于它是私有的（private），因此无法访问该实例变量。然而，调用者可以访问 Account 的公共方法 SetName 和 GetName。这些方法访问私有实例变量。我们将在第 4.5 节更详细地讨论这种“私有变量和公共访问方法”的架构的强大之处。

![](img/57baed2319be0bb1b5f98674846f2711_152_0.png)

#### 良好的编程实践 4.1

我们倾向于在类的顶部列出所有实例变量，这样在类方法和属性使用它们之前，你就能看到变量的名称和类型。你可以在此方法（和属性）声明之外任何地方列出类实例变量，但散布实例变量会导致代码难以阅读。

#### null——String 变量的默认初始值

每个实例都有一个默认初始值——如果你没有指定实例初始值，C# 会提供该值。因此，在程序中使用实例之前，不需要显式初始化它们——除非它们被初始化为除默认值以外的值。`string` 类型实例变量的默认值是 `null`，我们将在第 7 章考虑引用类型时讨论这一点。当你使用 `Console.Write` 或 `Console.WriteLine` 显示包含包含 `null` 值的字符串时，屏幕上不会显示任何文本——这就是为什么在图 4.1 的 Main 方法第 13 行中，第一次调用 Account 的 GetName 时没有显示名称。

### 4.3.4 SetName 方法

让我们过一遍 setName 方法声明的代码（图 4.2，第 10–13 行）：

```cs
public void SetName(string accountName)
{
    name = accountName; // store the account name
}
```

每个方法声明的第一行（第 10 行）是方法头。方法的返回类型（出现在方法名左侧）指定了方法在执行任务后返回给调用者的数据类型。返回类型 `void`（第 10 行）表示 setName 完成了它的任务，它不向其调用方法（在本例中为图 4.1 Main 方法的第 18 行）返回（即给出）任何信息。正如你看到的，Account 方法 GetName 返回了一个值。

### SetName 的参数

我们在 1.6 节中的汽车类比提到，按下汽车油门会向汽车发送一个执行任务的消息——让汽车跑得更快。但汽车应该加速多快呢？踩得越深，汽车加速越快。因此，发送给汽车的消息包含了任务以及帮助汽车执行该任务的信息。这种信息被称为参数（parameter）该值帮助汽车决定加速多快。同样，方法可以需要一个或多个参数，代表它执行任务所需的数据。

MethodName 声明了参数 `accountName`——它接收作为参数传递给它的名称。当图 4.1 中的第 18 行：

```
myAccount.setName(theName); // put theName in myAccount object
```

执行时，括号中的参数值（即存储在 `theName` 中的值）被复制到方法头中的对应参数 `accountName` 中（图 4.2 的第 10 行）。在图 4.1 的示例执行中，我们为 `theName` 输入了 "Jane Green"，因此 "Jane Green" 被复制到 `accountName` 参数中。

### SetName 参数列表

像 `accountName` 这样的参数声明在位于方法名括号后的参数列表中。每个参数必须指定一个类型（例如 `string`）后跟一个名称。当有多个参数时，它们以逗号分隔列表的形式排列，如下：

```
(type name1, type2 name2, ...)
```

方法声明中参数的数量和顺序必须与方法参数列表中参数的数量和顺序匹配。

### SetName 方法体

每个方法体由左括号（图 4.2，第 11 行）和右括号（第 12 行）定义。在大括号内包含一个或多个执行任务的语句。在本例中，第 12 行：

```name = accountName; // store the account name
```

将参数 `accountName` 的值赋值给实例变量 `name`。在第 12 行执行后，方法返回给调用者。

### 参数是局部变量

在第 3 章中，我们声明在特定方法（如 Main）中的变量是局部变量，它们只能在该方法中使用，无法访问其他方法。当方法终止时，局部变量的值就会丢失。方法的参数也是局部变量。

- 2. 行业中通常对 SetName 方法参数 `accountName` 和实例变量 `name` 使用相同的名称。我们将在 10.4 节介绍如何这样做。

### 4.3.5 GetName 方法

GetName 方法（第 16–19 行）：

```cs
public string GetName()
    return name; // returns name's value to this method's caller
}
```

向调用者返回特定对象的名称——根据方法的返回类型指定的字符串。该方法有一个空参数列表，因此它执行任务不需要额外信息。当调用返回类型非 void 的方法并完成任务时，它必须返回一个结果。调用 Account 对象的语句期望接收 Account 的名称。例如，图 4.1 第 21 行的语句：

```
Console.WriteLine("myAccount name is: {myAccount.GetName()}");
```

使用 GetName 返回的值来输出存储在对象中的名称。

### 4.3.6 访问修饰符 private

`private` 关键字（图 4.2 的第 7 行）：

```
private string name; // instance variable
```

是一个访问修饰符。实例变量 `name` 设置为私有，表示它仅对 Account 类的方法（以及其他成员，如你将在后续看到的属性）可见。这被称为信息隐藏——实例变量 `name` 被隐藏，并且只能在 Account 类的方法（SetName 和 GetName）中使用。大多数实例变量都声明为私有。
该类还包含 `public` 访问修饰符（第 10 行）：

```
public void SetName(string accountName)
```

以及第 16 行
声明为公共的方法（以及其他类成员）是“公开的”。它们可以被：

- 声明所在类的方法或其他成员使用
- 该类的调用者使用——即任何其他类的方法或其他成员（在本应用中，AccountTest 类的 Main 方法是该类的调用者）。

在第 11 章，我们将引入 `protected` 访问修饰符。

# 类成员的默认访问权限

默认情况下，类中的所有内容都是私有的（private），除非你通过提供访问修饰符另行指定。因此，在程序中使用实例之前，不需要显式初始化它们——除非它们被初始化为除默认值以外的值。

