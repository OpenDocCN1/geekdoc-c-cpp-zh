
此外，你将学习更多关于继承的知识并接触接口。你将探索多态如何与面向对象设计相关，并学习使用`.NET`语言进行编程。重载、重写和虚方法的使用等高级特性包含在本章中。

## 面向对象语言特性

一种真正的面向对象编程 (`OOP`) 语言，必须支持以下 `C#` 和 `.NET` 语言采用的主要概念：

- **抽象 (Abstraction)**：语言必须提供管理复杂问题的方法，允许你抽象或识别相关的对象。
- **封装 (Encapsulation)**：语言必须支持将数据属性和行为封装在单元，从而隐藏实现细节。
- **继承 (Inheritance)**：语言必须提供扩展程序单元功能以实现代码复用的特性。
- **多态 (Polymorphism)**：语言必须允许行为有多种实现，以便根据情况执行相应的实现。

基于组件开发 645

面向对象的开发侧重于设计可以在许多应用程序中重用的类。确保这种重用的一种方法是设计和构建组件，这些组件可以存储在库中并在需要时调用。下一节描述了如何通过`.NET`实现这一目标。

## 基于组件开发

在过去，应用程序主要作为单一的、自包含的单体程序进行开发。现在的应用程序是涉及程序员团队开发工作的大型系统。这些应用程序通常需要许多不同的组件打包在一起以响应业务功能。现在的开发通常不是在一个单独文件中编写包含所有功能的程序，而是倾向于编写类似于图 11-1 所示的多程序应用程序。

![](img/45e6f245af31396d967c3186f196d331_678_0.png)

图 11-1 基于组件开发

组件通过 `C#` 中的类来实现。在第 9 章和第 10 章中，你学习了如何设计图形用户界面，这使得创建表示层成为可能。第 15 章为你介绍了 Web 应用程序，它有助于创建另一种类型的表示层，这种层可以通过不同类型的平台的浏览器进行查看。在下一章第 12 章中，你将学习通过编写访问文本文件和数据库（如使用 Microsoft Access 创建的数据库）数据的类来添加数据访问层。你在书中之前章节中完成的所有工作都已为你开发组件中间层的业务逻辑做好了准备。

## 第 11 章 高级面向对象编程特性

面向对象的开发技术非常适合构建应用程序。当你查看图 11-1 时，请将图中的每个组件想象成相互独立的类，它们彼此分离。可以设计这些类，并创建新的子类来扩展原始类的功能。许多不同的应用程序可以通过扩展或将这些类组合成新的应用程序来重用这些类。

在 `C#` 中，除了创建 `EXE` 文件外，你还可以创建带有动态链接库（`DLL`）扩展名的类库文件。这些文件可以成为从任意数量应用程序引用的组件。为了利用面向对象编程的特性，你必须理解的核心概念之一是继承。

### 继承

继承允许你创建一个通用类，然后定义专门的类，这些这些类可以访问通用类的成员。这些新的专门化类可以通过添加它们特有的数据和行为来扩展功能。继承与“is a”（是一个）关系相关联。专门的类是通用类的一种。例如，你可能会创建一个名为 `Person` 的类，并包含身份号、姓名、年龄和家庭地址等数据特征。在使用社会安全号作为身份号的地区，社会安全号就是身份号。可能还包含标题为 `Eat()` 和 `Talk()` 的行为或方法。在定义这些之后，你可以创建如 `Student`（学生）或 `Faculty`（教职工）之类的专门类，它们继承自 `Person` 类。`Student` “是一个” `Person`，就像 `Faculty` “是一个” `Person` 一样。`Student` 可能具有 `ID`、专业和年级等独特的数据特征。通过使用继承，实例化 `Student` 类对象的应用程序不仅具有这些独特特征，还可以访问 `Person` 类的特征（身份号、姓名、年龄和地址）。

![](img/45e6f245af31396d967c3186f196d331_679_0.png)

类也可以具有“has”（拥有有一个）关系，即定义一个类拥有其他类型类的实例。这种概念被称为包含或聚合。当你在 `C#` 中定义实例化 `string` 或 `int` 类对象的类时，你会体验到便利性。然而，“has a”关系通常与用户定义的类相关联。例如，`Person` “有一个” `medicalRecord`（医疗记录）且“有一个” `dentalRecord`（牙科记录）。

### 继承 Object 类

自你在第 1 章编写第一个程序以来，你就一直在创建类了。你学到 `C#` 中创建的每个对象都自动继承自位于 `System` 命名空间的名为 `object` 的基类。`Object` 有四个方法，任何在 `C#` 中编写的继承类只要提供了对 `System` 命名空间的引用，就会继承这四个方法。其中之一的 `ToString()` 方法你已经在许多程序中使用过。图 11-2 使用 IntelliSense（智能感知）显示了 `Object.ToString()` 的签名以及从 `object` 继承的其他方法的名称。

![](img/45e6f245af31396d967c3186f196d331_680_0.png)

图 11-2 继承自 object 方法

## 继承其他 .NET FCL 类

