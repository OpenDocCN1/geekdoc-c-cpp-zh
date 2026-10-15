
## Chapter 7 Assembling a C# Program

So far, we've seen just a few snippets of C#, a few lines of code in a file. More interesting programs are usually made up of many files, so in this chapter let's up our game and focus on building a program from multiple files. And also, if you remember, there are a couple of lines in "Hello, World!" that we still didn't explain, because those lines are easier to understand once you know how to write programs with more than one file. In this chapter we'll cover these lines as well, so we're going to give one last look at "Hello, World!". The file that we just added to the project contains a class with the same name as the file. That's a common practice to have one class per file, and the same name for the file and the class.

```
namespace MyUtilities
{
    class WeatherUtilities
    {
        static float FahrenheitToCelsius(float temperatureFahrenheit)
        {
            var temperatureCelsius = temperatureFahrenheit - 32 / 1.8f;
            return temperatureCelsius;
        }

        static float CelsiusToFahrenheit(float temperatureCelsius)
        {
            var temperatureFahrenheit = temperatureCelsius * 1.8f + 32;
            return temperatureFahrenheit;
        }

        static float ComfortIndex(float temperatureFahrenheit, float humidityPercent)
        {
            var comfortIndex = (temperatureFahrenheit + humidityPercent) / 4;
            return comfortIndex;
        }
    }
}
```

It's certainly not mandatory, but it's a convenient default way to organize classes in files. And this class contains a few static methods, one, two, four methods. It's like a tiny library to do weather calculations.

```
static float FahrenheitToCelsius(float temperatureFahrenheit)
{
    var temperatureCelsius = temperatureFahrenheit - 32 / 1.8f;
    return temperatureCelsius;
}

static float CelsiusToFahrenheit(float temperatureCelsius)
{
    var temperatureFahrenheit = temperatureCelsius * 1.8f + 32;
    return temperatureFahrenheit;
}

static float ComfortIndex(float temperatureFahrenheit, float humidityPercent)
{
    var comfortIndex = (temperatureFahrenheit + humidityPercent) / 4;
    return comfortIndex;
}

static void Report(string location, float temperatureCelsius, float humidity)
{
    var temperatureFahrenheit = CelsiusToFahrenheit(temperatureCelsius);
    Console.WriteLine("Comfort Index for " + location + ": " + ComfortIndex(temperatureFahrenheit
```

These methods build upon our earlier example. So we have the conversion from Fahrenheit to Celsius, so you probably remember this one, and also the other way around, from Celsius to Fahrenheit. I also added this method that calculates something called the ComfortIndex. It takes a temperature and humidity in percent, so a number from 0 to 100. And it returns an arbitrary index that essentially tells you how pleasant it is to do physical exercise at this temperature and humidity. This idea of comfort is a vague concept. There are many possible ways to calculate comfort or perceived temperature and similar indexes. This formula that I found on the

internet is just temperature plus humidity divided by 4, and the lower the index, the more comfortable it is to do physical exercise. It's certainly not a very reliable index, but it's simple and it kind of works for average temperatures and humidity, so it will do for now. And finally, we have this Report() method. It takes a string that's supposed to be the name of a place and its temperature and humidity and prints a short report on the screen that shows the comfort index for this location. The + operator applied to strings means concatenate these strings. So this is the string Comfort Index for, followed by the name of the location, then a colon, then the ComfortIndex calculated by this other method. Note that the ComfortIndex is not a string; it's a float. But when we concatenate it to a string, C# converts it automatically from float to string. We know that C# is fussy about types, so it won't let us convert types implicitly, unless it's a safe conversion we're talking about and this one is a safe conversion. You can always convert a floating point number to a string without getting an error, so it's okay to have a float concatenated to a string, like here. So, this is the class I came up with. I called it a library class. But speaking of that, we need to take digression about this concept of a library. I told you that I wrote this class that contains utility methods, and it's like a little library. And I this class in the project to use it from our program. Just to be clear, I don't want to give you the wrong message and encourage you to code like that. In most cases, when you want to share functionality like a library, you import the compiled library, not the source code of the library. If you're used to compiled languages, you're thinking, of course. But if you're more used to interpreted languages, then it's worth spending a moment on this distinction. You remember that I told you earlier on that a C# project results in an assembly, a file or sometimes a small bunch of files? So, let's say that we have a project that delivers a Windows executable, and this

project depends on a library, a DLL. In general, you don't need the source code of the library; you just take the compiled library, a DLL file, put it into the project, and tell Visual Studio that the project depends on the DLL. Then when you compile the project, Visual Studio will put both the executable and the DLL in the same directory so that the executable can see the DLL and everything works at runtime. And there are other ways to make a DLL visible to a project in Visual Studio. You can put the DLL in a global area on your machine that's visible to any project or install the library from the internet using the NuGet package manager, all stuff that's outside the scope of this book. But one thing is common to all these cases: you don't the source code. You generally share compiled code, not source code. The reason why I source code in our case is that we want to modify this code, and that's what we're going to do next. There are a few things that we can improve in this class before we go on and use it in our program, small things, but they kind of add up. First, we could add comments. I did try to make this code to use explicit names for variables like here and so on, but sometimes you just need a comment. For example, we said that this formula that calculates the comfort index is probably not the most accurate way to do it, so let's write a comment about that. If you type a double slash, everything that follows is a comment, up to the end of the line. To be honest, this is the kind of comment that I end up regretting because then I come back to my code after a while and I should have fixed this code instead of commenting that it's not so great. But in this case I plan to stop updating this code as soon as I finish this writing book, so maybe this time I'll get away with it. Another thing worth commenting is, when we call ComfortIndex(), we need to remember that higher indexes mean less comfort. That's not very intuitive. It's easy to get wrong. So let's write a comment about

that. We've seen comments with a double slash, but there are other flavors of comments in C# as well.

```
```csharp
// This is a comment until the end of the line

/*
 * This is a comment that
 * spans multiple lines.
 */

/// <summary>This is a <i>formatted</i> comment.</summary>
```
```

You can write a comment that spans multiple lines, delimited by a slash star sequence in the beginning and a star slash sequence in the end. And many people also had a few more asterisks to make it look nicer. And you can also write comments with advanced formatting, used to generate documentation for classes and methods and so on. But double slashes are probably the most common way to comment code. Besides comments, another small improvement we can make to this class is, this method defines a variable and then returns it, but we don't need this intermediate variable. We can do the calculation and return the result straightaway. It's a little refactoring, as they call it, an internal change that doesn't change the behavior of the code, because this method returns the same result as before. But most programmers would find it a bit easier to read. These two methods also create temporary variables that we can remove, but this time, instead of doing it by hand, let's ask Visual Studio to do it for us.
