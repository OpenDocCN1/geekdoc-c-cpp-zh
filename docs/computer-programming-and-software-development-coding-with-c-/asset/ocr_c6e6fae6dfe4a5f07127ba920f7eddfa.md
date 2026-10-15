# Additional information

Console Application  C#  Linux  macOS  Windows  Console

Target Framework

.NET 5.0 (Current)

Now let's remove here the Console.WriteLine statement and let's create here a stack variable and let's initialize it with a SimpleStack instance. I press Ctrl+dot, and now you can see Visual Studio suggests here to generate a class, SimpleStack, in a new file. Let's hit Enter, and now you can see here in the Solution Explorer the new SimpleStack C# file.

```
{
    class Program
    {
        static void Main(string[] args)
        {
            var stack = new SimpleStack();
        }
    }
}
```

Now on that stack, let's call a Push method and let's pass in a double value. I press Ctrl+C and Ctrl+V, and again Ctrl+V, to copy this line two times. Let's also push in the double value 2.8, and let's also push in the double value 3.0. Now I press Ctrl+dot again to