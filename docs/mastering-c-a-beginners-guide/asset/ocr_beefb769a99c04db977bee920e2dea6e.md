```
```csharp
// as we have used "using System"
Console.WriteLine("Hello Newsco!");
}
}
} // ending of first namespace
// Class declaration
class Newsco_2
{
    // Main Method
    public static void Main(String []args)
    {
        // calling the display method of
        // class Newsco_1 by using only one
        // dot operator as display is the
        // static method of class Newsco_1
        Newsco_1.display();
    }
}
```
```

The final output is:

+   - Hello Newsco!

# Nested Namespaces

As an alternative, you can define a namespace into another namespace which is referred to as the nested namespace. In order to access the members of the nested namespace, user has to use the dot(.) operator.