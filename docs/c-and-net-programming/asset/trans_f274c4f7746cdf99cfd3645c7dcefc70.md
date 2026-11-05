
```
obj.Add(50); //No boxing
int data= obj[0]; // No unboxing
foreach(int cnt in obj)
{
    Console.WriteLine(cnt); //No unboxing
}
```

## C# 泛型方法

在C#中，如果方法使用类型参数定义，则称为泛型方法。下面是通过尖括号（<>）使用类型参数定义泛型方法的示例。

```
public void genericMethod<T>(T a, T b)
{
    // code Implementation
}
```

此泛型方法既可以指定参数类型来调用，也可以不指定参数类型来调用，如下所示。

```
genericMethod<int>(1, 2);
//或者
genericMethod(1, 2);
```

### 泛型方法示例

```
using System;
using System.Collections.Generic;
namespace GenericDemo
{
    class Program1
    {
        //Generic method
        static void Swap<T>(ref T data1, ref T data2)
        {
            T temp;
            temp = data1;
            data1 = data2;
            data2 = temp;
        }
        static void Main(string[] args)
        {
            // Swap of two integers.
            int n1 = 40, n2 = 60;
            Console.WriteLine("Before swap: {0}, {1}", n1, n2);
            Swap<int>(ref n1, ref n2);
            Console.WriteLine("After swap: {0}, {1}", n1, n2);
            Console.ReadLine();
        }
    }
}
```

## 继承中的泛型

### 泛型类作为基类

在C#中，泛型类可以用作基类，但需要为基类提供具体类型而不是类型参数，因为无法在运行时发送所需的类型参数来实例化基类。因此，从泛型基类派生时，必须提供类型参数来代替基类的泛型类型参数，如下所示。

```
// Below code do not have any Error
class DerivedClass1 : GenericClass<string> {
// implementation
}
// Where as in below code there is Compile Time Error
//class DerivedClass2 : GenericClass<T> {
// // implementation
//}
```

```
Example: Generic base class
class DerivedClass1 : GenericClass1<string>
{
    //implementation
}
```

如果派生类需要是泛型，则不需要为泛型基类指定类型。

示例：泛型派生类

```
class DerivedClass1<U> : GenericClass1<U>
{
    //implementation
}
```

**如果泛型基类具有约束，派生类必须使用相同的约束。**

示例：约束

```
class GenericClass1<T> where T: class
{
    // Implementation
}
class DerivedClass1<U> : GenericClass1<U> where U: class
{
    //implementation
}
```

## C# 泛型委托

在C#中，泛型委托与普通委托相同，只是额外带有尖括号（<>）中的泛型类型。

下面是在C#编程语言中定义泛型委托的示例。

```
using System;
namespace GenericsDemo
{
    // Declare Generic Delegate
    public delegate T GenericDelegate1<T>(T n1, T n2);
    class BasicOperations
    {
        public int Add(int n1, int n2)
        {
            return n1 + n2;
        }
        public int Subtract(int no1, int no2)
        {
            return no1 - no2;
        }
    }
    class Demo
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Generic Delegate");
            BasicOperations obj = new BasicOperations();
            // Instantiate delegate with add method
            GenericDelegate1<int> dlgobj = new GenericDelegate1<int>(obj.Add);
            Console.WriteLine("Addition Result: " + dlgobj(10, 90));
            // Instantiate delegate with subtract method
            dlgobj = obj.Subtract;
            Console.WriteLine("Subtraction Result: " + dlgobj(10, 90));
            Console.ReadLine();
        }
    }
}
```

## 两分题（附答案）

### Q.1 什么是基类和派生类？

答：类是创建对象的模板。其他类从其中派生基本功能的类称为基类。例如，如果类Y派生自类X，则类X是基类。

从基类派生功能的类称为派生类。如果类Y派生自类X，则类Y是派生类。

### Q.2 什么是继承？

答：继承表示两个类之间的关系，其中一个类型从另一个类型派生功能，然后通过添加新方法、属性、事件、字段和常量来扩展它。

C#支持两种类型的继承：

- 实现继承
- 接口继承

### Q.3 什么是实现继承和接口继承？

答：当一个类（类型）派生自另一个类（类型）并继承基类型的所有成员时，即为实现继承。

当一个类型（类或结构体）只从另一个类型继承函数的签名时，即为接口继承。

一般来说，类可以从另一个类派生，因此支持实现继承。同时，类也可以从一个或多个接口派生，因此它们支持接口继承。

### Q.4 定义重写。

答：重写是指派生类中的方法使用与其基类中方法相同的名称、返回类型和参数的概念。换句话说，如果派生类包含自己的方法实现，而不是使用基类中的方法，则该过程称为重写。

### Q.5 可以在.NET中使用多重继承吗？为什么在.NET中没有多重继承？

答：.NET仅支持单继承。但可以通过多个接口实现多重继承的目的。

这有几个原因。简单来说，付出多，收益少。不同语言对多重继承有不同的实现要求。因此，为了实现多重继承，我们需要研究所有符合CLR的语言的实现方面，然后实现一种通用的实现方法。这需要付出太多努力。此外，多接口继承在很大程度上涵盖了多重继承的好处。

## 长答题

- 1. **Q.1** 通过示例定义并讨论继承。（参见9.1节）
- 2. **Q.2** 如何在C#中实现多态？（参见9.2节）
- 3. **Q.3** 结合方法隐藏和方法重写的目的是什么？（参见9.5节）
- 4. **Q.4** 讨论C#中的运算符重载。（参见9.5节）
- 5. **Q.5** 什么是泛型？（参见9.7节）
- 6. **Q.6** 编写一个C#程序演示层次继承。**AU：2018年5月，7分**

答：

```
/*
 * C# Program to Illustrate Hierarchical Inheritance
 */
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace Inheritance
{
    class HierarchicalInherit
    {
        static void Main(string[] args)
        {
            Principal pobj = new Principal();
            pobj.Manage();
            Teacher tobj = new Teacher();
            tobj.Manage();
            tobj.Teach();
            Student sobj = new Student();
            sobj.Monitor();
            sobj.Learn();
            Console.ReadKey();
        }
        class Principal
        {
            public void Manage()
            {
                Console.WriteLine("I am managing");
            }
        }
        class Teacher : Principal
        {
            public void Teach()
            {
Console.WriteLine("I am teaching");
}
}
class Student : Principal
{
    public void Learn()
    {
        Console.WriteLine("I am learning");
    }
}
}
```

### Q.7 编写一个C#程序，演示带有虚方法的多级继承。

AU：2018年12月，6分

答：

```
/*
 * C# Program to Illustrate Multilevel Inheritance with Virtual Methods
 */
using System;
public class Person
{
    protected string RNO = "21";
    protected string name = "Hari";
    public virtual void GetInfo()
    {
        Console.WriteLine("Name: {0}", name);
        Console.WriteLine("RNO: {0}", RNO);
        Console.WriteLine();
    }
}
class Student : Person
{
    public string id = "S101";
    public override void GetInfo()
    {
        base.GetInfo();
        Console.WriteLine("Student ID: {0}", id);
    }
}
class Stud : Student
{
    private string StudentAddress = "India";
    public void GetInfo()
    {
```

