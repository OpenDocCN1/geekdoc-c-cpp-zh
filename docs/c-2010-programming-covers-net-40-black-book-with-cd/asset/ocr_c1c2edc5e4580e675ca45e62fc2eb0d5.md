CD), which demonstrates how a delegate can use a derived return type. Listing 6.12 shows the code of the Program.cs file of the Covariance application:

# Listing 6.12: Showing the Code of the Program.cs File

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace Covariance
{
    class X
    {
        public X CreateX() {
            Console.WriteLine("This is class X");
            return new X();
        }
    }
    class Y : X
    {
        public Y CreateY() {
            Console.WriteLine("This is class Y");
            return new Y();
        }
    }
    class Program
    {
        public delegate X Create();
        public static void Foo(Create obj) { obj(); }
        static void Main(string[] args) {
            Create obj1 = new Create(new X().CreateX);
            Create obj2 = new Create(new Y().CreateY);
            Foo(obj1);
            Foo(obj2);
            Console.Write("\nPress ENTER to quit...");
            Console.ReadLine();
        }
    }
}
```

Figure 6.14 shows the output of the preceding code:

![](bbox=[0.18, 0.6, 0.78, 0.7])

# Figure 6.14: Implementing Covariance

In this application, we have defined two classes, X and Y. The class Y derives from the class X. Now, a delegate can be defined with a return type of X, but this delegate can be used to return type X or Y. The defined delegate returns the base class X, though you can use the same delegate to return an object of the derived class Y.

Let’s now learn to implement contravariance.

# Implementing Contravariance

As discussed earlier in the In Depth section, contravariance allows you to use a method with derived parameters as a delegate. Let’s create a Console application, named Contravariance (also available in the CD), which demonstrates the use of contravariance for using a method as delegate. Listing 6.13 shows the code of the Program.cs file of the Contravariance application: