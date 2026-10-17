
```
{
    MessageBox.Show("Species: " + animal.Species);
    animal.MakeSound();
}
private void createAnimalButton_Click(object sender, EventArgs e)
{
    Animal myAnimal = new Animal("Regular animal");
    ShowAnimalInfo(myAnimal);
}
private void createDogButton_Click(object sender, EventArgs e)
{
    Dog myDog = new Dog("Fido");
    MessageBox.Show("The dog's name is " + myDog.Name);
    ShowAnimalInfo(myDog);
}
private void createButton_Click(object sender, EventArgs e)
{
    Cat myCat = new Cat("Kitty");
    MessageBox.Show("The cat's name is " + myCat.Name);
    ShowAnimalInfo(myCat);
}
private void editButton_Click(object sender, EventArgs e)
{
    // 关闭表单。
    this.Close();
}
```

## 知识点检查

### 10.6 观察以下类定义：

```csharp
class Vegetable
{
    public virtual void message()
    {
        MessageBox.Show("I'm a vegetable.");
    }
}
class Potato : Vegetable
{
    public override void message()
    {
        MessageBox.Show("I'm a potato.");
    }
}
```

有了这些类声明，以下代码将显示什么？
`Vegetable v = new Potato();`
`Potato p = new Potato();`
`v.message();`
`p.message();`

### 10.7 "is" 关系可以反向工作吗？为什么可以或不可以？

## 10.3 抽象类

**概念：** 抽象类作为基类，但本身不会被实例化。抽象方法没有方法体，必须在派生类中重写。

有时实例化一个基类是没有意义的。例如，一个制造飞机的工厂。该工厂不制造通用的飞机，而是制造两种特定类型的飞机：螺旋桨飞机和通勤喷气式飞机。用于分类飞机的计算机软件可能会使用名为 `Airplane` 的类。`Airplane` 类具有代表所有飞机共同特征的成员。此外，软件还有一个名为 `Plane` 的类和一个名为 `CommuterJet` 的类。这些类代表工厂制造的两种特定飞机型号，并派生自 `Airplane` 类。`Airplane` 类从不被实例化，而是作为其他类的基类使用。

不打算实例化而仅作为基类的类被称为抽象类。抽象类充当了起点，为它的派生类提供一些成员。要声明抽象类，请在类头部使用 `abstract` 关键字。

```csharp
abstract class ClassName
{
  // 成员声明
}
```

抽象类与普通类（有时称为具体类）的区别在于抽象类不能被实例化。尝试使用 `new` 运算符实例化抽象类的语句将无法编译。

抽象类还可以包含抽象方法。抽象方法是种期望在派生类中被重写的方法。抽象方法只有方法头而没有方法体。在方法头中，`abstract` 关键字出现在返回类型之前。这是一个包含抽象方法的抽象类的简单示例：

```csharp
abstract class Person
{
  public abstract void DoSomething();
}
```

当抽象方法出现在类中时，它必须在任何派生自该类的类中重写。在这个示例中，如果一个类派生自 `Person` 类，则该派生类必须重写 `DoSomething` 方法。

抽象类还可以包含抽象属性。抽象属性是出现在基类中期望在派生类中被重写的属性。在属性头中，`abstract` 关键字出现在属性类型之前。这是一个包含抽象方法的抽象类的简单示例：

```csharp
abstract class Person
{
  public abstract string JobTitle
  {
    get;
    set;
  }
}
```

注意，抽象属性显示了 `get` 和 `set` 访问器，但它没有指定这些访问器的作用。当抽象属性出现在类中时，它必须在任何派生自该类的类中重写。在这个示例中，如果一个类派生自 `Person` 类，则该派生类必须重写 `JobTitle` 属性。

> **注意：** 如果你想创建一个抽象只读属性，请省略 `set` 访问器。

## 10.3 抽象类

在教程 10-3 中，你完成了一个使用带有抽象属性的抽象基类的应用程序。

## 教程 10-3: 完成计算机学生应用程序

![](img/8a88e1d8c69a687988c05f162ce32cac_639_0.png)

在教程中，你编写了一个名为 `student` 的抽象类。`student` 类持有所有学生共有的数据，但它并不持有特定专业学生所需的所有数据。`student` 类旨在作为一个基类，可以被其他代表学生特定专业的类派生。

## 10.3 抽象类

```csharp
namespace Computer_Science_Student
{
    abstract class Student
    {
        // 字段
        private string _name;
        private string _id;
        // 构造函数
        public Student(string name, string id)
        {
            name = name;
            _id = id;
        }
        // Name 属性
        public string Name
        {
            get { return _name; }
            set { _name = value; }
        }
        // ID 属性
        public string ID
        {
            get { return _id; }
            set { _id = value; }
        }
        // RequiredHours 属性（抽象）
        public abstract double RequiredHours
        {
            get;
        }
    }
}
```

> **程序 10-11** Computer Student 应用中 CompSciStudent.cs 文件的完整代码

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
namespace Computer_Science_Student
{
    class CompSciStudent : Student
    {
        // 常量
        private const double MATH_HOURS = 20;
        private const double CS_HOURS = 40;
        private const double GEN_HOURS = 60;
        // 字段
        private string _academicTrack;
        // 构造函数
        public CompsciStudent(string name, string id, string track)
            : base(name, id)
        {
            _academicTrack = track;
        }
        // AcademicTrack 属性
        public string _academicTrack
        {
            get { return _academicTrack; }
            set { _academicTrack = value; }
        }
        // RequiredHours 属性
        public override double RequiredHours
        {
            get { return MATH_HOURS + CS_HOURS + GEN_HOURS; }
        }
    }
}
```

# 程序 10-12 Computer Science Student 应用中 Form1 的完整代码

```csharp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
namespace Computer_Science_Student
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }
        private void getHoursButton_Click(object sender, EventArgs e)
        {
            // 用于存储输入的变量
            string name, id, track;
            // 获取学生的姓名和 ID 号。
            name = textBox.Text;
            id = textBox.Text;
            // 获取学生的学术方向。
            if (infoSystemsRadioButton.Checked)
            {
                track = "Information Systems";
            }
            else
            {
                track = "Software Engineering";
            }
            // 创建一个 CompSciStudent 对象。
            CompSciStudent csStudent = new CompSciStudent(name, id, track);
            // 显示学生的所需学时。
            requiredHoursLabel.Text = csStudent.RequiredHours.ToString("\n");
        }
        private void exitButton_Click(object sender, EventArgs e)
        {
            // 关闭表单。
            this.Close();
        }
    }
}
```
