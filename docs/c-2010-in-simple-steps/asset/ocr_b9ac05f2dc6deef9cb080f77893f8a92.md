Let's perform the following steps to create an application named AccessingMembers to learn how to access members of a base class:

+   1. Repeat the steps 1 to 3 discussed while creating CreatingMethod application in the Defining a Method section of this chapter.
+   2. Enter AccessingMembers in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box.
+   3. Click the OK button. The AccessingMembers application is created.
+   4. In the Program.cs file, add the highlighted code given in Listing 4.19:

# Listing 4.19: Accessing Base Class Members

```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace AccessingMembers
{
    public class BaseClass
    {
        public void BaseClassMethod()
        {
            Console.WriteLine("I am a Base Class Method()");
        }
    }
    public class DerivedClass : BaseClass
    {
        public void DerivedClassMethod()
        {
            Console.WriteLine("I am a Derived Class Method()");
            base.BaseClassMethod();
        }
    }
    public class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("I am accessing Base Class Object:");
            BaseClass bc = new BaseClass();
            bc.BaseClassMethod();
            Console.WriteLine("");
            Console.WriteLine("I am accessing Derived Class Object:");
            DerivedClass dc = new DerivedClass();
            dc.DerivedClassMethod();
            Console.WriteLine("\nPRESS ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```
```

In Listing 4.19, BaseClass is the parent class and DerivedClass is the derived class. The DerivedClass class inherits the features of the BaseClass class and is, therefore, the child class of the BaseClass class.

5 Press the F5 key to run the AccessingMembers application.

The output of the application appears, as shown in Fig.C#4.18: