

常量通常是一个值类型或字符串字面量，因为除了 `string` 之外，创建引用类型的非空值的唯一方法是使用 `new` 运算符，而这是不被允许的。

### 注意！

#### 常量应当是恒定的

在创建常量时，你应确保其值在逻辑上是永远不变的。好的常量应该是那些永远不会改变的事物，例如圆周率的值、猫王出生的年份，或一个摩尔（mol）中包含的物品数量。

如果你需要创建一个具有类似常量行为但使用了常量声明中不允许的类型的字段，可以使用一个 `static` 只读字段代替，方法是同时指定 `static` 和 `readonly` 修饰符。只读字段只能在声明过程中或在构造函数中初始化。

### 亲自动手

### 处理字段

通过按照以下步骤操作，你可以探索如何创建一个包含数据的类，以及如何提供对该数据的访问。如果你已关闭 Visual Studio，请先重复之前的练习。在此练习结束时，请保持 Visual Studio 处于打开状态，因为你稍后仍会使用此应用程序。

- 1. 创建一个新的控制台应用程序。
- 2. 添加一个名为 Contact.cs 的新类文件。在类内部，声明三个私有字段，分别命名为 `firstName`、`lastName` 和 `dateOfBirth`，类型依次为 `string`、`string` 和 `DateTime`。
- 3. 向该类添加以下方法。你将在本小时后面的内容中更深入地了解方法，并在第 8 小时“使用字符串和正则表达式”中更深入地了解 StringBuilder 类：

```csharp
public override string ToString()
{
    StringBuilder stringBuilder = new StringBuilder();
    stringBuilder.AppendFormat("Name: {0} {1}\r\n", this.firstName, this.lastName);
    stringBuilder.AppendFormat("Date of Birth: {0}\r\n", this.dateOfBirth);
    return stringBuilder.ToString();
}
```

- 4. 在 Program.cs 文件的 Main 方法中，输入以下内容：

```csharp
Contact c = new Contact();
Console.WriteLine(c.ToString());
```

- 5. 使用 Ctrl+F5 运行应用程序，并观察输出结果是否与图 3.3 中显示的一致。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_91_0.png)

图 3.3 处理字段

### 属性

如果字段代表状态和数据，但通常都是私有的，那么必须存在一种机制使该类能够公开提供这些信息。了解允许的不同访问级别选项后，你可能会倾向于直接将类字段声明为具有公共访问权限。

这将使我们满足抽象的规则，但随后会违反封装的规则，因为字段可以被直接操纵。那么，如何同时满足封装和抽象的规则呢？我们需要的是某样东西，它可以使用与字段相同的语法来访问，但可以定义比字段本身不同的访问权限。属性使我们能够恰好做到这一点。属性提供了一种简单的方式来访问一个称为**后备字段**的字段，该字段可以公开可用，同时仍然允许隐藏该字段的内部细节。正如字段可以是静态的，属性也可以是静态的，并且不与类的实例相关联。

尽管字段声明变量，需要在内存中存储，但属性不需要。相反，属性通过访问器声明，这些访问器允许你控制值是否可以读取或写入，以及当你这样做时应发生什么。get 访问器允许读取属性值，而 set 访问器允许写入值。

列表 3.2 展示了声明属性的最简单方式。使用这种称为**自动属性**的语法时，你省略后备字段的声明，并且必须始终包含 get 和 set 访问器，且没有声明的实现，这些实现由编译器提供。

#### 列表 3.2 声明自动属性

```csharp
class Contact
{
   public string FirstName
   {
      get;
      set;
   }
}
```

实际上，编译器将列表 3.2 中显示的代码转换为看起来大致如列表 3.3 所示的代码。

#### 列表 3.3 声明属性

```csharp
class Contact
{
    private string firstName;

    public string FirstName
    {
        get
        {
            return this.firstName;
        }
        set
        {
            this.firstName = value;
        }
    }
}
```

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_92_0.png)

#### 自动属性

自动属性很方便，尤其是当你实现大量属性时。然而，这种方便确实带来了一点代价。

