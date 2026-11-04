# Implementing Encapsulation

Encapsulation is a process of hiding the internal details of an object and showing only the relevant information to a user. It is a way to organize data and methods into a structure by hiding the way an object is implemented. Encapsulation, therefore, helps to protect data from being misused and also prevents access to data by any means other than those specified.

Encapsulation is implemented through access modifiers. Access modifiers help to implement this feature by defining a scope to access data and methods in a restricted manner. Consequently, you can describe encapsulation as the ability of an object to hide its internal data and methods, and make only the intended parts of the object programmatically accessible.

Let’s perform the following steps to create a console application named EncapsulationExample to learn how to implement encapsulation:

+   1. Repeat the steps 1 to 3 discussed while creating the CreatingMethod application in the Defining a Method section of this chapter.
+   2. Enter EncapsulationExample in the Name text box to specify the name of the application, and specify an appropriate location for the application in the Location combo box.
+   3. Click the OK button. The EncapsulationExample application is created.
+   4. In the Program.cs file, add the highlighted code given in Listing 4.18:

Listing 4.18: Implementing Encapsulation

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace EncapsulationExample
{
    class MyClass
    {
        private int x;
        private float y;
        protected int z;
        private void add()
        {
            Console.WriteLine("This is a private method");
        }
        public void sub()
        {
            Console.WriteLine("This is a public method");
        }
        protected void div()
        {
            Console.WriteLine("This is a protected method");
        }
    }
    class Program : MyClass
    {
        static void Main(string[] args)
        {
            Program prg = new Program();
            prg.div();
            prg.z = 20;
            prg.sub();
            Console.ReadLine();
        }
    }
```