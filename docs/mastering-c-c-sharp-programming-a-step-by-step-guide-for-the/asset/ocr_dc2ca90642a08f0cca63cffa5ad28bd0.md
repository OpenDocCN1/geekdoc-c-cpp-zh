```
Console.WriteLine("These are the constructors in our Customer class:--");
foreach (ConstructorInfo c in constructorInfo)
{
    Console.WriteLine(c);
}
```

The method called GetConstructors() in the Type class will return an array of the ConstructorInfo type – basically, a list of the public constructors that are defined inside the reflected type.

Ok, so now we want to display all the Customer class public methods and, again, we only have the one so all you would see on the console when the program is executed is the one name. To do this, the code would look like this:

```
static void Main(string[] args)
{
    Type type = typeof(Customer);
    MethodInfo[] methodInfo = type.GetMethods();
    Console.WriteLine("The Customer class methods are:--");
    foreach (MethodInfo temp in methodInfo)
    {
        Console.WriteLine(temp.Name);
    }
    Console.Read();
}
```

Note, you may see the names of some extra methods, such as Equals, ToString, GetType, and GetHashCode. That is because those methods were inherited from the class called Object and, as