```
{
    Console.WriteLine ("Hello! I'm a cat.");
}
}
```

As you can notice, there are a few changes to the code in the above examples. A method has been added on the Cat Class and, on the Animal class, the virtual keyword has been added to the method. Additionally, there is the presence of the override keyword on the Cat class.

In C#, it is not possible to override an item of any class unless it has been marked as virtual. It is certainly possible to keep accessing the inherited method even after it has been overridden with the help of the base keyword. This is shown in the example below.

```
public override void Greet()
{
    base.Greet();
    Console.WriteLine ("Yes! I am - a cat!");
}
```

However, methods are not the only thing that can be inherited. In fact, nearly all members of a class will be inherited. This