因为你不为访问器提供主体，所以无法指定作为该访问器的一部分执行的任何逻辑，并且必须使用自动属性语法声明两个访问器。结果，如果以后某时你意识到需要为任一访问器提供逻辑，你需要添加一个后备字段以及两个访问器的适当逻辑。

幸运的是，这种更改不会影响类的公共接口，因此它是安全的，尽管可能有点繁琐。

get 访问器使用 return 语句，简单地指示访问器返回指示的值。在列表 3.3 代码的 set 访问器中，类字段 firstName 被设置为等于 value，但 value 来自哪里？根据第 1 章中的表 1.6，你知道 value 是一个上下文关键字。当在属性 set 访问器中使用时，value 关键字始终意味着“调用者提供的值”，并且其类型始终与属性类型相同。

默认情况下，属性访问器继承属性定义本身上声明的访问权限。但是，你可以为 get 或 set 访问器声明更具限制性的访问权限。

你还可以创建只读的且没有后备字段的计算属性。这些计算属性是提供从其他信息派生数据的好方法。

列表 3.4 展示了一个计算型 `FullName` 属性，它结合了 `firstName` 和 `lastName` 字段。

#### 列表 3.4 声明计算属性

```csharp
class Contact
{
    private string firstName;
    private string lastName;

    public string FullName
    {
        get
        {
            return this.firstName + " " + this.lastName;
        }
    }
}
```

#### 只读和只写属性

对于显式声明的属性，允许你省略任一访问器。仅包含 `get` 访问器，你创建一个只读属性。若要使用自动属性创建等效的只读属性，你会将 `set` 访问器声明为 `private`。

仅包含 `set` 访问器，或将 `get` 访问器声明为 `private`，你创建一个只写属性。在实践中，应避免使用只写属性。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_93_0.png)

由于属性像字段一样被访问，在访问器中执行的操作应尽可能简单。如果你需要执行更复杂的操作或执行可能耗时或昂贵（消耗资源）的操作，使用方法而不是属性可能更好。

### 亲自动手

### 处理属性

为了修改 `Contact` 类以允许使用属性访问私有数据，并使用自动属性和计算属性，请按照以下步骤操作。如果你已关闭 Visual Studio，请先重复之前的练习。在此练习结束时，请确保保持 Visual Studio 处于打开状态，因为你稍后仍会使用此应用程序。

- 1. 打开 Contact.cs 文件。
- 2. 添加一个新的公共属性，命名为 `DateOfBirth`，允许对 `dateOfBirth` 字段进行读写。
- 3. 移除 `firstName` 和 `lastName` 字段，并创建 `FirstName` 和 `LastName` 属性作为自动属性。
- 4. 添加一个名为 `FullName` 的计算属性，它结合 `FirstName` 和 `LastName` 属性的值。这应与列表 3.4 中显示的计算属性类似。
- 5. 修改 `ToString` 方法，使其使用新的 `FullName` 属性，而不是直接执行字符串拼接。
- 6. 在 `Program.cs` 文件的 `Main` 方法中，在 `Console.WriteLine` 语句之后输入以下代码：

```csharp
c.FirstName = "Jim";
c.LastName = "Morrison";
c.DateOfBirth = new DateTime(1943, 12, 8);
Console.WriteLine(c.ToString());
```

- 7. 使用 Ctrl+F5 运行应用程序，并观察输出结果是否与图 3.4 中显示的一致。

![](img/65e37f12eebfc3bcc97a5a4ae8e15bd3_94_0.png)

### 方法

如果字段和属性定义并实现数据，那么方法（也称为**函数**）定义并实现可以执行的行为或操作。我们在示例和练习中一直使用的 `Console` 类的 `WriteLine` 操作就是一个方法的例子。

列表 3.5 展示了如何向 `Contact` 类添加一个验证电子邮件地址的方法。在这种情况下，`VerifyEmailAddress` 方法指定 `void` 作为返回类型，这意味着它不返回任何值。

