all or nothing decision to choose the language that a large application or suite of applications will be built in. If C# is the best tool for a given job or the language that a given team is most proficient with, then that's the tool you can use. On the other hand, if VB or F# is the best tool for a given job or the language a different team prefers, then the majority of your skills transfer because although there are syntactic differences from language to language that you would need to understand, any investment you've made becoming proficient with the various classes and application frameworks defined in the BCL is transferable. Now, I'll demonstrate this kind of common language capability in action by writing a C# application that leverages a mathematical library written in F# using the same BCL types to communicate. As with the previous demonstration, I have created a very simple C# application that calls an Add method to compute the sum of two integer values and then display the result to the console.

```
```csharp
var a = 30;
var b = 12;
var sum = fscalc.Calculator.Add(a, b);

System.Console.WriteLine($"{a} + {b} = {sum}");
```
```

What's different is that I've implemented this Add method in a separate library named calc, which I've implemented using F# rather than C# because F# is a functional language particularly for mathematical problem domains.