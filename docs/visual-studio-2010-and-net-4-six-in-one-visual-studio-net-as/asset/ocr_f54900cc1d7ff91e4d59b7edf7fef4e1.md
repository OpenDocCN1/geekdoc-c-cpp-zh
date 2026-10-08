Here, you have abstract Pets with two concrete manifestations, Dog and Macaw. These types are intended to be in a pet shop application, and Pet has an operation named ShackUpWith accepting two sequences of pets and returns their union.

Modify the Program.cs file of the application as shown in Listing 24-5.

# LISTING 24-5: Program.cs

![](bbox=[0.045, 0.213, 0.108, 0.273])

```
using System;
using System.Collections.Generic;
using System.Linq;

namespace CovarianceSample
{
    class Program
    {
        static void Main(string[] args)
        {
            var dogs = new List<Dog>
            {
                new Dog( Name = "Spike", Age = 3 ),
                new Dog( Name = "Murray", Age = 12 ),
                new Dog( Name = "Peach", Age = 2 )
            };

            var macaws = new List<Macaw>
            {
                new Macaw( Name = "Georgey", Age = 32 ),
                new Macaw( Name = "Bella", Age = 4 ),
                new Macaw( Name = "Grey", Age = 11 )
            };

            var youngsters = from pet in Pet.ShackUpWith(dogs, macaws)
                            where pet.Age < 5
                            select pet;

            foreach (var pet in youngsters)
            {
                Console.WriteLine(pet.Name);
            }
        }
    }
}
```



The ShackUpWith method used in the query expression expects IEnumerable<Pet> arguments, but in the previous code, IEnumerable<Dog> and IEnumerable<Macaw> instances are passed. However, because IEnumerable<T> is covariant in T, the compiler accepts it. With C# 3.0 in Visual Studio 2008, this code would not compile. In order to make it work with C# 3.0, you would need to use a workaround. One possible solution is to cast dogs and macaws to IEnumerable<Pet>: