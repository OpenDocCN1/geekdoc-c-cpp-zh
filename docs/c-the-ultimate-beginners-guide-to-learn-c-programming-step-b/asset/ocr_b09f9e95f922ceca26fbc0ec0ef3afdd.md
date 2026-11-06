```
```csharp
Console.WriteLine("After calling the method, the of value of x is : {0}", x);
Console.ReadLine();
}

}

}
```
```

It returns the following:

```
```text
Before calling the method, value of x : 10
After calling the method, value of x is : 20
```
```

The variable that is supplied for the output parameter should be assigned a value. Output parameters are very useful when one wants to return values from a method via the parameters without assigning initial value to the parameter. The following example will help you understand this better:

```
```csharp
using System;

namespace MethodApplication {
    class NumberChecker {
        public void getValues(out int a, out int b) {
            Console.WriteLine("Enter in your first value: ");
            a = Convert.ToInt32(Console.ReadLine());

            Console.WriteLine("Enter in your second value: ");
            b = Convert.ToInt32(Console.ReadLine());
        }

        static void Main(string[] args) {
            NumberChecker n = new NumberChecker();

            /* defining a local variable */
            int x, y;
```
```