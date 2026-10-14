```
{
    swanAsDuck.Walk();
    swanAsDuck.Swim();
    swanAsDuck.Quack();
}
}
}
```

The is predicate and the as cast return false and null, respectively. The Common Language Runtime (CLR) does not consider a Swan as being an IDuck, even though it actually fulfils that interface. A type must *implement* the interface via interface inheritance.

There are a couple of tricks that you can employ to enable the Swan class to be usable as an instance of the IDuck interface *without* having to implement it. Either you can take advantage of the dynamic typing extensions in newer versions of the CLR, or you can make use of a third-party library called Impromptu Interface.

# Using the Dynamic Language Runtime

As of version 4, the .NET Framework was no longer strictly statically typed. With the introduction of the dynamic keyword, and some supporting types, you can avoid the CLR’s static typing and switch to the dynamic typing of the Dynamic Language Runtime (DLR). An example of dynamic typing in C# is shown in Listing 3-22.

# LISTING 3-22 The DLR can be used for duck typing.

Click here to view code image

```
class Program
{
    static void Main(string[] args)
    {
        var swan = new Swan();

        DoDuckLikeThings(swan);

        Console.ReadKey();
    }

    static void DoDuckLikeThings(dynamic duckish)
    {
        if(duckish != null)
        {
            duckish.Walk();
            duckish.Swim();
            duckish.Quack();
        }
    }
```