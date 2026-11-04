In this example, we use the return type to denote success or failure, while the output parameter will receive the result in case of success. This is a common pattern for various Base Class Library (BCL) types such as numeric value types that have a TryParse method:

```
Console.Write("Enter your age: ");
string input = Console.ReadLine();

int age;
if (!int.TryParse(input, out age))
    // Print error message, maybe let the user retry
else
    // We got a valid age
```

Prior to .NET 2.0, such methods didn't exist, and Parse methods had to be used instead. The difference between TryParse and Parse is what happens upon passing invalid input to the method. Parse throws an exception, whereas TryParse doesn't. Because exceptions are expensive and an invalid numeric string is not an exceptional case when dealing with user input, TryParse makes much more sense because it communicates success or failure through a Boolean value that can be checked easily.

Notice again how the out keyword has to be used at both the declaration site and the call site. Similar to reference parameters, this clarifies to the reader of the code what's going on at the method's call site.

Internally, ref and out are implemented both as ref. In fact, the common language runtime does not have a notion of output parameters. Figure 10.6 shows the method header for the following declaration, which uses both ref and out:

```
void Bar(int a, ref int b, out int c)
```

![](bbox=[0.18, 0.78, 0.68, 0.9])

FIGURE 10.6 Reference and output parameters use the & suffix.

Basically, output parameters are implemented as reference parameters with an extra piece of metadata stuck on them. The use of this metadata allows compilers to give reference and output parameters different treatment.

So what's the key difference between both parameter types from a C# programmer's point of view? The answer lies in “definite assignment rules” both at the side of the caller and of the callee. For a variable to be passed to a reference parameter, it must be assigned first. For output parameters, the responsibility for assignment is with the method being called,