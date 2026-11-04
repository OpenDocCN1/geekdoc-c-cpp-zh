First, `f(x)` doesn't care what `x` is. The program assumes that whatever comes in gets changed to an integer at `gets_to_i`, but the function itself is case agnostic. This is good and bad, because if you do happen to give it a string or some other type, it will fail.

The array itself isn't typed, either. This can have benefits, because it is possible to drop a differently typed value in there if you know you are just going to write it to the screen.

# ## Dynamic C#

Of course, C# now has similar features, right? You should be able to do the same thing! Yes, in fact, you can. Here's the code:

```
```csharp
static dynamic f(dynamic x)
{
    return (Math.Sqrt(x) + 5.0 * Math.Pow(x, 3.0));
}
static void Main(string[] args)
{
    dynamic[] array = new Array[11];
    for (int i = 0; i < 11; i++)
    {
        array[i] = Console.ReadLine();
    }
    for (int i = 10; i>=0; i--)
    {
        dynamic y = f(array[i]);
        if (y > 400.0)
        {
            Console.WriteLine(string.Format("{0} TOO LARGE", i));
        }else{
            Console.WriteLine("{0} : {1}", i, array[i]);
        }
        Console.ReadKey();
    }
}
```
```

Line for line, the application does the same thing as the Ruby code, albeit longer. I kept the names the same so it was easier to follow. Because I had to use for loops to handle the integers, it made the body of the program quite a bit beefier. Figure 6-2 shows what the program looks like when it runs.

But why use the dynamic type here? Clearly, you could have just used double for this. Use of dynamic just made the program easier to create. Try changing the array to an array of double, like this:

```
```
Double[] array = new Double[11];
```
```

Hey, look at that: Now the `ReadLine` doesn't work. You'll just cast it to a double. Nope, can't do that; you have to use `TryParse`. You get the picture. Static types are hard to code with. Dynamic types are easier to code with.