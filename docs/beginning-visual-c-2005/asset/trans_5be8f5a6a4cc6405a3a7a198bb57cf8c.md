

# 第6章

由于你在此处提取的字符串包含用括号括起的子表达式，最终会再次调用 extract() 来处理这些子表达式。

函数 extract() 还需要为子字符串分配内存并返回指向它的指针。当然，原始字符串中当前位置的索引最终需要选择子字符串之后的字符，因此该参数需要指定为引用。因此，extract() 的原型如下：

```
char* extract(char* str, int& index); //Function to extract a substring
```

你现在可以尝试该函数的定义。

```
// Function to extract a substring between parentheses
// (requires <cstring> header file)
char* extract(char* str, int& index)
{
    char buffer[MAX];                 // Temporary space for substring
    char* pstr = 0;                   // Pointer to new string for return
    int numL = 0;                     // Count of left parentheses found
    int bufindex = index;             // Save starting value for index

    do
    {
        buffer[index - bufindex] = *(str + index);
        switch(buffer[index - bufindex])
        {
            case ')':
                if(numL == 0)
                {
                    buffer[index - bufindex] = '\0';  // Replace ')' with '\0'
                    ++index;
                    pstr = new char[index - bufindex];
                    if(!pstr)
                    {
                        cout << "Memory allocation failed," << " program terminated.";
                        exit(1);
                    }
                    strcpy_s(pstr, index-bufindex, buffer); // Copy substring to new memory
                    return pstr;               // Return substring in new memory
                }
                else
                    numL--;                   // Reduce count of '(' to be matched
                break;

            case '(': 
                numL++;                   // Increase count of '(' to be
                                          // matched
                break;
        }
    } while(*(str + index++) != '\0');   // Loop - don't overrun end of string

    cout << "Ran off the end of the expression, must be bad input."
    << endl;
    exit(1);
    return pstr;
}

## 函数如何工作

你声明一个 char 数组来临时保存子字符串。你不知道子字符串有多长，但它不能超过 MAX 个字符。你不能将 buffer 的地址返回给调用函数，因为它是局部的，在函数退出时会销毁；因此，当你知道字符串长度时，需要在自由存储区上分配一些内存。你通过声明一个类型为‘指向 char 的指针’的变量 pstr 来实现这一点，当你将子字符串安全地保存在自由存储区内存中时，通过值返回它。

你声明一个计数器 numL 来跟踪子字符串中的左括号（正如我之前讨论的那样）。index 的初始值（函数开始执行时）存储在变量 bufindex 中。你将它与 index 的递增值结合起来对数组 buffer 进行索引。

函数的可执行部分基本上是一个大的 do-while 循环。子字符串从 str 复制到 buffer，每次循环迭代复制一个字符，同时在每个周期检查左括号或右括号。如果找到左括号，numL 会递增，如果找到右括号且 numL 非零，则会递减。当你找到右括号且 numL 为零时，你就找到了子字符串的末尾。然后用‘\0’替换 buffer 中子字符串中的‘)’，并在自由存储区上获取足够的内存来容纳子字符串。然后使用 <cstring> 头文件中声明的 strcpy_s() 函数将 buffer 中的子字符串复制到你通过 new 运算符获得的内存中；这是在同一头文件中声明的旧 strcpy() 函数的安全版本。此函数将第三个参数 buffer 指定的字符串复制到第一个参数 pstr 指定的地址。第二个参数是目标字符串 pstr 的长度。

如果你从循环底部掉出来，这意味着你在 str 中表达式末尾的‘\0’处命中，而没有找到对应的右括号，因此你显示一条消息并终止程序。

## 运行修改后的程序

在旧版本的程序中替换 number() 函数后，添加 <cstring> 的 #include 语句，并合并你刚刚编写的新 extract() 函数的原型和定义，你就可以使用一个全功能的全能计算器了。如果你在没有错误的情况下组装了所有这些，你可以得到类似这样的输出：

```
Welcome to your friendly calculator.
Enter an expression, or an empty line to quit.
1/(1+1/(1+1/(1+1)))
    = 0.6

