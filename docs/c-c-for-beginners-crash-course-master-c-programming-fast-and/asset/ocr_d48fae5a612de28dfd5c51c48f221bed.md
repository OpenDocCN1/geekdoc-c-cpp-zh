# Example 41:

```
```csharp
using System;
namespace internal
{
    class Location
    {
        //member variables
        internal string city;
        public void AddValue()
        {
            Console.WriteLine("Enter the city name:");
            name = Console.ReadLine();
        }
        public void Show()
        {
            Console.WriteLine("City name is:{0}", name);
        }
    }
    class Program
    {
        static void Main(string[] args)
        {
            Location l = new Location();
            l.AddValue();
            l.Show();
            Console.Read();
        }
    }
}
```
```

When the code is compiled and executed, the output is:

```
```
Enter the city name:
London
City name is: London
```
```

# Protected Internal access specifier

The **protected internal** access specifier allows a class to expose the member functions and variables to the containing class, child class, or classes in same application. The access to the derived classes outside the application is allowed.