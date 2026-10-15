make a change to the original method. I am going to use the names of the parameters when specifying the arguments for my method invocation.

```
```csharp
static void Main(string[] args)
{
    //UsingValueParameters();
    //UsingRefParameters();
    //UsingOutParameters();
    //UsingParams();
    //UsingOptionalParameters();
    UsingNamedArguments();

    Console.ReadLine();
}

private static void UsingNamedArguments()
{
    int monthlyWage = 1234;
    int months = 12;
    int bonus = 500;
}
```
```

I'm going to invoke my method, and instead of just passing the values here, I'm also going to declare which parameter I'm specifying the value for. So I can say, for example here, use bonus, and I then specify a colon, and so this bonus points to this bonus, and I pass it the value of bonus, the local variable. I can then do the same, for example, specifying the numberOfMonthsWorked, and, again, use a colon, and I set that to months. And finally, I need to also specify the monthlyWage, colon, and that will be then the monthlyWage.