
面向对象开发技术非常适合构建多层应用程序。在查看图11-1时，请将图中的每个组件都视为相互独立的类，彼此分离。可以设计类，并创建新的子类来扩展原始类的功能。许多不同的应用程序可以通过扩展这些类或将它们组合到新应用程序中来重用这些类。

在 C# 中，除了创建 .EXE 文件外，还可以创建扩展名为动态链接库（DLL）的类库文件。这些文件可以成为被任意数量的应用程序引用的组件。要利用面向对象编程的特性，你必须理解的关键概念之一就是继承。

## 继承

继承允许你创建一个通用类，然后定义可以访问该通用类成员的专用类。这些新的专用类可以通过添加自己独有的新数据和行为来扩展功能。继承与“是一个”关系相关联。专用类是通用类的一种形式。例如，你可以创建一个名为 Person 的类，并包含标识号、姓名、年龄和家庭住址等数据特征。在使用社会保障号作为标识的地区（例如美国），社会保障号就是标识号。其中可能包含名为 Eat( )、Walk( ) 和 Talk( ) 的行为或方法。定义这些内容后，你可以创建诸如 Student 或 Faculty 之类的专用类，它们继承自 Person 类。Student“是一个”Person，正如 Faculty“是一个”Person。Student 可能具有学生 ID、专业和年级等独特数据特征。通过使用继承，实例化 Student 类对象的应用程序不仅会具有学生独有的特征（学生 ID、专业和年级），还可以访问 Person 的特征（标识号、姓名、年龄和地址）。

![](img/e33ae760e23d89eac66541252ad65de8_681_0.png)

类还可以具有“拥有一个”关系，其中定义单个类拥有其他类类型的实例。这是一个称为包含或聚合的概念。当你在 C# 中定义实例化 string 或 int 类对象的类时，就会体验到包含。然而，“拥有一个”关系通常与用户定义的类相关联。例如，一个 Person“拥有一个”medicalRecord，并且“拥有一个”dentalRecord。

### 从 Object 类继承

自从你在第 1 章编写第一个程序以来，你就一直在创建自己的类。你了解到，在 C# 中创建的每个对象都会自动继承 System 命名空间中名为 object 的基类。Object 有四个方法，只要 C# 中编写的类提供了对 System 命名空间的引用，就会继承这些方法。其中之一是 ToString() 方法，你已在许多程序中使用过它。图11-2 使用 IntelliSense 显示 Object.ToString() 的签名以及从 object 继承的其他方法的名称。

![](img/e33ae760e23d89eac66541252ad65de8_682_0.png)

**图11-2** 从 object 继承的方法

### 从其他 .NET FCL 类继承

你在第 9 章和第 10 章开发基于 Windows 的程序时也体验过继承。你创建的 Windows Forms 类继承自 System.Windows.Forms.Form 类。扩展该类使你能够基于该 .NET Framework 类中包含的功能进行构建。添加从 Button、Label、TextBox 和 ListBox 等类实例化的对象，使你能够以最少的编程工作为程序添加功能。为了继承 System.Windows.Forms.Form 类，你的类定义中添加了新条目。图11-3 说明了当你决定通过从“项目类型”菜单中选择“Windows 应用程序”模板来构建 Windows 应用程序时，Visual Studio 会添加什么内容。

![](img/e33ae760e23d89eac66541252ad65de8_682_1.png)

**图11-3** 派生类

在面向对象术语中，图11-3 中冒号后面列出的类是基类。冒号左侧的类 PresentationGUI 称为**派生类**。要从基类继承，冒号用作派生类和基类之间的分隔符，如图11-3 所示。PresentationGUI 是用户定义的名称。Form 类属于 System.Windows.Forms 命名空间。在此示例中，用户定义的**类**继承自预定义的 .NET **类**；然而，当用户定义的**类**继承自另一个用户定义的**类**时，相同的概念也适用。通过使用冒号，你表明 PresentationGUI **类**派生自 Form **类**。

### 创建用于继承的基类

你可以定义自己的类，其他类可以从这些类继承特征。示例11-1 创建了一个名为 Person 的类，其中包含四个数据成员。该类用作基类，其他类可以从它继承特征。基类有时称为**超类**或**父类**。

### 示例11-1

```csharp
public class Person
{
        private string idNumber;
        private string lastName;
        private string firstName;
        private int age;

        public Person()              // Constructor with zero arguments
        {
                idNumber = "";
                lastName = "unknown";
                firstName = string.Empty;
                age = 0;
        }
        public Person(string id, string lname, string fname,
                      int anAge)     // Constructor with four arguments
        {
                idNumber = id;
                lastName = lname;
                firstName = fname;
                age = anAge;
        }
        public Person(string id, string lname, string fname)
        {                            // Constructor with three arguments
                idNumber = id;
                lastName = lname;
                firstName = fname;
                age = 0;
        }
        public Person(string id)
        {                            // Constructor with one argument
                idNumber = id;
                lastName = "unknown";
                firstName = string.Empty;
                age = 0;
        }
}
```

示例11-1 中的 **Person 类**仅显示了数据成员和构造函数方法。请注意，数据成员使用 private 访问修饰符定义，而构造函数使用 public 访问修饰符定义。下一节将回顾为什么做出这些选择。

### 访问修饰符

对使用 private 访问修饰符定义的成员的访问仅限于当前类的成员。派生自该类的其他类或实例化该类对象的其他类无法访问这些 private 成员。使用 private 访问修饰符使类能够保护其数据，并且只允许通过其方法或属性访问数据。这确保了封装的数据隐藏特性。

**构造函数使用 public 访问权限**   构造函数与类同名，使用 public 访问权限定义。需要注意的是，如果不对构造函数使用 public 访问修饰符，则无法从该类实例化任何对象。构造函数与其他方法的不同之处在于它们不能有返回类型。请记住，当有多个方法使用相同标识符时，就构成了**重载方法**。重载方法的要求是，每个方法的参数数量和/或类型必须与其他方法不同。因此，根据定义，当一个类有两个或更多构造函数时，就拥有重载方法。

**属性为数据字段提供 public 访问权限**   在创建专用类以继承 **Person 类**的特征之前，会向 **Person 类**添加属性。通过包含属性，编写访问器（getter）和修改器（setter）方法的需求就减少了。可以通过这些属性访问 private 成员字段。

![](img/e33ae760e23d89eac66541252ad65de8_684_0.png)

属性是 C/C++/C# 编程语言家族中的新特性。它们看起来像数据字段，但实现为可用于获取或设置 private 数据字段实例的方法。

示例11-2 显示了添加到 **Person 类**的一些属性。由于篇幅限制，仅显示了四个属性中的两个。第一个属性使数据字段 firstName 成为只读属性；它不包含 set 属性。如果不定义额外的修改器方法，firstName 在构造后永远无法更改。
