# Chapter 155: Interoperability

# Section 155.1: Import function from unmanaged C++ DLL

Here is an example of how to import a function that is defined in an unmanaged C++ DLL. In the C++ source code for "myDLL.dll", the function add is defined:

```
```cpp
extern "C" __declspec(dllexport) int __stdcall add(int a, int b)
{
    return a + b;
}
```
```

Then it can be included into a C# program as follows:

```
```csharp
class Program
{
    // This line will import the C++ method.
    // The name specified in the DllImport attribute must be the DLL name.
    // The names of parameters are unimportant, but the types must be correct.
    [DllImport("myDLL.dll")]
    private static extern int add(int left, int right);

    static void Main(string[] args)
    {
        //The extern method can be called just as any other C# method.
        Console.WriteLine(add(1, 2));
    }
}
```
```

See Calling conventions and C++ name mangling for explanations about why extern "C" and __stdcall are necessary.

# Finding the dynamic library

When the extern method is first invoked the C# program will search for and load the appropriate DLL. For more information about where is searched to find the DLL, and how you can influence the search locations see this stackoverflow question.

# Section 155.2: Calling conventions

There're several conventions of calling functions, specifying who (caller or callee) pops arguments from the stack, how arguments are passed and in what order. C++ uses Cdecl calling convention by default, but C# expects StdCall, which is usually used by Windows API. You need to change one or the other:

+   - Change calling convention to StdCall in C++:
+   ```cpp
+   extern "C" __declspec(dllexport) int __stdcall add(int a, int b)
+   ```
+   `[DllImport("myDLL.dll")]`
+   - Or, change calling convention to Cdecl in C#:
+   ```cpp
+   extern "C" __declspec(dllexport) int /*__cdecl*/ add(int a, int b)
+   ```
+   `[DllImport("myDLL.dll", CallingConvention = CallingConvention.Cdecl)]`