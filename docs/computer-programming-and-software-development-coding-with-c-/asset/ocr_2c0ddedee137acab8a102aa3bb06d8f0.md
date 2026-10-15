```
{
    public int X;
    public int Y;
    public override string ToString()
    {
        return $"({X}, {Y})";
    }
}
```

To show you what I mean by resilience, I've set up a new application that uses a very simple point structure that's been defined in a separate library. For now, the important bit is that the definition and implementation of the point structure is in a separate binary, which allows it to be reused across multiple applications, including this one. All the application does is initialize a local variable called pt, set its X and Y fields to initial values, and then display the result of calling the point structures toString method to the console.

```
class Program
{
    static void Main()
    {
        var pt = new Point { X = 30, Y = 12 };
        Console.WriteLine(pt.ToString());
    }
}
```

Notice that when this version of the program is run, the implementation of toString returns a string that shows the X, Y