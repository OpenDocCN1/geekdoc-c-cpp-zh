comment.
11. Add a public instance field called Number of type int to the WrappedInt class, as shown in bold type in the following code:

```
namespace Parameters
{
    class WrappedInt
{
        public int Number;
    }
}
```

12. Display the Pass.cs file in the Code and Text Editor window. Add a public static method called Reference to the Pass class. This method should accept a single WrappedInt parameter called param and have the return type void. The body of the Reference method should assign 42 to param.Number, as shown here:

Click here to view code image

```
public static void Reference (WrappedInt param)
{
    param.Number = 42;
}
```

13. Display the Program.cs file in the Code and Text Editor window. Comment out the existing code in the doWork method and add four more statements to perform the following tasks:

+   - Declare a local WrappedInt variable wi and initialize it to a new WrappedInt object by calling the default constructor.
- Write the value of wi.Number to the console.
- Call the Pass.Reference method, passing wi as an argument.
- Write the value of wi.Number to the console again.

As before, with the calls to Console.WriteLine, you can see whether the call to Pass.Reference modifies the value of wi.Number. The doWork method should now look exactly like this (the new statements are in bold);