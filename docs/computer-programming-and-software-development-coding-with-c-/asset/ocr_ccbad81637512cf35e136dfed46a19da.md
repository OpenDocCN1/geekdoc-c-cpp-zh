That said, it's okay if you've never seen any of those things before. The point of this demonstration is not to acquire an understanding of those things, but to prove the claim that C# can be both safe and resilient to change as a result of being a managed language and yet still exhibit the performance characteristics of native code.
However, if you are content to take my word for it or don't care to know how exactly the CLR pulls off JIT compilation magic, feel free to skip. You can rest assured that you will not miss any of the big picture regarding C#, only a bit of proof that one of the biggest claims made in this book and elsewhere is, in fact, true. For the adventurous among you, let's dig in. To show you compilation in action, I've created a very simple C# application that adds two numbers together and displays the result to the console.

```
{
    static void Main()
    {
        Console.WriteLine("Main called. Press ENTER when ready to call Add.");
        Console.ReadLine();

        var sum = Add(30, 12);

        Console.WriteLine(sum);
        Console.WriteLine("Press ENTER to exit program.");
        Console.ReadLine();
    }

    static int Add(int a, int b)
    {
        return (a + b);
    }
}
```

However, to give us a chance to observe the before and after aspects of compilation, I'm calling a separate method named Add to perform that arithmetic. Similarly, I've strategically placed calls to console.readline both before and after the call to that Add method in order to pause the application and give me a chance to attach a