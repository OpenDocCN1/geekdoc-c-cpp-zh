

# 示例：

```
using System;
using System.Threading;

namespace multithreadingapplication {

class mainthreadprogram {

static void Main(string[] args) {

Thread th = Thread.currentthread;

th.Name = "mainthread";

Console.writeline("This is {0}", th.Name);

Console.readkey();

}

}

}
```

当上面的代码被编译并执行时，会产生以下结果 –

This is mainthread

```
}
}
}
```

当上面的代码被编译并执行时，会产生以下结果 –

In Main: Creating the Child thread

# Child thread starts

控制台是通过用户使用交互式命令集与系统进行通信的一组设备。在这方面，GUI 不被视为控制台。大多数计算机系统中的主要输入设备是键盘，主要输出是显示器。这对在大多数情况下构成了用户的控制台

内容

The Console Class

Managing Console I/O Operations

Console.openstandardinput Method()

Console.openstandardoutput Method()

Console.Read Method()

Console.readline Method()

Console.Write Method(Boolean)

Console.Write Method(String)

## The Console Class

为了允许控制台输入/输出操作，C# 提供了，C# 提供了一个控制台类。Console 类为从控制台读取和写入字符的应用程序提供基本的输入和输出支持。标准输入、输出和错误流由属性表示，并在应用程序启动时自动与控制台关联。应用程序可以将这些属性重定向到其他流；例如，与文件而不是控制台关联的流。默认情况下，控制台类中的读取方法使用标准输入流（键盘），而写入方法使用标准输出（显示器）流。

写入方法支持在不自动附加回车和换行字符的情况下写入数据。这使得无需先将它们转换为字符串即可写入字符串、格式化字符串、字符数组、原始类型实例和任意对象。

以下示例：演示了基本 Console 输入和输出函数的使用。

```
/* Console Input/Ouput */
```

Using System;

```
Class consoletest
{
    Public static void Main()
    {
        Console.Write("Hello");
        Console.writeline("World");
        Console.Write("What is Your Name");
        String name = Console.readline();
        Console.Write("Hello, ");
        Console.Write(name);
        Console.writeline(" !");
    }
}
```

## 3.5 Managing Console I/O Operations

控制台输入/输出操作由 Console 类执行，该类位于 system 命名空间内并存储在 Mscorlib（在 Mscorlib.dll）程序集中。

数据从控制台读取自标准输入流；正常数据写入控制台写入标准输出流；错误数据写入控制台写入标准错误输出流。这些流在应用程序启动时自动与控制台关联，并以 In、Out 和 Error 属性的形式呈现给您。

默认情况下，In 属性的值为 System.IO.textreader，而 Out 和 Error 属性的值为 System.IO.textwriter 对象。但是，您可以将这些属性与不代表控制台的流关联。此类同步 textreader 和 textwriter 实例。多个线程可以并发地从此类型的实例读取或写入。

## Console.openstandardinput Method()

此方法获取标准输入流。下面给出的代码显示了这一点。此方法可用于在 setin 方法更改后重新获取标准输入流。考虑以下代码片段以作说明。

以下代码示例说明了 openstandardinput 的用户：

```
Public class Decoder
```

```
{
```

```
Public static void Main()
{
    Stream inputstream = Console.openstandardinput();
    Byte [] bytes = new byte[100];
    Console.writeline("To decode, type or paste the UTF7 encoded string and press enter:");
    Console.writeline("(Example::  \"M+apw-nchen  ist wundervoll\")");
    Int outputlength = inputstream.Read(bytes, 0 ,100);
    Char [] chars = Encoding.UTF7.getchars(bytes, 0 , outputlenght);
    Console.writeline("Decoded String:");
    Console.writeline(new string(chars));
}
}
```

## Console.openstandardoutput Method()

该方法获取标准输出流。此方法可用于在 setout 方法更改后重新获取标准输出流。考虑以下代码片段以作说明。

```
Public class inserttabs
```

```
```csharp
Standardoutput.autoflush = true;
Console.setout(standardoutput);
Console.writeline("INSERTTABS has completed the processing of (0).", args[0]);
Return 0;
}
}
```
```

## Console.Read Method()

此方法从标准输入流读取下一个字符。它返回来自输入流的下一个字符，如果没有更多字符可用，则返回负一 (-1)。此方法不会在读取操作终止之前返回；例如：用户按下回车键。如果有数据可用，输入流包含用户输入的内容，后缀为环境相关的换行符。考虑以下说明。

```
```csharp
Int i;
Char c;
While(true)
{
I = Console.Read();
```

```
If (i == 1)

Break;

C = (char) l;

Console.writeline("Echo: )0").c);

}

Console.writeline("Done");

Return 0;
```

## Console.readline Method()

此方法从标准输入流读取下一行字符。它返回来自输入流的下一行，如果没有更多字符可用，则返回空引用。行定义为由回车（十六进制 0x000d）、换行（十六进制 0x000a）跟随的字符序列。返回的字符串不包含终止字符。考虑以下代码以作说明。

```
Public class inserttabs

{

    Private const int tabsize = 4;

    Private const string usagetext = "Usage: INSERTTABS inputfile.txt outputfile.txt";
```

```
Public static int Main(String[] args)
{
	Streamwriter writer = null;
	If (args.Length < 2)
	{
		Console.writeline(usagetext);
		Return 1;
	}
	Try
	{
		Write = new strmwriter(args[1]);
		Console.setout(writer);
		Console.setin(new streamreader(args[0]));
	}
	Catch(ioexception e)
	{
		Textwriter errorwriter = Console.Error;
		Errorwriter.writeline(e.Message);
	}
}
```

```
Errorwriter.writeline(usagetext);

Return 1;
}

String line;

While((line = Console.readline())!= null)
{

String newline = line.Replace(("").padright(tabsize,' '),"\t");

Console.writeline(newline);
}

Writer.Close();

//Recover the standard output stream so that a
// Completion message can be displayed.

Streamwriter standardoutput = new streamwriter(Console.openstandardoutput());

Standardoutput.autoflush = true;

Console.setout(standardoutput);

Console.writeline("INSERTTABS has completed the processing of (0).", args[0]);
```

```
Return 0;
}
}
```

## Console.Write Method(Boolean)

此方法将指定布尔值的文本表示形式写入标准输出流。值的文本表示形式是通过调用 Boolean.ToString 产生的。Consdier 以下代码以作说明。

```
Public class formatconverter
{
Public static void Main(string[] args)
{
String lineinput;
While((lineinput = Console.readline()) != null)
{
Bool isfirstfield = true;
Foreach(string item in fields)
{
If (isfirstfield)
```

```
Isfirstfield = false;

Else

Console.Write('');

Try

{
    Console.Write(Convert.tobyte(Convert.toboolean(item)))
    ;
}

Catch(formatexception)

{
    Console.Write(item);
}

}

Console.writeline();
}

}

}
```

## Console.Write Method(String)

