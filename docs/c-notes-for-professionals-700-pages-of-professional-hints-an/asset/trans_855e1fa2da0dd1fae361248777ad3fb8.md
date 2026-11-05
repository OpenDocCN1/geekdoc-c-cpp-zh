
```
}
Console.WriteLine(s); // The variable 's' still refers to the same System.String
// value in memory, but the contents at that location were
// changed by the unsafe write above.
// Displays: "aaaaa"
```

### 第 152.3 节：不安全数组索引

```
void Main()
{
    unsafe
    {
        int[] a = {1, 2, 3};
        fixed(int* b = a)
        {
            Console.WriteLine(b[4]);
        }
    }
}
```

运行此代码会创建一个长度为 3 的数组，但随后尝试获取第 5 个元素（索引 4）。在我机器上，这打印出了 1910457872，但行为未定义。

如果没有 unsafe 块，就无法使用指针，因此无法在不引发异常的情况下访问数组末尾之后的值。

## 第 153 章：C# 脚本

### 第 153.1 节：简单代码求值

你可以求值任何有效的 C# 代码：

```
int value = await CSharpScript.EvaluateAsync<int>("15 * 89 + 95");
var span = await CSharpScript.EvaluateAsync<TimeSpan>("new DateTime(2016,1,1) - DateTime.Now");
```

如果未指定类型，结果为 object：

```
object value = await CSharpScript.EvaluateAsync("15 * 89 + 95");
```

## 第 154 章：运行时编译

### 第 154.1 节：RoslynScript

Microsoft.CodeAnalysis.CSharp.Scripting.CSharpScript 是一个新的 C# 脚本引擎。

```csharp
var code = "(1 + 2).ToString()";
var run = await CSharpScript.RunAsync(code, ScriptOptions.Default);
var result = (string)run.ReturnValue;
Console.WriteLine(result); //output 3
```

你可以编译并运行任何语句、变量、方法、类或任何代码片段。

### 第 154.2 节：CSharpCodeProvider

Microsoft.CSharp.CSharpCodeProvider 可用于编译 C# 类。

```csharp
var code = @"
    public class Abc {
        public string Get() { return "abc"; }
    }
";

var options = new CompilerParameters();
options.GenerateExecutable = false;
options.GenerateInMemory = false;

var provider = new CSharpCodeProvider();
var compile = provider.CompileAssemblyFromSource(options, code);

var type = compile.CompiledAssembly.GetType("Abc");
var abc = Activator.CreateInstance(type);

var method = type.GetMethod("Get");
var result = method.Invoke(abc, null);

Console.WriteLine(result); //output: abc
```

## 第 155 章：互操作性

### 第 155.1 节：从非托管 C++ DLL 导入函数

以下是如何导入在非托管 C++ DLL 中定义的函数的示例。在 "myDLL.dll" 的 C++ 源代码中，函数 add 被定义为：

```cpp
extern "C" __declspec(dllexport) int __stdcall add(int a, int b)
{
    return a + b;
}
```

然后它可以按如下方式包含到 C# 程序中：

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

请参阅 Calling conventions 和 C++ name mangling 以了解为何 extern "C" 和 __stdcall 是必要的。

### 查找动态库

当首次调用 extern 方法时，C# 程序会搜索并加载适当的 DLL。有关在何处搜索 DLL 以及如何影响搜索位置的更多信息，请参阅此 stackoverflow 问题。

### 第 155.2 节：调用约定

有几种调用函数的约定，指定谁（调用方或被调用方）从栈中弹出参数、参数如何传递以及传递顺序。C++ 默认使用 Cdecl 调用约定，但 C# 期望 StdCall，这通常由 Windows API 使用。你需要更改其中之一：

- 在 C++ 中将调用约定更改为 StdCall：
```cpp
extern "C" __declspec(dllexport) int __stdcall add(int a, int b)
```
[DllImport("myDLL.dll")]
- 或者，在 C# 中将调用约定更改为 Cdecl：
```cpp
extern "C" __declspec(dllexport) int /*__cdecl*/ add(int a, int b)
```
[DllImport("myDLL.dll", CallingConvention = CallingConvention.Cdecl)]

