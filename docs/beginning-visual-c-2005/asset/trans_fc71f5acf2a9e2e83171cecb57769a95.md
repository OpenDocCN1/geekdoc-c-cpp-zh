

你可以看到这些属性值的意义，设置 Level 属性也会设置这些属性的状态。例如，如果你将 Level 属性设置为 TraceLevel::Warning，则 TraceWarning 和 TraceError 被设置为 true，而 TraceVerbose 和 TraceInfo 被设置为 false。

要决定是否输出特定消息，只需测试相应的属性：

```cpp
if(traceCtrl->TraceWarning)
    Debug::WriteLine(L"This is your last warning!");
```

只有当 traceCtrl 的 TraceWarning 属性为 true 时，消息才会被输出。

## 断言

Debug 和 Trace 类都有静态 Assert() 函数，其功能与原生 C++ assert() 函数类似。Debug::Assert() 函数的第一个参数是一个 bool 值或表达式，当参数为 false 时程序会触发断言。然后调用堆栈会显示在对话框中，如图 10-20 所示。

![](img/2359b0c604600c58fba3539c738a356e_648_0.png)

图 10-20 显示了下一个示例产生的断言。当程序触发断言时，对话框中呈现的调用堆栈会显示代码中的行号以及此时正在执行的函数名称。这里有四个正在执行的函数，包括 main()。

断言后你有三种处理方式。单击 Abort 按钮会立即结束程序；单击 Ignore 按钮允许程序继续；单击 Retry 按钮可选择以调试模式执行程序。

你有三种重载的 Assert() 函数可用：

| Function | Description |
|---|---|
| Debug::Assert(bool condition) | 当 condition 为 false 时，对话框会显示该点的调用堆栈。 |
| Debug::Assert(bool condition, String^ message) | 同上，但会在调用堆栈信息上方在对话框中显示 message。 |
| Debug::Assert(bool condition, String^ message, String^ details) | 与前一版本相同，但会在对话框中额外显示 details。 |

亲眼看到其运行是理解的最佳帮助，因此请制作一个示例来演示调试和跟踪代码的实际运行情况。

## 试用 Debug 和 Trace

此示例只是对我所描述的一些跟踪和调试函数的练习。创建一个 CLR 控制台项目并将其修改为如下所示：

```cpp
// Ex10_03.cpp : main project file.
// CLR trace and debug output

#include "stdafx.h"

using namespace System;
using namespace System::Diagnostics;

public ref class TraceTest
{
public:
    TraceTest(int n):value(n){}

    property TraceLevel Level
    {
        void set(TraceLevel level) {sw->Level = level; }
        TraceLevel get(){return sw->Level; }
    }

    void FunA()
    {
        ++value;
        Trace::Indent();
        Trace::WriteLine(L"Starting FunA");
        if(sw->TraceInfo)
            Debug::WriteLine(L"FunA working...");
        FunB();
        Trace::WriteLine(L"Ending FunA");
        Trace::Unindent();
    }
}

void FunB()
{
    Trace::Indent();
    Trace::WriteLine(L"Starting FunB");
    if(sw->TraceWarning)
        Debug::WriteLine(L"FunB warning...");
    FunC();
    Trace::WriteLine(L"Ending FunB");
    Trace::Unindent();
}

void FunC()
{
    Trace::Indent();
    Trace::WriteLine(L"Starting FunC");
    if(sw->TraceError)
        Debug::WriteLine(L"FunC error...");
    Debug::Assert(value < 4);
    Trace::WriteLine(L"Ending FunC");
    Trace::Unindent();
}
private:
    int value;
    static TraceSwitch^ sw =
        gcnew TraceSwitch(L"Trace Switch", L"Controls trace output");
};

int main(array<System::String ^> ^args)
{
    // Direct output to the command line
    TextWriterTraceListener^ listener = gcnew TextWriterTraceListener(Console::Out);
    Debug::Listeners->Add(listener);

    Debug::IndentSize = 2;                 // Set the indent size

    array<TraceLevel>^ levels = { TraceLevel::Off,
                                  TraceLevel::Error,
                                  TraceLevel::Warning, TraceLevel::Verbose };
    TraceTest^ obj = gcnew TraceTest(0);

    Console::WriteLine(L"Starting trace and debug test...");
    for each(TraceLevel level in levels)
    {
        obj->Level = level;                 // Set level for messages
        Console::WriteLine(L"\nTrace level is {0}", obj->Level);
        obj->FunA();
    }
    return 0;
}
```