(1/2-1/3)*(1/3-1/4)*(1/4-1/5)
    = 0.000694444

3.5*(1.25-3/(1.333-2.1*1.6))-1
    = 8.55507

2,4-3.4

Arrrgh!*#!! There's an error
```

最后输出行中友好而信息丰富的错误消息是由于在上面的表达式中使用了逗号而不是小数点，在本应为 2.4 的地方。正如你所见，你可以用相对简单的程序扩展来获得任意深度的嵌套括号，这全都归功于递归的惊人威力。

## C++/CLI 编程

到目前为止关于原生 C++ 函数所讨论的几乎所有内容同样适用于 C++/CLI 语言代码，前提是参数类型和返回类型将是基本类型，你知道它们等同于 CLR 程序中的值类类型，跟踪句柄类型或跟踪引用类型。因为你不能对存储在跟踪句柄中的地址执行算术运算，我为将参数作为指针进行算术运算的原生 C++ 数组所演示的编码技术不适用于 C++/CLI 数组。许多原生 C++ 函数参数可能出现的问题消失了，但在 C++/CLI 中对粗心的人来说仍有一些陷阱。计算器的 CLR 版本可以帮助你理解函数在 C++/CLI 中编写的样子。

throw 和 catch 异常机制在 CLR 程序中与原生 C++ 程序中工作方式相同，但有一些差异。在 C++/CLI 程序中抛出的异常必须始终使用跟踪句柄抛出。因此你应该始终抛出异常对象，尽可能避免抛出字面量，尤其是字符串字面量。例如，考虑这段 try-catch 代码：

```
try
{
    throw L"Catch me if you can.";
}
catch(String^ ex)                // The exception will not be caught by this
{
    Console::WriteLine(L"String^: {0}",ex);
}
```

catch 块无法捕获此处抛出的对象，因为 throw 语句抛出的是类型为 const wchar_t* 的异常，而不是类型为 String^ 的异常。要按抛出方式捕获异常，catch 块需要是：

```
try
{
    throw L"Catch me if you can.";
}
catch(const wchar_t* ex)          // OK. The exception thrown is of this type
{
    String^ exc = gcnew String(ex);
    Console::WriteLine(L"wchar_t*: {0}", exc);
}
```

这个 catch 块捕获了异常，因为它现在具有正确的类型。

要抛出异常以便能被原始的 catch 块捕获，你必须更改 try 块中的代码：

```
try
{
    throw gcnew String(L"Catch me if you can.");
}
catch(String^ ex)                // OK. Exception thrown is of this type
{
    Console::WriteLine(L"String^: {0}",ex);
}
```

现在异常是一个 String 对象，并作为类型 String^ 的句柄抛出，该句柄引用字符串。

你可以在 C++/CLI 程序中使用函数模板，但你还有一个称为泛型函数的额外功能，看起来非常相似；然而，两者存在显著差异。

## 理解泛型函数

尽管泛型函数看起来与函数模板做同样的事情，因此乍一看似乎是多余的，但泛型函数的工作方式与模板函数大不相同，而这些差异使它们成为 CLR 程序中宝贵的额外功能。当你使用函数模板时，编译器会从模板生成你需要的函数的源代码；然后生成的代码会与你的其余程序代码一起编译。在某些情况下，这可能会生成许多函数，并且可执行模块的大小可能会大幅增加。另一方面，泛型函数规范本身会被编译，并且当你调用匹配泛型函数规范的函数时，实际类型会在执行时替换类型参数。编译时不会生成额外代码，也不会出现模板函数可能出现的代码膨胀。

定义泛型函数的某些方面依赖于后面章节中才会出现的知识，但最终一切都会清楚。我将在此处对新事物提供最少的解释，你将在本书后面学习细节。

## 定义泛型函数

你使用在函数调用时被实际类型替换的类型参数来定义泛型函数。以下是泛型函数定义的示例：

```
generic<typename T> where T:IComparable
T MaxElement(array<T>^ x)
{
    T max = x[0];
    for(int i = 1; i < x->Length; i++)
        if(max->CompareTo(x[i]) < 0)
            max = x[i];
    return max;
}
```

