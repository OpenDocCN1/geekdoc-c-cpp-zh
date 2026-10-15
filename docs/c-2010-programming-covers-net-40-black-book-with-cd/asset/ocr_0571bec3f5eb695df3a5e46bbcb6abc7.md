![](bbox=[0.105, 0.05, 0.82, 0.22])

# Figure 32.50: Searching an Index Number of a Value

Now, the result is displayed, as shown in Figure 32.51:

![](bbox=[0.25, 0.27, 0.68, 0.41])

# Figure 32.51: Displaying the Index Number of a Value

The index number of 4000 is 3, as an index number starts with zero.

Let’s learn how to implement covariance and contravariance in generics.

# Implementing Covariance and Contravariance in Generics

In this section, you learn to create a Console application named GenericContravarianceCovariance, also available on the CD-ROM, to understand the use of covariance and contravariance in generic classes of C#.

Listing 32.16 shows the code of the Program.cs file of the GenericContravarianceCovariance application:

# Listing 32.16: Showing the Code of the Program.cs File of the GenericContravarianceCovariance Application

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace GenericContravarianceCovariance
{
    class Vehicle { }
    class Car : Vehicle { }
    class Program
    {
        delegate T Func1<out T>();
        delegate void Action1<in T>(T a);
        static void Main(string[] args)
        {
            Func1<Car> c = () => new Car();
            Func1<Vehicle> vehi = c;

            Action1<Vehicle> v2 = (vehi2) => { Console.WriteLine(vehi2); };
            Action1<Car> c1 = v2;
        }
    }
}
```