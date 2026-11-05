
```
obj.Add(50); //No boxing
int data= obj[0]; // No unboxing
foreach(int cnt in obj)
{
    Console.WriteLine(cnt); //No unboxing
}
```

## C# Generic Methods

In C#, if a method is defined with type parameter, then it is called a generic method. Following is the example of defining a generic method with type parameter using angle (<>) brackets.

```
public void genericMethod<T>(T a, T b)
{
    // code Implementation
}
```

This generic method can be called either by specifying the type of argument or without an argument like as shown below.

```
genericMethod<int>(1, 2);
//or
genericMethod(1, 2);
```

### Example of generic method

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

## Generics in inheritance

### Generic Class as Base Class

In C# the generic class can used as a base class, but there is need to provide a type instead of type parameter for the base class because there is no way to send a required type argument to instantiate a base class at run time. Hence, while deriving from a generic base class, one must provide a type argument instead of the base-class's generic type parameter as shown below.

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

If the derived class is required to be generic then no need to specify type for the generic base class.

Example : Generic derived class

```
class DerivedClass1<U> : GenericClass1<U>
{
    //implementation
}
```

**If the generic base class has constraints, the derived class must use the same constraints.**

Example : Constraints

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

## C# Generic Delegates

In C#, a generic delegate will be same as a normal delegate with additional generic type with angle (<>) brackets.

Following is the example of defining a generic delegate in C# programming language.

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

## Two Marks Questions with Answers

### Q.1 What is a base class and derived class ?

Ans. : A class is a template for creating an object. The class from which other classes derive fundamental functionality is called a base class. For e.g. If Class Y derives from Class X, then Class X is a base class.

The class which derives functionality from a base class is called a derived class. If Class Y derives from Class X, then Class Y is a derived class.

### Q.2 What is inheritance ?

Ans. : Inheritance represents the relationship between two classes where one type derives functionality from a second type and then extends it by adding new methods, properties, events, fields and constants.

C# support two types of inheritance :

- Implementation inheritance
- Interface inheritance

### Q.3 What is implementation and interface inheritance ?

Ans. : When a class (type) is derived from another class(type) such that it inherits all the members of the base type it is Implementation Inheritance.

When a type (class or a struct) inherits only the signatures of the functions from another type it is Interface Inheritance.

In general Classes can be derived from another class, hence support Implementation inheritance. At the same time Classes can also be derived from one or more interfaces. Hence they support Interface inheritance.

### Q.4 Define Overriding.

Ans. : Overriding is a concept where a method in a derived class uses the same name, return type, and arguments as a method in its base class. In other words, if the derived class contains its own implementation of the method rather than using the method in the base class, the process is called overriding.

### Q.5 Can you use multiple inheritance in .NET ? Why don’t we have multiple inheritance in .NET ?

Ans. : .NET supports only single inheritance. However the purpose is accomplished using multiple interfaces.

There are several reasons for this. In simple words, the efforts are more, benefits are less. Different languages have different implementation requirements of multiple inheritance. So in order to implement multiple inheritance, we need to study the implementation aspects of all the languages that are CLR compliant and then implement a common methodology of implementing it. This is too much of efforts. Moreover multiple interface inheritance very much covers the benefits that multiple inheritance has.

## Long Answered Questions

- 1. **Q.1** Define and discuss inheritance by giving example. (Refer section 9.1)
- 2. **Q.2** How polymorphism is achieved in C# ? (Refer section 9.2)
- 3. **Q.3** What is the purpose of combining method hiding and method overriding ? (Refer section 9.5)
- 4. **Q.4** Discuss operator overloading in C#. (Refer section 9.5)
- 5. **Q.5** What are generics ? (Refer section 9.7)
- 6. **Q.6** Write a C# program to demonstrate hierarchical inheritance. **AU : May-18, Marks 7**

Ans. :

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

### Q.7 Write a C# Program to Illustrate Multilevel Inheritance with Virtual Methods.

AU : Dec.-18, Marks 6

Ans. :

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
