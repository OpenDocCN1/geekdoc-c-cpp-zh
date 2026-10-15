![](bbox=[0.19, 0.07, 0.86, 0.3])

In Figure 34.2, you can see elements, such as methods and properties, which can be obtained from a class by using reflection.

# Dynamically Invoking Methods from Classes in an Assembly

If you are creating a new compiler or interpreter for C# or any other .NET language, you need to use reflection to find information about the objects loaded in the compiler or interpreter. You can not only find information about different objects, but also invoke methods on them dynamically, if you know the name of the method you want to call and the arguments you want to pass to the method.

In addition to transferring information into a method, C# allows you to return information from a method to the calling function. This means that if a method, which you call, returns a value, then it will also provide the information back to the method of your calling application. In this section, we are creating the DynamicInvoke.cs file, which gives a simple set of classes. First, we create a class that implements a specific interface by defining the methods of the interface. Next, you call some of these methods directly to show the output of the functions. Finally, you dynamically invoke some of these methods to show how that particular process takes place.

The following steps are performed to create and execute the DynamicInvoke.cs file (also available in the CD):

+   1. Open a Notepad and add the code given in Listing 34.4:

# Listing 34.4: Showing the Code for Dynamically Invoking Methods from a Class

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Reflection;
namespace DynamicInvoke
{
    interface IMyInterface
    {
        void PrintAString(string s);
        void PrintAnInteger(int i);
        void PrintSomeNumbers(string desc, int i, double d);
        int GetANumber(string s);
    }
    public class DoMyInterface : IMyInterface
    {
        public DoMyInterface() { }
        public void PrintAString(string s)
        {
            Console.WriteLine("PrintAString: {0}", s);
```