
```csharp
namespace CaseStudy14
{
    interface HPSystem
    {
        void ListComputer();
        void ShowComputerColor(string str);
        void ShowComputerFeature(string feature);
        void ShowComputerPrice(double price);
    }
    class ComputerList : HPSystem
    {
        string comptercolor = "";
        string computernames = "";
        public void ListComputer()
        {
            computernames = "1.      HP Pavilion Media Center m8000\n";
            computernames = computernames + "\n2.      HP Compaq DC5750 PC";
            computernames = computernames + "\n3.      HP Compaq DX2300 pc";
            Console.WriteLine("The HP Computers are :\n\n" + computernames);
        }
        public void ShowComputerColor(string color)
        {
            this.comptercolor = color;
            Console.WriteLine("\nThe color of the systems are : " + comptercolor + "\n");
        }
        public void ShowComputerFeature(string feature)
        {}
        public void ShowComputerPrice(double price) {}
    }
    class ShowHPCompterDetails : ComputerList
    {
        string Computerfeature = "";
        double ComputerPrice = 0;
        public void ShowComputerFeature(string feature)
        {
            this.Computerfeature = feature;
            Console.WriteLine("The features of the systems are " +Computerfeature);
        }
        public void ShowComputerPrice(double price)
        {
            this.ComputerPrice = price;
            Console.WriteLine("\nThe Prices of the systems are:" +ComputerPrice);
        }
    }
    class ShowComputerFeatures
    {
        static void Main(string[] args)
        {
            ShowHPCompterDetails hpm = new ShowHPCompterDetails();
            hpm.ListComputer();
            hpm.ShowComputerColor("Steel Gray");
            hpm.ShowComputerColor("Black");
            hpm.ShowComputerColor("Gray");
            hpm.ShowComputerFeature("Pentium PIV PC Dual Core2");
            hpm.ShowComputerFeature("Pentium PIV 2.5GHz processor");
            hpm.ShowComputerFeature("Pentium PIV PC Dual Core");
            hpm.ShowComputerPrice(63000);
            hpm.ShowComputerPrice(30000);
            hpm.ShowComputerPrice(45000);
        }
    }
}
```

## Remarks

The Interface feature allows us to implement the concept of multiple inheritance in a C# application. It also provides the benefit of reusing the code, which is defined in one application, for another application. In an Interface, the methods are declared as abstract without any implementation code. Interface can be implemented in multiple classes in C#.

## Common Programming Errors

- Declaring data fields as members.
- Declaring a member as static.
- Using a visibility modifier to declare a member.
- Forgetting to place a semicolon at the end of a method declaration.
- Forgetting to implement a member in the implementing class.
- Forgetting to cast the class object to the interface type.
- Using an access modifier on an explicit implementation method.
- Attempting to create an instance of an interface.
- Forgetting to declare an implementation method as public.

## Review Questions

14.1 State whether the following statements are true or false.

- (a) Like classes, an interface can inherit only one interface.
- (b) All the members of an interface are implicitly abstract.
- (c) A member of an interface may be declared private.
- (d) An interface is normally used to declare constant data fields.
- (e) An interface cannot extend classes.
- (f) A method declared in a super interface must be implemented in the subinterface.
- (g) A class can implement any number of interfaces.
- (h) Any number of classes can implement an interface.
- (i) An interface may be considered as an alternative to an abstract class.
- (j) An abstract class can implement an interface.
- (k) We can create an instance of an interface using the new operator.

14.2 What is an interface?

14.3 What are the major differences between a class and an interface?

14.4 What are the similarities between a class and an interface?

14.5 All the members of an interface are made implicitly public. Why?

14.6 All the members of an interface are implicitly abstract. What is the implication of this?

14.7 When an interface inherits another interface, we call it as extending an interface. But when a class inherits an interface, we call it as implementing an interface. Why?

14.8 What is explicit interface implementation? When is it used?

14.9 Does C# support multiple inheritance? If yes, how can it be implemented?

14.10 Using interfaces, we can implement multiple inheritance characteristics in a class. How?

14.11 How do we indicate that class Class1 derives from base class BaseClass and implements the interfaces FileRead and FileWrite?

14.12 We can combine two or more interfaces together. Discuss.

14.13 Describe various forms of implementing interfaces. Give examples of C# code for each case.