如果你想使用具有 Cdecl 调用约定且名称被修饰的函数，你的代码将如下所示：

```
__declspec(dllexport) int add(int a, int b)
```

```
[DllImport("myDLL.dll", CallingConvention = CallingConvention.Cdecl, EntryPoint = "?add@@YAHHH@Z")]
```

- thiscall(__thiscall) 主要用于类成员函数中。
- 当函数使用 thiscall(__thiscall) 时，会将指向该类的指针作为第一个参数传递下去。

### 第 155.3 节：C++ 名称修饰

C++ 编译器会在导出的函数名称中编码额外信息，例如参数类型，以便使具有不同参数的重载成为可能。此过程称为名称修饰。这会导致在 C# 中导入函数（以及与其他语言的互操作）时出现问题，因为 int add(int a, int b) 函数的名称不再是 add，它可能是 ?add@YAHHH@Z、_add@8 或其他任何内容，具体取决于编译器和调用约定。

有几种解决名称修饰问题的方法：

- 使用 extern "C" 导出函数以切换到 C 外部链接，该链接使用 C 名称修饰：
```
extern "C" __declspec(dllexport) int __stdcall add(int a, int b)
```

```
[DllImport("myDLL.dll")]
```

函数名仍会被修饰（_add@8），但 C# 编译器可以识别 StdCall+extern "C" 名称修饰。

- 在 myDLL.def 模块定义文件中指定导出的函数名称：
```
EXPORTS
add
```

```
int __stdcall add(int a, int b)
```

```
[DllImport("myDLL.dll")]
```

在这种情况下，函数名将为纯 add。

- 导入被修饰的名称。你需要一些 DLL 查看器来查看被修饰的名称，然后可以显式指定它：
```
__declspec(dllexport) int __stdcall add(int a, int b)
```

```
[DllImport("myDLL.dll", EntryPoint = "?add@YAHHH@Z")]
```

### 第 155.4 节：动态加载和卸载非托管 DLL

使用 DllImport 属性时，你必须在编译时知道正确的 dll 和方法名称。如果你想更灵活并在运行时决定加载哪个 dll 和方法，可以使用 Windows API 方法 LoadLibrary()、GetProcAddress() 和 FreeLibrary()。如果要使用的库取决于运行时条件，这会很有帮助。

GetProcAddress() 返回的指针可以使用 [Marshal.GetDelegateForFunctionPointer()]() 转换为委托。

以下代码示例使用前面的示例中的 myDLL.dll 演示了这一点：

```csharp
class Program
{
    // import necessary API as shown in other examples
    [DllImport("kernel32.dll", SetLastError = true)]
    public static extern IntPtr LoadLibrary(string lib);
    [DllImport("kernel32.dll", SetLastError = true)]
    public static extern void FreeLibrary(IntPtr module);
    [DllImport("kernel32.dll", SetLastError = true)]
    public static extern IntPtr GetProcAddress(IntPtr module, string proc);

    // declare a delegate with the required signature
    private delegate int AddDelegate(int a, int b);

    private static void Main()
    {
        // load the dll
        IntPtr module = LoadLibrary("myDLL.dll");
        if (module == IntPtr.Zero) // error handling
        {
            Console.WriteLine($"Could not load library: {Marshal.GetLastWin32Error()}");
            return;
        }

        // get a "pointer" to the method
        IntPtr method = GetProcAddress(module, "add");
        if (method == IntPtr.Zero) // error handling
        {
            Console.WriteLine($"Could not load method: {Marshal.GetLastWin32Error()}");
            FreeLibrary(module);  // unload library
            return;
        }

        // convert "pointer" to delegate
        AddDelegate add = (AddDelegate)Marshal.GetDelegateForFunctionPointer(method, typeof(AddDelegate));

        // use function
        int result = add(750, 300);

        // unload library
        FreeLibrary(module);
    }
}
```

### 第 155.5 节：使用 Marshal 读取结构

Marshal 类包含一个名为 **PtrToStructure** 的函数，该函数使我们能够通过非托管指针读取结构。

**PtrToStructure** 函数有许多重载，但它们都具有相同的意图。

泛型 **PtrToStructure**：
