
```
}
}
class Hierarchical
{
    public static void Main()
    {
        Book bk = new Book();
        CompactDisc cd= new CompactDisc();
        bk.Details();        // base class Media member function
        bk.BookInfo();       // own member function
        cd.Details();        // base class Media member function
        cd.License();        // own member function
    }
}
```

输入
无

# 输出

已发布
书名 ERP
已发布
版权已验证并颁发许可证。

## 9.1.2.4 多重继承

在 C# 中，类不支持多重继承。也就是说，一个类不能继承多个类。但是，一个类允许继承单个类和多个接口。这被称为多重继承。

```
namespace MultipleInheritanceApplication
{
    interface IOP1
    {
        int Add(int n1, int n2);
    }
    interface IOP2
    {
        int Sub(int n1, int n2);
    }
    interface IOP3
    {
        int check_Even(int n1);
    }
    class Data_Operations : IOP1, IOP2, IOP3
{
    public int result;
    public int Add(int n1, int n2)
    {
        result = n1 + n2;
        return (result);
    }
    public int Sub(int n1, int n2)
    {
        result = n1 - n2;
        return (result);
    }
    public int check_Even(int n)
    {
        if (n % 2 == 0)
            return 1;
        else
            return 0;
    }
}

class MultipleInheritDemo
{
    static void Main(string[] args)
    {
        Data_Operations numop = new Data_Operations();
        Console.WriteLine("Multiple Inheritance concept Using Interfaces \n");
        Console.WriteLine("Addition: " + numop.Add(32, 4));
        Console.WriteLine("Subtraction: " + numop.Sub(128, 16));
        if (numop.check_Even(64) == 1)
            Console.WriteLine("Number is Even");
        else
            Console.WriteLine("Number is Odd");
    }
}
```

输入
无

# 输出

加法：36
减法：112
数字是偶数

## 9.1.3 访问修饰符

- 1. 类继承结合了接口继承和实现继承。接口继承根据一个或多个现有接口定义新接口。实现继承根据一个或多个现有实现定义新实现。
- 
- 2. 类成员的访问修饰符为派生类提供不同级别的访问权限。下表描述了派生类根据访问修饰符对继承类成员所具有的访问权限。

| 父类访问修饰符 | 子类中的访问权限 |
|---|---|
| public | 可访问 |
| protected | 可访问 |
| private | 不可访问 |

表 9.1.1 继承中的访问修饰符和作用域

### 示例

```
//illustration of access modifiers and inheritance scope  1

using System;

class Base // derived from built in class Object
{
    public void BDraw() { Console.WriteLine("Base method BDraw"); }
}

class Derived : Base // Derived inherits Base
{
    public void DDraw() { Console.WriteLine("Derived method DDraw"); }
}

class InheritScope
{
    static void Main()
    {
        Base b = new Base();
        b.BDraw(); // own method
        b.DDraw(); // Error derived class method can't access
        Derived d = new Derived();
        
d.BDraw();//inherited method

d.DDraw();//own method

}
//Illustration of access modifiers and inheritance scope  2
class Base
{
    protected int var =478 ;
}

class Derived : Base
{
    void Show()
    {
        Base b = new Base();
        Derived d = new Derived();
        b.var = 28; // Error
        d.var = 60; // OK
    }
}



// example2 protected

using System;

class Base
{
    protected int n1;
    protected int n2;
}

class Derived : Base //private inheritance
{
    public static void Main()
    {
        Derived d = new Derived();
        // Direct access to protected members to derived class
        d.n1 = 45;
        d.n2 = 68;
        Console.WriteLine("n1 = {0}, n2 = {1}", d.n1, d.n2);
        Console.ReadLine();
    }
}
```

## 9.1.4 C# 中的可见性修饰符

### 概念

可见性控制是面向对象编程中的一个关键问题。可见性控制很重要，因为它保护类的不可见部分不被其他类直接访问。程序的其他部分不能直接依赖于它们无法访问的细节。如果类的某个细节（通常是变量）在类外部不可见，那么以后修改这个细节就会容易得多。

### 解释

### 程序集中类型的可见性和类型中成员的可见性

- 程序集中类型（例如类）的可见性。
  - **internal：** 该类型从程序集外部不可见。
  - **public：** 该类型在程序集外部可见。
- 类型中成员（例如类中的方法）的可见性。
  - **private：** 仅在包含类型中可访问。
  - **protected：** 在包含类型及其子类型中可访问。
  - **internal：** 在程序集中可访问。
  - **protected internal：** 在程序集、包含类型及其子类型中可访问。
  - **public：** 只要封闭类型可访问，就可访问。

## 9.1.5 类修饰符

### 概念

- 1. 在实现继承时，重要的是要理解如何为新设计的派生类及其成员建立可访问性级别。

### 解释

- 2. 类修饰符用于决定系统的哪些部分可以创建类对象。
  
  有四种不同的可选类修饰符，分别是，
  
  1. **public** - 'public' 关键字将类型标识为可被所有其他类型完全访问。这是枚举成员和接口成员的隐式可访问性。
  
  2. **internal** - 如果类被声明为 'internal'，则所定义的类型仅对同一程序集（一个自包含的打包单元，包含代码、元数据等）中的类型可访问。这是非嵌套类的默认访问级别。

- 3. **protected** - 如果类被声明为 'protected'，则其类型可由包含类型以及继承自该包含类型的任何类型访问。此修饰符只应用于内部类（即在其他类中声明的类）。
  
- 4. **private** - 如果类被声明为 'private'，则对其所定义类型的访问仅限于包含类型。此修饰符只应用于内部类（即在其他类中声明的类）。

这些用于指定类所定义类型的访问级别。

3. 此外，可以使用上述四种修饰符指定以下不同的访问级别，

- 1. **Protected internal** - 此访问级别允许的权限是 'protected' 级别允许的权限加上 'internal' 级别允许的权限。因此，该访问级别比单独使用其各部分更宽松。此修饰符只应用于内部类（即在其他类中声明的类）。
  
- 2. **New** - 'new' 关键字可用于“嵌套”类。嵌套类是在另一个类的主体中定义的类；它在大多数方面与以常规方式定义的类相同，但其访问级别不能比定义它的类的访问级别更宽松。嵌套类应使用 'new' 关键字声明，以防它与继承类型同名（并因此覆盖该继承类型）。
  
- 3. **Abstract** - 声明为 'abstract' 的类本身不能被实例化——它仅设计为用于继承的基类。
  
- 4. **sealed** - 声明为 'sealed' 的类不能从其他类继承。将密封类用作基类是错误。在类声明中使用 sealed 修饰符可防止该类被继承。

## 9.1.6 C# 继承层次结构中构造函数和析构函数的调用顺序

- 1. **当实例化派生类时，会自动调用基类的默认构造函数。** 这样，基类构造函数可以在派生类构造函数执行之前初始化基类。

### 示例

```
// Demonstrate when constructors are called.
using System;

// Create a base class.
class Media{
    public Media () {
        Console.WriteLine("Constructing Media.");
    }
}
```