在第 9 章和第 10 章开发基于 Windows 的程序时，你也经历了继承。你创建的 Windows forms 类继承自 `System.Windows.Forms.Form` 类。扩展该类使你能够构建作为该 `.NET Framework` 类一部分的功能。通过添加 `Button`、`Label`、`TextBox` 和 `ListBox` 等类的实例化对象，能够以最少的编程量为你的程序添加功能。要继承 `System.Windows.Forms.Form` 类，需要在你的类定义中添加新条目。图 11-3 说明了当你决定通过从项目类型菜单选择 Windows 应用程序模板来构建 Windows 应用程序时，Visual Studio 如何添加内容的。

图 11-3 派生类

在面向对象的术语中，图 11-3 中冒号后面的类是基类。冒号左侧的 `PresentationGUI` 被称为派生类。要继承基类，使用冒号作为派生类和基类之间的分隔符，如图 11-3 所示。`PresentationGUI` 是用户定义的名称。`Form` 类属于 `System.Windows.Forms` 命名空间。在这个示例中，用户定义的类继承自一个预定义的 `.NET` 类；然而，当用户定义的类继承另一个用户定义的类时，相同的概念也适用。通过使用冒号，你表示 `PresentationGUI` 类派生自 `Form` 类。

### 为继承创建基类

你可以定义自己的类，其他类可以从这些类继承特征。示例 11-1 创建了一个名为 `Person` 的类，具有四个数据成员。该类被用作基类，其他类可以从它继承特征。基类有时称为 super class（超类）或 parent class（父类）。

### 示例 11-1

```
public class Person
{
    private string idNumber;
    private string lastName;
    private string firstName;
    private int age;

    public Person() // 零参数构造函数
    {
        idNumber = "";
        lastName = "unknown";
        firstName = string.Empty;
        age = 0;
    }
    public Person(string id, string lname, string fname, int anAge) // 四个参数构造函数
    {
        idNumber = id;
        lastName = lname;
        firstName = fname;
        age = anAge;
    }
    public Person(string id, string lname, string fname) // 三个参数构造函数
    {
        idNumber = id;
        lastName = lname;
        firstName = fname;
    }
    public Person(string id) // 单个参数构造函数
    {
        idNumber = id;
        lastName = "unknown";
    }
}
```

继承

649

在 11-1 中仅显示了 `Person` 类的数据成员和构造方法。注意，数据成员使用了 `private` 访问修符，而构造函数使用了 `public` 访问修符。下一节将回顾做出这些选择。

### 访问修符

使用 `private` 访问修符定义的成员的访问限制在当前类内部。私有成员对于派自该类或实例化该类的类是不可访问的。使用私修符允许类保护其数据，并仅通过其方法或属性访问数据。这确保了封装的数据隐藏特性。

构造函数 使用 Public 构造函数与类名相同，使用 `public` 访问修符定义。需要注意的是，如果你不在构造函数未使用 `public` 访问修符，则无法从该类实例化对象。记住，当你有多个使用相同标识的方法时，你就拥有重载方法。重载方法的要求是每个方法的参数数量和或类型与其他方法不同。因此，根据定义，如果一个类有两个或多个构造函数，你就拥有重载方法。

属性

11

在创建继承 `Person` 类特征的专门化类之前，为 `Person` 类添加了属性。通过包含属性，就不再需要编写访问器（getter）和修改器（setter）方法。私有成员字段可以通过这些属性进行访问。

属性是 `C/C++/C` 编程家族的新特性。它们看起来像数据字段，但实现为可以获取或设置私有数据字段实例的方法。

![](img/45e6f245af31396d967c3186f196d331_682_0.png)

示例 11-2 显示了 `Person` 类的一些属性。由于空间限制，只显示了四个属性中的两个。第一个允许数据字段 `firstName` 只读属性；它不包含 `set` 属性。如果没有定义额外的修改器方法，`firstName` 在构造后永远无法更改。

如果你正在实现此解决方案，可能需要考虑一些重要的设计问题。首先，一个或多个构造函数允许通过为 `lastName` 赋值 "unknown" 并为 `firstName` 赋值空字符串来实例化对象。但是，对于从该类实例化对象的类来说，没有可用属性可以更改该值。因此，你需要编写一个变异方法（`set_firstName( )`）；否则，名称将无法更改。

在示例 11-2 中，`FirstName` 属性被显示为只读，以强化属性并不需要同时包含 `get` 和 `set` 的这一观点。你应该为不能更改的字段（如标识码）定义只读属性。

### 示例 11-2

```csharp
// 只读属性。名字不能更改。
public string FirstName
{
    get
    {
        return firstName;
    }
}
// 姓名的属性
public string LastName
{
    get
    {
        return lastName;
    }
    set
    {
        lastName = value;
    }
}
```

当你向类中添加 `LastName` 属性时，可以使用 `LastName` 标识符检索 `lastName` 的当前内容。注意你没有声明 `value`。它可以几乎像魔法一样，用于引用通过赋值语句传递的值。

> 注意 `get`、`set` 和 `value` 在代码中是如何显示为蓝色的。当你开始阅读这本书时，你被告诉关键字将显示为蓝色。Visual Studio 遵循这一标准，但有少数例外。一个例外是，`set`、`value` 和 `get` 在 Visual Studio 中默认显示为蓝色，但它们并不是关键字。因为你会在 IDE 中看到它们是蓝色的，所以它们在本书中也显示为蓝色。

