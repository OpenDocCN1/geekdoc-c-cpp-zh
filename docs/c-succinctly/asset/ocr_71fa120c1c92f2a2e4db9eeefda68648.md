The code in `pchar.h` gives us a reasonably portable entry point, while the `int _pmain(int, _pchar*[])` entry point itself ensures that we will never use the passed-in command-line arguments. If you ever need the command-line arguments, then this solution will not work—you will need a more advanced, more complicated solution.

# ## Arguments and Parameters

I use the terms *argument* and *parameter* at various points in this book. To me, an argument is a value that is passed in to a function when called in a program, whereas a parameter is part of the specification of a function that tells the programmer the function is expecting to receive a value of a certain type. It also tells the programmer how it might treat that value. A parameter typically provides a name by which that value can be referenced, though C++ allows us to provide just a type if we are required to have a particular parameter (e.g., to match an interface specification) but do not intend to actually use its value.

As an example of a parameter versus an argument, in C# you might have a class method such as `void AddTwoNumbers(int a, int b, ref int result) { result = a + b; }`. In this case, `a`, `b`, and `result` are parameters; we know that `AddTwoNumbers` might change the value of the argument passed in for the result parameter (as, indeed, it does). If you called this method as so, `int one = 1, two = 2, answer = 0; someClass.AddTwoNumbers(one, two, ref answer);` then `one`, `two`, and `answer` would all be arguments passed in to `AddTwoNumbers`.

# ## Syntax Highlighting

The code examples in this book use the syntax-highlighting colors from Visual Studio 2012 Ultimate RC. This will help you understand the code, but you will also be fine reading this on a monochrome e-book reader.

# ## Samples

The samples in this book are available at [https://bitbucket.org/syncfusion/cpp_succinctly](https://bitbucket.org/syncfusion/cpp_succinctly).

The samples for this book were designed and developed using Visual Studio 2012 Ultimate RC. The C++ compiler that comes with VS 2012 includes new features of the C++11 language standard that were not included in Visual Studio 2010. In the fall of 2012, Microsoft will release a free “Express” version of Visual Studio 2012, which will allow developers to use C++ targeted desktop applications (such as the console application, which the samples use). Until then, to make full use of the samples, you will need a non-Express version of Visual Studio 2012.

I tested many of the samples along the way using Minimalist GNU for Windows (MinGW), so there should be a lot of cross-compiler portability. The one sample I know for sure that does not work as written with the GCC compiler that MinGW provides is `StorageDurationSample`. It makes use of the Microsoft-specific language extension `__declspec(thread)` in order to simulate `thread_local` storage. GCC has its own very similar extension, and other compiler vendors undoubtedly do too, so if you replace that with the appropriate code for the compiler you decide to use, it should then compile and run.

Lastly, the samples are all console samples. I chose console samples so we could avoid all the extraneous code that comes with creating and displaying windows within a windowing environment. To see the output of any particular sample, you can either set a breakpoint on the return statement at the end of the `_pmain` function and then run it using the Visual Studio debugger, or you can run it using the **Start Without Debugging** command in the **Debug** menu in Visual Studio (typically this uses the **Ctrl+F5** keyboard shortcut). You also need to make sure that the project you wish to run is set as the start-up project. You can accomplish this by right-clicking on the project’s name in Solution Explorer and then left-clicking on **Set as Startup Project** in the context menu that appears.