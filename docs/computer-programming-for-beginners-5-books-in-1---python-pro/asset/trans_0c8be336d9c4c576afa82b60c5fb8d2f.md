
析构函数是在离开程序之前释放内存资源的有用工具。你不能重载或继承析构函数。以下示例演示如何使用析构函数：

```csharp
using System;
namespace ConstructorApplication {
  class Person {
    private double height;  // Height of a person

    public Person() {  // A constructor
      Console.WriteLine("We are creating an object!");
    }
    ~Person() {  // A destructor
      Console.WriteLine("We are deleting an object!");
    }
    public void setHeight( double heig ) {
      height = heig;
    }
    public double getHeight() {
      return height;
    }
    static void Main(string[] args) {
      Person p = new Person();
      // set the height of the person
      p.setHeight(7.0);
      Console.WriteLine("The height of the person is : {0}", p.getHeight());
    }
  }
}
```

以下是该函数的输出：

![](img/239ff1e8a63502805c86c4dfbd71509a_562_0.png)

## 静态成员

要将类成员定义为静态，我们使用 *static* 关键字。当类成员被声明为静态时，这意味着无论创建了多少个该类的对象，静态成员都只存在一份副本。

使用 *static* 关键字意味着类中只存在一个成员实例。当需要声明常量时，我们使用此关键字，因为无需创建类的实例，通过调用类即可获取它们的值。我们可以在类定义或成员函数之外初始化静态变量。静态变量也可以在类定义内部初始化。

让我们通过一个示例演示静态变量的使用：

```csharp
using System;
namespace StaticApp {
    class StaticVariables {
        public static int x;

        public void count() {
            x++;
        }
        public int getX() {
            return x;
        }
    }
    class StaticTester {
        static void Main(string[] args) {
            StaticVariables var1 = new StaticVariables();
            StaticVariables var2 = new StaticVariables();
            var1.count();
            var1.count();
            var1.count();
            var2.count();
            var2.count();
            var2.count();
            Console.WriteLine("Variable x for var1 is: {0}", var1.getX());
            Console.WriteLine("Variable x for var2 is: {0}", var2.getX());
            Console.ReadKey();
        }
    }
}
```

该代码返回以下结果：

![](img/239ff1e8a63502805c86c4dfbd71509a_563_0.png)

成员函数也可以声明为静态。这样的函数只能访问静态变量。静态函数甚至在对象创建之前就存在。静态函数可以如以下示例所示使用：

```csharp
using System;
namespace StaticAppli {
    class StaticVariable {
        public static int x;
        public void count() {
            x++;
        }
        public static int getX() {
            return x;
        }
    }
    class StaticTester {
        static void Main(string[] args) {
            StaticVariable var = new StaticVariable();

            var.count();
            var.count();
            var.count();
            Console.WriteLine("Variable x is: {0}", StaticVariable.getX());
            Console.ReadKey();
        }
    }
}
```

该代码将返回以下内容：

![](img/239ff1e8a63502805c86c4dfbd71509a_564_0.png)

## 第12章：结构

C# 中的结构是一种值类型数据类型。使用结构，你可以用一个变量保存属于不同数据类型的相关数据。在 C# 中，我们使用 *struct* 关键字创建结构。

结构用于跟踪记录。一个很好的例子是当你需要保存所有班级学生或所有公司员工的记录时。对于存储学生记录的情况，你可能需要跟踪的一些详细信息，包括姓名、年龄、课程、入学日期、完成日期、已缴费用金额、费用余额等、监护人地址和手机号码等。所有这些详细信息属于不同的数据类型，这意味着你将需要为每一项创建一个变量。然而，通过使用结构，你可以定义一个单一变量，并将这些详细信息作为一个整体保存。

以下是声明结构的示例：

```csharp
struct Employee{
    public string name;
    public string department;
    public string title;
    public int age;
    public double salary;
};
```

要初始化结构，我们可以选择使用 *new* 关键字或不使用。结构的成员可以如下所示赋值：

```csharp
using System;

public class MyStruct
{
    public static void Main()
    {
        Employee emp = new Employee();
        emp.name = "Nicholas Samuel";
        emp.department = "Computing";
```

注意，结构是值类型，这使得它比类对象更快。这使其非常适合用于游戏编程。然而，传输类对象比传输结构更容易。这意味着当需要将数据传输到其他类时，不应使用结构。

以下是 C# 中结构的另一个示例：

```csharp
using System;
struct Cars {
    public string model;
    public int cc;
    public int passengers;
    public int year;
};
public class carStructure {
    public static void Main(string[] args) {
        Cars Premio;    /* Declare premio of type Car */
        Cars X6;    /* Declare X6 of type Car */
        /* premio specification */
        Premio.model = "Saloon";
        Premio.cc = 1800;
        Premio.passengers = 5;
        Premio.year = 2010;
        /* X6 specification */
        X6.model = "Saloon";
        X6.cc = 3500;
        X6.passengers = 5;
        X6.year = 2012;
        /* print premio info */
        Console.WriteLine("Premio model: {0}", Premio.model);
        Console.WriteLine("Premio CC : {0}", Premio.cc);
        Console.WriteLine("Premio passengers : {0}", Premio.passengers);
        Console.WriteLine("Premio year : {0}", Premio.year);
        /* print X6 info */
        Console.WriteLine("X6 model: {0}", X6.model);
        Console.WriteLine("X6 CC : {0}", X6.cc);
        Console.WriteLine("X6 passengers : {0}", X6.passengers);
        Console.WriteLine("X6 year :{0}", X6.year);
        Console.ReadKey();
    }
}
```

该代码将返回以下详细信息¹³⁰：

![](img/239ff1e8a63502805c86c4dfbd71509a_568_0.png)

![](img/239ff1e8a63502805c86c4dfbd71509a_569_0.png)

我们创建了一个名为 *Cars* 的单一结构。在这个结构中，我们存储了两个成员 Premio 和 X6。这两个实例是该结构的实例。它们的属性已在结构内部定义。这两个实例共享属性，但会取不同的值。然后我们打印了这些属性的值，如上述输出所示。

### 结构的特征

到目前为止，你已经了解了如何使用结构及其一些特征。C# 中的结构与 C 和 C++ 支持的结构有很大不同。C# 结构具有以下描述的特征：

- 结构可以包含字段、索引器、方法、属性、运算符和事件。
- 结构可以定义构造函数，但不能定义析构函数。但是，在结构中，不允许定义默认构造函数。原因是默认构造函数是自动定义的，无法更改。
- 结构不能继承另一个结构或类。
- 使用结构，我们可以实现一个或多个接口。
- 结构的成员不能指定为 virtual、abstract 或 protected。
- 通过 *New* 关键字创建结构对象后，结构对象被创建，并调用必要的构造函数。与类不同，我们可以不使用 *New* 关键字来实例化结构。
- 如果我们不使用 New 运算符，字段将不会被赋值，并且在所有字段完成赋值之前，无法使用该对象。

### 结构与类的比较

以下是结构与类之间的区别：

- 结构被解释为值类型。另一方面，类被定义为引用类型。
- 结构不支持继承。类支持继承。
- 结构不能有默认构造函数。类可以有默认构造函数。

让我们创建一个与上述区别相关的示例：

```csharp
using System;
struct Cars {
    private string model;
    private int cc;
    private int passengers;
    private int year;
    public void getValues(string m, int c, int p, int yr) {
        model = m;
        cc = c;
        passengers = p;
        year = yr;
```
