class. In C#, a class can implement more than one interface, and an interface can also be implemented by another interface.

Let's perform the following steps to create an application named **InterfaceInheritance** to learn to implement an interface inheritance:

+   1. Repeat the steps 1 to 3 discussed while creating the **CreatingMethod** application in the **Defining a Method** section of this chapter.
+   2. Enter **InterfaceInheritance** in the **Name** text box to specify the name of the application, and specify an appropriate location for the application in the **Location** combo box.
+   3. Click the **OK** button. The **InterfaceInheritance** application is created.
+   4. In the **Program.cs** file, add the highlighted code given in Listing 4.26:

**Listing 4.26: Implementing an Interface Inside a Class**

```
~~~csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace InterfaceInheritance
{
    interface BaseInterface
    {
        void GetDetail();
    }
    interface DerivedInterface : BaseInterface
    {
        void ShowDetail();
    }
    class InterfaceImplementer : DerivedInterface
    {
        string Name;
        int Age;
        string Address;
        long PhoneNumber;
        public void GetDetail()
        {
            Console.Write("Enter Your Name:");
            Name = Console.ReadLine();
            Console.Write("Enter Your Age:");
            Age = int.Parse(Console.ReadLine());
            Console.Write("Enter Your Address:");
            Address = Console.ReadLine();
            Console.Write("Enter Your Phone Number:");
            PhoneNumber = long.Parse(Console.ReadLine());
        }
        public void ShowDetail()
        {
            Console.WriteLine("");
            Console.WriteLine("Your Details are:");
            Console.WriteLine("Name: " + Name);
            Console.WriteLine("Age: " + Age);
            Console.WriteLine("Address: " + Address);
            Console.WriteLine("Phone Number: " + PhoneNumber);
        }
    }
    class MainClass
~~~
```