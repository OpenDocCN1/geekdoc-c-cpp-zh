```
{
    Console.WriteLine("Add(x={0}, y={1})", x, y);
    
    var result = calculator.Add(x, y);
    
    Console.WriteLine("result={0}", result);
    
    return result;
}
}
private readonly ICalculator calculator;
}
// . .
public class ConcreteCalculator : ICalculator
{
    public int Add(int x, int y)
    {
        return x + y;
    }
}
```

Clients of the ICalculator interface will pass in various parameters, and some of the methods themselves will return values, too. Because the LoggingCalculator is in a position to intercept both of these artifacts, it can interrogate them directly. There are limitations to using logging decorators that should be considered. First, any private state contained in the decorated class remains unavailable to the logging decorator, which cannot access this state and write it to a log. Second, a logging decorator would need to be created for every interface in the application—a significant undertaking. For something so common, logging is better implemented as a logging aspect. Aspect-oriented programming (AOP) was covered in Chapter 3.

# Profiling decorators

One of the major reasons to choose the .NET Framework as the target platform for developing an application is that it lends itself well to Rapid Application Development (RAD). A working application can be developed in a far shorter time frame than in a lower-level language like, for example, C++. This is for several reasons, including the automatic memory management of the .NET Framework, the rich and varied list of libraries that can be used, and the .NET Framework itself. C# is often deemed fast at development time but slow at run time. C++, on the other hand, is considered to be slow at development time and fast at run time.

Although the .NET Framework can also be fast, bottlenecks do occur. How can you tell which part of the code is slow? By profiling the methods of the application, you gather statistics on which parts of the code are slower than others. See the code in Listing 7-25.