此示例在执行期间会导致显示断言对话框。然后你可以选择继续、终止执行或通过在对话框中选择相应的按钮以调试模式重试程序。

根据你在程序断言时所做的操作，此示例会产生以下输出：

```
Starting trace and debug test...

Trace level is Off
    Starting FunA
        Starting FunB
            Starting FunC
            Ending FunC
        Ending FunB
    Ending FunA

Trace level is Error
    Starting FunA
        Starting FunB
            Starting FunC
            FunC error...
            Ending FunC
        Ending FunB
    Ending FunA

Trace level is Warning
    Starting FunA
        Starting FunB
        FunB warning...
            Starting FunC
            FunC error...
            Ending FunC
        Ending FunB
    Ending FunA

Trace level is Verbose
    Starting FunA
    FunA working...
        Starting FunB
        FunB warning...
            Starting FunC
            FunC error...
            Fail:
            Ending FunC
        Ending FunB
    Ending FunA
Press any key to continue . . .
```

## 工作原理

TraceTest 类定义了三个实例函数 FunA()、FunB() 和 FunC()。每个函数都包含对 Trace::Indent() 函数的调用以增加调试输出的缩进，以及 Debug::WriteLine() 函数调用以跟踪函数进入和退出时间。在退出每个函数之前立即调用 Trace::Unindent() 函数，以将缩进级别恢复为函数调用时的状态。

TraceTest 类定义了一个私有的 TraceSwitch 成员 sw，用于控制显示多少级别的调试输出。三个成员函数中的每一个也会根据类中 sw 成员设置的级别调用 Debug::WriteLine() 函数以发出调试消息。

FunA() 函数每次被调用时都会递增类的 value 成员，而 FunC() 函数如果 value 超过 3 则触发断言。

在 main() 中，你创建一个 TextWriterTraceListener 对象，将跟踪和调试输出定向到命令行：

```cpp
TextWriterTraceListener^ listener = gcnew TextWriterTraceListener( Console::Out);
```

然后你将侦听器对象添加到 Debug 类的侦听器集合中：

```cpp
Debug::Listeners->Add(listener);
```

这会导致调试和跟踪输出被定向到 Console::Out，即标准输出流。

你创建一个 TraceLevel 对象数组，表示调试和跟踪输出的各种控制级别：

```cpp
array<TraceLevel>^ levels = { TraceLevel::Off,    TraceLevel::Error,
                           TraceLevel::Warning, TraceLevel::Verbose};
```

创建 TraceLevel 对象后，你在 for each 循环中为其设置跟踪级别：

```cpp
for each(TraceLevel level in levels)
{
    obj->Level = level;                    // Set level for messages
    Console::WriteLine(L"\nTrace level is {0}", obj->Level);
    obj->FunA();
}
```

级别是通过 obj 的 Level 属性设置的。这会在实例函数中用于控制输出的 TraceSwitch 成员 sw 中设置 Level 属性。

从输出中可以看到，你设置的缩进会影响 Debug 和 Trace 类中静态 WriteLine() 函数的输出。你也可以看到你在 TraceSwitch 类成员中设置的级别如何影响输出。当 TraceTest 类对象 obj 的 value 成员达到 4 时，FunC() 函数会触发断言。你可以重新运行示例并尝试断言对话框上三个按钮的效果。

## 总结

调试是一个很大的主题，Visual C++ 2005 提供了超出本章讨论范围的许多调试功能。如果你对本章所涵盖的内容感到满意，应该很容易通过 Visual C++ 2005 文档扩展你对调试功能的了解。搜索“debugging”应该会生成丰富的进一步信息列表。