14.14 Give an example where interfaces can be used to support multiple inheritance.

14.15 Can an abstract class implement interfaces? If yes, how are the interface methods implemented?

14.16 Distinguish between an abstract class and an interface?

14.17 Find errors in the following interface definitions and implementations:

- (a)

  ```csharp
  new interface A
  {
      void M1();
  };
  ```

- (b)

  ```csharp
  private interface A {}
  public interface B : A {}
  ```

- (c)

  ```csharp
  interface A {}
  interface B {}
  interface C extends A, B
  {}
  ```

- (d)

  ```csharp
  interface A {}
  class B {}
  class C : A, B
  {}
  ```

- (e)

  ```csharp
  interface A {}
  class B implements A
  {}
  ```

- (f)

  ```csharp
  interface A
  {
      void M1();
      int n;
  }
  ```

- (g)

  ```csharp
  interface X
  {
      static void Fun();
  }
  ```

- (h)

  ```csharp
  interface Y
  {
      public void Display ();
      int count {get;}
  }
  ```

- (i)

  ```csharp
  interface P
  {
      abstract void Paint ();
  }
  ```

- (j)

  ```csharp
  interface A
  {
      void Mul ();
  }
  interface B : A
  {
      void Mul ();
  }
  ```

## Debugging Exercises

### 14.1 Locate and correct errors in the program shown below.

```csharp
using System;
using System.Collections.Generic;
using System.Text;
namespace debugApp1_chap14
{
    public abstract class Car
    {
        abstract void RemoveAllFuses();
        abstract void StartEngine();
    }
    class Seat : Car
    {
        public override void RemoveAllFuses()
        {
        }
        public override void StartEngine()
        {
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Seat c = new Seat();
            c.RemoveAllFuses();
        }
    }
}
```

### 14.2 Find the errors in the following program.

```csharp
using System;
using System.Collections.Generic;
using System.Text;

namespace debugApp2_chap14
{
    interface Dimensions
    {
        float Length();
        float Width();
    }
    interface MetricDimensions
    {
        int Length();
        int Width();
    }
    class Box : Dimensions, MetricDimensions
    {
        float lengthInches;
        float widthInches;
        public Box(float length, float width)
        {
            lengthInches = length;
            widthInches = width;
        }
        // Explicitly implement the members of IEnglishDimensions:
        float Dimensions.Length()
        {
            return lengthInches;
        }
        float Dimensions.Width()
        {
            return widthInches;
        }

        float MetricDimensions.Length()
        {
            return lengthInches * 2.54f;
        }
        float MetricDimensions.Width()
        {
            return widthInches * 2.54f;
        }
        static void Main()
        {
            Box box1 = new Box(30.0f, 20.0f);
            // Declare an instance of the English units interface:
            Dimensions eDimensions = (Dimensions)box1;
            // Declare an instance of the metric units interface:
            MetricDimensions mDim = (MetricDimensions)box1;
            // Print dimensions in English units:
            System.Console.WriteLine("Length(in): {0}", eDimensions.Length());
            System.Console.WriteLine("Width (in): {0}", eDimensions.Width());
            // Print dimensions in metric units:
            System.Console.WriteLine("Length(cm): {0}", mDim.Length());
            System.Console.WriteLine("Width (cm): {0}", mDim.Width());
        }
    }
}
```

### 14.3 Check for syntax errors in the program and correct them.

```csharp
using System;
using System.Collections.Generic;
using System.Text;

namespace debugApp3_chap14
{
    class Program
    {
        public class ShowValues
        {
            void Show();
        }

        public class CharContainer :: ShowValues
        {
            public void Show()
            {
                // Do character type sorting here.
                Console.WriteLine("From CharContainer.");
            }
        }

        public class NumberContainer :: ShowValues
        {
            public void Show()
            {
                // Do numeric type sorting here.
                Console.WriteLine("From NumberContainer.");
            }
        }

        public void ShowAll(ShowValues[] sortobj)
        {
            foreach (ShowValues sv in sortobj)
            {
                sv.Show();
            }
        }

        static void Main(string[] args)
        {
            Program Obj = new Program();
            obj.ShowAll(new ShowValues[2] { new CharContainer(), new NumberContainer() }
            );
        }
    }
}
```
