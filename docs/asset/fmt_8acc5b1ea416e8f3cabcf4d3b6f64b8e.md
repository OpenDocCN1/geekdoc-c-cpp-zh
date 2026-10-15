
```csharp
using static System.Console;

class HeyYou
{
    static void Main()
    {
        string firstName;
        string lastName;

        WriteLine("Hey you!");

        Write("Enter your first name: ");

        firstName = ReadLine();
        Write("Enter your last name: ");
        lastName = ReadLine();
        WriteLine(
            $"Your full name is { firstName } { lastName }.");
    }
}
```

In this case, there is no loss of readability of the code: `WriteLine()`, `Write()`, and `ReadLine()` all clearly relate to a console directive. In fact, one could argue that the resulting code is simpler and, therefore, clearer than before.

However, sometimes this is not the case. For example, if your code uses classes that have overlapping behavior names, such as an `Exists()` method on a file and an `Exists()` method on a directory, then perhaps a `using static` directive would reduce clarity when you invoke `Exists()`. Similarly, if the class you were writing had its own members with overlapping behavior names to those imported with a `using static` statement—for example, `Display()` and `Write()`—then perhaps clarity would be lost to the reader.

This ambiguity would not be allowed by the compiler. If two members with the same signature were available (through either `using static` directives or separately declared members), any invocation of them that was ambiguous would result in a compile error.

## Aliasing

The `using` directive also allows **aliasing** a namespace or type. An alias is an alternative name that you can use within the text to which the `using` directive applies. The two most common reasons for aliasing are to disambiguate two types that have the same name and to abbreviate a long name. In Listing 4.9, for example, the `CountDownTimer` alias is declared as a means of referring to the type `System.Timers.Timer`. Simply adding a `using System.Timers` directive will not sufficiently enable the code to avoid fully qualifying the `Timer` type. The reason is that `System.Threading` also includes a type called `Timer`; therefore, just using `Timer` within the code will be ambiguous.

```csharp
using System;
using System.Threading;
using CountDownTimer = System.Timers.Timer;

class HelloWorld
{
    static void Main()
    {
        CountDownTimer timer;

        // ...
    }
}
```

Listing 4.9 uses an entirely new name, `CountDownTimer`, as the alias. It is possible, however, to specify the alias as `Timer`, as shown in Listing 4.10.

### LISTING 4.10: Declaring a Type Alias with the Same Name

```csharp
using System;
using System.Threading;

// Declare alias Timer to refer to System.Timers.Timer to
// avoid code ambiguity with System.Threading.Timer
using Timer = System.Timers.Timer;

class HelloWorld
{
    static void Main()
    {
        Timer timer;

        // ...
    }
}
```

Because of the alias directive, “Timer” is not an ambiguous reference. Furthermore, to refer to the `System.Threading.Timer` type, you will have to either qualify the type or define a different alias.

## Returns and Parameters on `Main()`

So far, declaration of an executable’s `Main()` method has been the simplest declaration possible. You have not included any parameters or non-void return type in your `Main()` method declarations. However, C# supports the ability to retrieve the command-line arguments when executing a program, and it is possible to return a status indicator from the `Main()` method.

The runtime passes the command-line arguments to `Main()` using a single string array parameter. All you need to do to retrieve the parameters is to access the array, as demonstrated in Listing 4.11. The purpose of this program is to download a file whose location is given by a URL. The first command-line argument identifies the URL, and the optional second argument is the filename to which to save the file. The listing begins with a switch statement that evaluates the number of parameters (`args.Length`) as follows:

- 1. If there are not two parameters, display an error indicating that it is necessary to provide the URL and filename.

- 2. The presence of two arguments indicates the user has provided both the URL of the resource and the download target filename.

### LISTING 4.11: Passing Command-Line Arguments to `Main()`

```csharp
using System;
using System.Net;

class Program
{
    static int Main(string[] args)
    {
        int result;
        string targetFileName;
        string url;
        switch (args.Length)
        {
            default:
                // Exactly two arguments must be specified; give an error.
                Console.WriteLine(
                    "ERROR: You must specify the "
                    + "URL and the file name");
                targetFileName = null;
                url = null;
                break;
            case 2:
                url = args[0];
                targetFileName = args[1];
                break;
        }

        if (targetFileName != null && url != null)
        {
            WebClient webClient = new WebClient();
            webClient.DownloadFile(url, targetFileName);
            result = 0;
        }
        else
        {
            Console.WriteLine(
                "Usage: Downloader.exe <URL> <TargetFileName>");
            result = 1;
        }
        return result;
    }
}
```

The results of Listing 4.11 appear in Output 4.4.

### OUTPUT 4.4

```text
>Downloader.exe
ERROR: You must specify the URL to be downloaded
Downloader.exe <URL> <TargetFileName>
```

If you were successful in calculating the target filename, you would use it to save the downloaded file. Otherwise, you would display the help text. The `Main()` method also returns an int rather than a void. This is optional for a `Main()` declaration, but if it is used, the program can return a status code to a caller (such as a script or a batch file). By convention, a return other than zero indicates an error.

Although all command-line arguments can be passed to `Main()` via an array of strings, sometimes it is convenient to access the arguments from inside a method other than `Main()`. The `System.Environment.GetCommandLineArgs()` method returns the command-line arguments array in the same form that `Main(string[] args)` passes the arguments into `Main()`.

## ADVANCED TOPIC

### Disambiguate Multiple `Main()` Methods

If a program includes two classes with `Main()` methods, it is possible to specify on the command line which class to use for the `Main()` declaration. `csc.exe` includes an `/m` option to specify the fully qualified class name of `Main()`.

## BEGINNER TOPIC

### Call Stack and Call Site

As code executes, methods call more methods, which in turn call additional methods, and so on. In the simple case of Listing 4.4, `Main()` calls `GetUserInput()`, which in turn calls `System.Console.ReadLine()`, which in turn calls even more methods internally. Every time a new method is invoked, the runtime creates an “activation frame” that contains information about the arguments passed to the new call, the local variables of the new call, and information about where control should resume when the new method returns. The set of calls within calls within calls, and so on, produces a series of activation frames that is termed the **call stack**. As program complexity increases, the call stack generally gets larger and larger as each method calls another method. As calls complete, however, the call stack shrinks until another method is invoked. The process of removing activation frames from the call stack is termed **stack unwinding**. Stack 展开总是以与方法调用相反的顺序发生。当方法完成时，执行将返回到调用点——即调用该方法的位置。

## 高级方法参数

到目前为止，本章的示例都是通过方法的返回值返回数据。本节演示了方法如何通过其方法参数返回数据，并展示了方法如何接受可变数量的参数。

### 值参数

方法调用的参数通常按值传递，这意味着参数表达式的值会被复制到目标参数中。例如，在清单 4.12 中，`Main()` 在调用 `Combine()` 时使用的每个变量的值都会被复制到 `Combine()` 方法的参数中。输出 4.5 显示了该清单的结果。

#### LISTING 4.12: Passing Variables by Value