在你的解决方案中添加属性允许使用属性标识符访问私有数据，而不是编写额外的方法。

### 重写方法

向 `Person` 类增加了两个额外的方法，并在示例 11-3 中显示。第一个方法重写了 `object` 的 `ToString( )` 方法。当你重写一个方法时，你会用新的定义或行为替换更高层级定义的方法。注意 `override` 关键字被添加到 `ToString( )` 方法头部上，而 `virtual` 被添加到 `GetSleepAmt( )` 方法头部上。在方法头部放置 `virtual` 允许该方法被重写。

### 示例 11-3

```csharp
public override string ToString() // 定义在 Person 中
{
    return firstName + " " + lastName;
}
public virtual int GetSleepAmt()
{
    return 8;
}
```

> 重写方法（Overriding）与重载方法（Overloading）不同。重写的方法必须与它重写的方法具有相同的签名。新功能通常通过重写方法定义。重载方法必须与其他同名的方法具有不同的性质。重载方法通常定义用于执行相似的行为，但使用不同的数据类型。

### 使用 override 关键字

`override` 关键字允许方法为继承自基类的方法提供新的实现。当你重写一个方法时，方法的签名必须匹配。要重写基方法，该基方法必须被定义为 `virtual`、`abstract` 或 `override`。图 11-4 显示了属于 `object` 类的 `ToString( )` 方法签名。这取自 Visual Studio 的在线文档。

C#

`public virtual string ToString();`

图 11-4 ToString() 签名

### 虚方法

`.NET` 开发者将 `virtual` 修饰符作为方法签名的一部分，它可以被任何 `C#` 类重写。每个类都继承自 `object` 类的方法。`ToString()` 不需要被重写。它返回一个表示当前对象的字符串。它经常被重写，以根据调用它的对象提供不同的功能。

> > 这是多态的一个示例，意味着许多形式。你将在本章后面的部分读到更多关于多态的内容。思考“变形”（morphing）的含义——一个对象重塑自身。在这种背景下，`ToString()` 方法可以有很多不同的定义。调用该方法时使用的定义取决于哪个对象调用了它。

在示例 11-3 中，`GetSleep()` 方法也使用了 `virtual` 修饰符，这意味着任何派自 `Person` 的类都可以重写该方法。要重写方法，新方法必须与你计划重写的方法具有完全相同的参数。

### 创建派生类

继承自基类的类被称为派生类。它们也被称为子类或子类，因为它们继承了父类的特征。任意数量的类都可以继承自之前示例中定义的 `Person` 类。`Person` 是使用 `public` 访问修饰符定义的。

## 保护访问修饰符

虽然派生类确实继承了基类的所有特征，但它们无法直接访问其私有成员。除了 `private` 和 `public` 访问外，`C#` 还提供了 `internal` 和 `protected` 访问。`internal` 成员仅在同一程序集中的文件中可访问。`protected` 成员对任何派生类可见，但对任何其他类可见。因此，如果你希望派生类中的方法能够更改基类中的数据，请使用 `protected` 访问修饰符定义数据成员，而不是 `private` 访问。这样，数据对其他类仍然隐藏，但对派生类可用。

为了演示继承，为 `Student` 类创建一个新文件。`Student` 类继承了 `Person` 类的所有成员，并增加了两个额外的数据字段成员。这是一个“是一个”（is a）的关系。`Student` “是一个” `Person`。示例 11-4 显示了来自 `Student` 类的一些源代码。

### 示例 11-4

```csharp
public class Student : Person {
    private string major;
    private int studentId;

    // 默认构造函数
    public Student() {
        major = "unknown";
        studentId = 0;
    }

    // 向基类传递数据的构造函数
    public Student(string id, string fname, string lname, int sid)
        :base(id, lname) {
        major = maj;
        studentId = sid;
    }

    public override int GetSleepAmt() {
        return 6;
    }
}
```

示例 11-4 包含了一些有趣的特性。首先，头部指示 `Student` 继承自 `Person`。该类在示例 11-5 中重复出现。

### 示例 11-5

`public class Student : Person // Student 继承自 Person`

### 调用基构造函数

要调用基类的构造函数，需要在 `Student` 头部和括号之间添加额外的条目，如示例 11-6 所示。

### 示例 11-6

```csharp
public Student()
  :base() // 不向基传递参数
```

这调用了 `Person` 的默认构造函数。要向基类传递数据，你必须具有匹配的签名。

在实例化 `Student` 类的同时向基类传递数据，在 `base` 关键字后跟随与 `Person` 的某个构造函数匹配的参数：

```csharp
public Student(string id, string fname, string lname, string maj, int sid)
  :base(id, lname) // 基参数
```

关键字 `base` 在示例 11-6 中以冒号和括号的形式显示（`:base( )`），用于指示创建派生类对象时应使用哪个基类构造函数。注意它位于类头部。第一次对基构造函数的调用使用了无参数的默认构造函数。
