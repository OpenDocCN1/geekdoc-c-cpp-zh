# Part I: C# Fundamentals

In this case, rather than use a number to represent the day of a week, it would be better if the user could choose from a list of possible named values representing the days in a week. The following code example declares an enumeration called Days that comprises seven names (Sun, Mon, Tue, and so forth). Each name has a value assigned (Sun is 0, Mon is 1, and so on):

```
```csharp
namespace HelloWorld
{
    public enum Days
    {
        Sun = 0,
        Mon = 1,
        Tue = 2,
        Wed = 3,
        Thur = 4,
        Fri = 5,
        Sat = 6
    }

    class Program
    {
        static void Main(string[] args)
        {
            Days day = Days.Mon;
            Console.WriteLine(day);    //---Mon---
            Console.WriteLine((int) day);  //---1---
            Console.ReadLine();
            return;
        }
    }
}
```
```

Instead of representing the day of a week using an int variable, you can create a variable of type Days. Visual Studio 2008's IntelliSense automatically displays the list of allowed values in the Days enumeration (see Figure 3-9).

```
```csharp
static void Main(string[] args)
{
    Days day = Days.
}
```
```

![](bbox=[0.55, 0.82, 0.7, 0.9])

Figure 3-9