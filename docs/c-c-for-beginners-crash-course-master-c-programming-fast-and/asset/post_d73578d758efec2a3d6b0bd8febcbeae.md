
```csharp
Thread.Sleep(2000);

//child thread aborted
Console.WriteLine("Aborting child thread");
t2.Abort();
Console.Read();
}
}
}
```

**When the code is compiled and executed, the output is:**

Creating child thread  
Child thread started  
0  
1  
Aborting child thread  
Exception caught  
Exception is not handled

## Reference links on C#

User can get more detailed information about the C# language using the following reference links.

- Visual Studio Application – The IDE for creating C# applications.
- C# (Programming Guide) – An overview of C# programming language.
- C# Programming – The information about the C# features using .NET framework is explained.
- Mono – Cross platform applications can be easily created using the software.
- C# Complete Tutorial – It contains lessons useful for beginners to learn C# language.

## Conclusion

This brings us to the end of this book. We hope that this guide has been thoroughly comprehensible and easy for you to understand and follow. The book should not end your journey on the road to learning C#, instead it should only serve as the beginning. There is a vast amount of information that you can learn on C# therefore once you are done with this book, explore further boundaries of C#.

C# has a growing popularity and is steadily being used more and more. Many famous sites and enterprise level applications are powered by C#. You can find C# in the scientific computing being run on supercomputers. System administration tasks such as package management and configuration use C# as well. No matter what your programming interests, the possibilities for learning, exploring, and growing are endless.
