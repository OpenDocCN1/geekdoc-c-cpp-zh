
Turns out with var you can reach a similar effect. But ideally, you still want to see the type, don't you? That's what the whole argument for some people is all about. Turns out you sort of can force the type in there if you really want:

```
var x = (int)42;
var y = (string)"Hello";
var z = new List<Person>();
```

Now I don't recommend this practice. That's why this sidebar is titled a "philosophical note." Turns out there are hidden caveats. Runtime costs, not really. But assume you have a complex expression as the right side of an assignment and you inserted the wrong cast. Casts are about stating you somehow know more than the compiler, telling it to try a conversion between types at runtime (as discussed in Chapter 6, "A Primer on Types and Objects," in the section, "Cast Expressions"). Chances are that your code compiles just fine but blows up at runtime. This is definitely worse than what we started from.

## Intermezzo on Comments

So far, we've dealt with some of the program text the compiler cares about the most. If you make mistakes with regard to syntax or more involved rules, you'll be punished and prompted to correct the error. As valuable as source code itself are comments to document the code. Even though good source code should be self-explanatory for the most part— because of the use of meaningful identifier names and so on—correct use of comments is invaluable, too.

Being a C-style language, C# inherits a few of its commenting styles from that group of languages. Let's take a look.

## Single-Line Comments

A single-line comment starts with two consecutive forward slashes and stretches until the end of the source line. You've seen numerous examples of this style already:

```
// Bad
var mystery = GetSomething(); // what's the return type of GetSomething?
var x = 2159940436;           // answer immediately: int or long?
```

As you can see, the comment doesn't necessarily need to stand on its own in a line of code; it can also be used just at the end of a line after some meaningful source code. But it can't be used in the middle of a line of code because there's no way to terminate the run of comment text.

This style of commenting has a technical advantage: There are no worries about nesting of comments, which—as you will see in the next section—can be problematic. For this reason, Visual Studio provides tooling support for this commenting style, typically used to “comment out” a bunch of source code, as shown in Figure 4.24.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_250_0.png)

FIGURE 4.24 Single-line commenting a block of code in Visual Studio.

### TIP

Don’t leave large chunks of commented-out source code behind in code files; most people find it very distracting when reading code. Even though you’ve deleted a large portion of code because you found a better way to approach the problem, the old code might still be of value for archeological purposes. A better way to keep track of those changes is to use a decent source control system from which you can consult the history of source code files. Or if you really want to drop a hint in the source code, leave just the essence of the original problem behind to help others avoid repeating the same mistakes.

The Visual Studio editor uses a different colorization scheme for comments in source text. The default color is green, but you can change that.

## A Primer to Preprocessing Directives

Use the Visual Studio feature to comment out blocks of code while evolving the code at development time. If you find yourself doing this quite often (for example, to enable or disable some diagnostic code), you’re likely better off with conditional compilation using an #if preprocessing directive. We won’t detail the preprocessing capabilities (which is really a misnomer in the world of C# because there’s no separate preprocessor stage in compilation) right now, but here’s the crux of it.

Using the #define directive, a symbol can be defined for further use in conditional preprocessing directives like #if. Blocks of code surrounded by #if and #endif are conditionally included in the source code analyzed by the compiler, based on whether the conditioning symbol is defined:

```
using System;

class Program
{
    static void Main(string[] args)
    {
#if DEBUG
        Console.WriteLine("Some diagnostic output:");
        Console.WriteLine(DateTime.Now);
#endif

        foreach (string arg in args)
        {
            Console.WriteLine(arg);
        }
    }
}
```

The DEBUG symbol I'm using in the preceding fragment is automatically set when using the Debug mode in Visual Studio. In Release mode, it isn't. You can define your own symbols using #define in the source text or by specifying the symbols to be set to a compiler flag. The Project Properties dialog's Build tab provides easy access to this setting, illustrated in Figure 4.25.

![](img/a16f85e62ce9bdc527f4b09dbfe26092_251_0.png)

FIGURE 4.25 Defining symbols for conditional compilation.

### TIP

Conditional compilation is a very powerful beast to maintain different build flavors of the same source code. For example, large portions of the BCL are compiled for the “desktop CLR” as well as for Silverlight. To accommodate for the slight differences required here and there, conditional compilation is used.

As an example, consider the following piece of code:

```
/*
int x = 5;

/* Long comment starts here
 * ...
 */

Console.WriteLine("Some diagnostic output:");
Console.WriteLine(DateTime.Now);
*/
```

Here, the last */ isn't paired up with a starting /* sequence, causing a compilation error. In Visual Studio, because of correct colorization, you'll see this immediately.

## Documentation Comments

The first goal of API writers obviously is to deliver a binary with the desired library functionality. But without decent documentation, it's often of little use for the consumers of it. No matter how good the naming of types and public members is, additional information on the intended behavior, caveats, and so on is invaluable, too.

To stimulate this practice and provide a structured approach for dealing with it, the C# specification defines the concept of documentation comments. They're only defined meaningfully when applied to user-defined types or members, where the compiler knows how to export them into a documentation file.

Documentation comments are based on XML to structure the different parts of documentation required. Two styles can be used to write them down, either by starting with a sequence of three forward slashes (///) or by using an extended version of delimited comments with an additional asterisk (/**). The former is preferred because Visual Studio helps you a lot. Third-party tools exist that help with the generation of comments as well. One sample is GhostDoc, which can be found through the Visual Studio Gallery of add-ins on MSDN.

For example, assume we've written a little Calculator class (cheesy, I know):

```
public static class Calculator
{
    public static int Add(int a, int b)
    {
        return a + b;
    }
}
```

Don’t worry about the use of various modifiers such as static, which will become clear pretty soon. Suffice it to say I’m using best practices here by defining a stateless class as a static class.

Parts of the code that will benefit from documentation comments are the class itself, its public methods, and the parameters and the returned data. In this case, it’s fairly obvious what the meaning is, but you can imagine much more involved definitions.

In Visual Studio, you can make the editor generate a template for required documentation by typing the /// sequence on the line in front of the entity to be documented. In Figure 4.26, I’ve done this for both the class and its Add method.

```
```csharp
/// <summary>
///
/// </summary>
public static class Calculator
{
    /// <summary>
    ///
    /// </summary>
    /// <param name="a"></param>
    /// <param name="b"></param>
    /// <returns></returns>
    public static int Add(int a, int b)
    {
        return a + b;
    }
}
```
```

FIGURE 4.26 Generating documentation comments.

All you have to do now is supply some meaningful documentation. To make documentation as structured as possible, different tags are available, one of which appears in Figure 4.27.

```
```csharp
/// <summary>
/// Adds the numbers in <param...
/// </summary>
/// <param name="a"></param>
/// <param name="b"></param>
/// <returns></returns>
public static int Add(int a, int b)
{
    return a + b;
}
```
```

FIGURE 4.27 IntelliSense for different tags is available.

Rich documentation on writing documentation comments is available in the MSDN library. The logical next question is how this documentation is emitted. First off, you need to tell the compiler to generate a documentation file. In Visual Studio, the one-stop shop for all such settings is the project’s Properties window.
