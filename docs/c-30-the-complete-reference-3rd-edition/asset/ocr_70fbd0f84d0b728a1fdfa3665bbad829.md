Although the preceding program is correct, it is not written as efficiently as it could be. Specifically, there is no need for the areaPP variable. A call to AreaPerPerson() can be used in the WriteLine() statement directly, as shown here:

```
```csharp
Console.WriteLine("house has:\n " +
    house.Floors + " floors\n " +
    house.Occupants + " occupants\n " +
    house.Area + " total area\n " +
    house.AreaPerPerson() + " area per person");
```
```

In this case, when WriteLine() is executed, house.AreaPerPerson() is called automatically, and its value will be passed to WriteLine(). Furthermore, you can use a call to AreaPerPerson() whenever the area-per-person of a Building object is needed. For example, this statement compares the per-person areas of two buildings:

```
```csharp
if(b1.AreaPerPerson() > b2.AreaPerPerson())
    Console.WriteLine("b1 has more space for each person");
```
```

# Use Parameters

It is possible to pass one or more values to a method when the method is called. A value passed to a method is called an argument. Inside the method, the variable that receives the argument is called a formal parameter, or just parameter, for short. Parameters are declared inside the parentheses that follow the method's name. The parameter declaration syntax is the same as that used for variables. The scope of a parameter is the body of its method. Aside from its special task of receiving an argument, it acts like any other local variable.

Here is a simple example that uses a parameter. Inside the ChkNum class, the method IsPrime() returns true if the value that it is passed is prime. It returns false otherwise. Therefore, IsPrime() has a return type of bool.

```
```csharp
// A simple example that uses a parameter.

using System;

class ChkNum {
    // Return true if x is prime.
    public bool IsPrime(int x) {
        if(x <= 1) return false;

        for(int i=2; i <= x/2; i++)
            if((x %i) == 0) return false;

        return true;
    }
}

class ParmDemo {
    static void Main() {
        ChkNum ob = new ChkNum();

        for(int i=2; i < 10; i++)
            if(ob.IsPrime(i)) Console.WriteLine(i + " is prime.");
    }
}
```
```