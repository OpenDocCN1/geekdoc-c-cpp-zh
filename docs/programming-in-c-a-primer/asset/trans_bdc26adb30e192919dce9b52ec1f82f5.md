

```csharp
public void show()
{
    Console.WriteLine("Teacher Code is {0} ", tcode);
    Console.WriteLine("Teacher Name is {0} ", tname);
}
}
//End of nested structure
//Here method overloading applicable for the function addStudents() and addStudents(string str3, string str4)
public void addStudents()
{
    studentname = "Suresh Goyal";
    rollno = "S0011_class4";
}
public void addStudents(string str3, string str4)
{
    studentname = str3;
    rollno = str4;
}
public void show()
{
    Console.WriteLine("Student Name {0} ", studentname);
    Console.WriteLine("Roll Number {0} ", rollno);
}
}; // End of Structure student
class Program
{
    static void Main(string[] args)
    {
    //creating an instance of student
    student st=new student();
    st.RollNo="50007_Class3";
    Console.WriteLine("Roll Number after overriding the property {0}", st.RollNo);
    //Creating an instance of inner structure teachers
    student.teachers te=new student.teachers();
    //Directly Refering the fields of inner structure teachers
    te.tcode="T00014";
    te.tname="Kishan Singh";
    //Accessing the getValues() of inner structure teachers
    te.getValues("T00015","Naresh Kumar");
    //calling the show() of inner structure of teachers
    te.show();
    //overriding the instance of student.teachers
    student.teachers intf1=new student.teachers();
    intf1.getValues("T00014","Sunil Mohan");
    intf1.show();
    //Creating the instance of the nested class examination
    student.school ee=new student.school();
    ee.schoolproperty="St. Johns School, Janakpuri, Delhi";
    ee.show_details();
    }
}
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_214_0.png)

## 11.5 类与结构的区别

结构是类的一种简单轻量级替代方案。虽然结构在基本概念上与类相同，但结构更适用于我们只是想将一些数据组合在一起的情况。因此，结构在设计和实现上与类有显著不同。 （类将在第 12 章和第 13 章中讨论）。重要区别列于表 11.1。

表 11.1 类与结构的区别

| CATEGORY | CLASSES | STRUCTS |
|---|---|---|
| Data Type | Reference type and therefore stored on the heap | Value type and therefore stored on the stack. Behave like simple data types |
| Inheritance | Support inheritance | Do not support inheritance |
| Default values | Default value of a class type is null | Default value is the value produced by 'zeroing out' the fields of the struct |
| Field initialization | Permit initialization of instance fields | Do not permit initialization of instance fields |
| Constructors | Permit declaration of parameterless constructors | Do not permit declaration of parameterless constructors |
| Destructors | Supported | Not supported |
| Assignment | Assignment copies the reference | Assignment copies the values. |

结构是值类型这一事实会影响它们作为参数传递给方法时的性能。我们可以通过将结构作为 ref 参数传递给方法来避免这种性能损失。在这种情况下，只会传递内存中的地址，这与传递类一样快。

```
class EnumTest:
{
    public static void Main()
    {
        Area area = new Area ();
        area.AreaShape ( 15, Area.Shape.Circle);
        area.AreaShape ( 15, Area.Shape.Square);
        area.AreaShape ( 15, (Area.Shape) 1 );
        area.AreaShape ( 15, (Area.Shape) 10 );
    }
}
```

Shape 枚举定义了可以为枚举指定的值，并且在方法调用中也使用相同的枚举来指定需要计算面积的形状。请注意枚举成员的访问方式。

Shape.Circle // Access to Circle inside Area class
Area.Shape.Circle // Access to Circle outside Area class

声明；
Shape shape
在方法定义中将 shape 声明为枚举类型对象。

在方法调用中，可以为枚举指定的值并不限于在枚举定义中指定的标识符。第三次和第四次调用
area.AreaShape ( 15, ( Area.Shape) 1 );
area.AreaShape ( 15, ( Area.Shape) 10 );
是合法的调用。但是，传递的值必须在有效值的范围内。由于枚举成员的值范围为 0 到 1，第三次调用指的是 Shape.Square 情况，而第四次调用传递的值超出范围。请注意，当传递 int 类型值时，它们会被强制转换为枚举类型值。

程序 11.4 将产生以下输出：
Circle Area      =      706.8583
Square Area      =      225.00000
Square Area      =      225.00000
Invalid Input

程序 11.5 在两个枚举 Staff 和 Company 中存储值。它使用两个函数来显示 Staff 和 Company 枚举中包含的数据。

## 程序 11.5 进一步说明枚举

```
using System;
using System.Collections.Generic;
using System.Text;
namespace EnumerationExample
```
```
{
    enum Staff
    {
        Directors,
        Managers,
        Executives
    }
    enum Company
    {
        NewSoftLtd,
        TechnologiesInc,
        HillRockLtd
    }
    class Program
    {
        public static void Show(Staff st)
        {
            switch (st)
            {
                case Staff.Directors:
                    Console.WriteLine("You are a Director.");
                    break;
                case Staff.Managers:
                    Console.WriteLine("You are a Manager.");
                    break;
                case Staff.Executives:
                    Console.WriteLine("You are an Executive.");
                    break;
                default: break;
            }
        }
        public static void CompDisplay(Company com)
        {
            switch (com)
            {
                case Company.NewSoftLtd:
                    Console.WriteLine("NewSoftLtd.");
                    break;
                case Company.TechnologiesInc:
                    Console.WriteLine("TechnologiesInc.");
                    break;
                case Company.HillRockLtd:
                    Console.WriteLine("HillRockLtd.");
                    break;
                default: break;
            }
        }
        static void Main(string[] args)
        {
```

```
Staff st;
st = Staff.Directors;
Console.WriteLine("This is an example of Enumeration in C#\n");
Show(st);
Company com;
com = Company.NewSoftLtd;
Console.Write("Director belongs to Company : ");
CompDisplay(com);
```

![](img/bae4ee2c7c29c052feb3b9a9c5659998_218_0.png)

## 11.7 枚举器初始化

如前所述，默认情况下，第一个枚举成员的值设为 0，后续每个成员的值递增 1。然而，我们可以根据需要为不同成员分配特定值。

示例：

```
enum Colour
{
    Red   = 1,
    Blue  = 3,
    Green = 7,
    Yellow = 5
}
```

我们也可以使用表达式，只要它们使用已定义的枚举成员即可。

示例：

```
enum Colour
{
```
```
Red      = 1,
Blue     = Red + 2,
Green    = Red + Blue + 3,
Yellow   = Blue + 2
}
```

如果枚举成员的声明没有初始化器，则其值按如下方式隐式设置：

- 如果它是第一个成员，其值为零。
- 否则，其值是通过将前一个成员的值加一获得的

考虑以下枚举声明：

```
enum Alphabet
{
    A,
    B = 5,
    C,
    D = 20,
    E
}
```

成员 A 设为零。由于成员 B 明确赋值为 5，成员 C 的值设为 6（即 5 + 1）。同理，E 设为 21。

以下枚举声明无效，因为声明是循环的。

```
enum ABC
{
    A,
    B = C,
    C
}
```

## 11.8 枚举器基类型

默认情况下，枚举的类型为 int。然而，我们可以为每个枚举显式声明基类型。

有效基类型为：

byte, sbyte, short, ushort, int, uint, long and ulong

示例：

```
enum Position : byte
{
    off,
    on
}
```

```
enum Shape : long
{
    Circle,
    Square = 100,
    Triangle
}
```

分配给成员的值必须在基类型可以表示的值范围内。例如，如果基类型为 byte，分配值 300 是非法的。

