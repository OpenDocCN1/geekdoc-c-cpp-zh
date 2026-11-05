```
```csharp
class Account
{
    public string Name ;
};
class StructsAndObjectsDemo
{
    public static void Main ()
    {
        Account RobsAccount ;
        RobsAccount = new Account();
        RobsAccount.Name = "Rob";
        Console.WriteLine (RobsAccount.Name );
    }
}
```
```

The line I have added creates a new Account object and sets the reference RobsAccount to refer to it.

![](bbox=[0.42, 0.47, 0.85, 0.6])

We have seen this keyword new before. We use it to create arrays. This is because an array is actually implemented as an object, and so we use new to create it. The thing that new creates is an object. An object is an instance of a class. I'll repeat that in a posh font:

> > “An object is an instance of a class”

I have repeated this because it is very important that you understand this. A class provides the instructions to C# as to what is to be made, and what it can do. The new keyword causes C# to use the class information to actually make an instance. Note that in the above diagram I have called the object an Account, not RobsAccount. This is because the object instance does not have the identifier RobsAccount, it is simply the one which RobsAccount is connected to at the moment.

# 4.4.2 References

We now have to get used to the idea that if we want to use objects, we have to use references. The two come hand in hand and are inseparable. Structures are kind of useful, but for real object oriented satisfaction you have to have an object, and that means that we must manage our access to a particular object by making use of references to it. Actually this is not that painful in reality, in that you can treat a reference as if it really was the object just about all of the time, but you must remember that when you hold a reference you do not hold an instance, you hold a tag which is tied onto an instance...

# Multiple References to an Instance

Perhaps another example of references would help at this point. Consider the following code: