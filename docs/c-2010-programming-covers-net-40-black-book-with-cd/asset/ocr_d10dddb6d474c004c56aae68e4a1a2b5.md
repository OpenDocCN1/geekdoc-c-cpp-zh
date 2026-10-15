# Using Nested Classes

A nested class is a class that is defined inside another class. This class acts as the member of the parent class in which it is defined. A nested class has the advantage of accessing all the members of its outer class. To see how to create nested classes in an application, first create a new Console application, named MyNestedClass (also available in the CD) and then replace the default code of the Program.cs file of the application with the code shown in Listing 4.26:

# Listing 4.26: Showing the Code of the MyNestedClass Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
namespace MyNestedClass
{
    public class Outer
    {
        public Outer(int num)
        {
            Number = num;
        }
        public class Inner
        {
            public void DisplayNumber(Outer o)
            {
                Console.WriteLine("The Number is: " + o.Number);
                Console.Write("\nPress Enter to quit...");
                Console.ReadLine();
            }
        }
        private int Number;
    }
    public class Nesting
    {
        static void Main()
        {
            Outer o1 = new Outer(100);
            Outer.Inner i1 = new Outer.Inner();
            i1.DisplayNumber(o1);
        }
    }
}
```

In Listing 4.26, we create a class, Outer, and inside this class, we create another class, Inner. In Listing 4.26, you can see that the DisplayNumber() method accesses the private variable, Number, of the Outer class.

Figure 4.27 shows the output of the MyNestedClass application:

![](bbox=[0.22, 0.69, 0.64, 0.81])

# Figure 4.27: Showing the Output of the MyNestedClass Application

# Using a Struct

There are several differences between a struct and a class. One big difference is that a struct is created on a stack; whereas, a class is created on a heap. To see how to create a struct, first create a new Console application, named MyStruct (also available in the CD) and then replace the default code of the Program.cs file of the application with the code shown in Listing 4.27: