
## 第78章：将字符串转换为其他类型时处理 FormatException

### 第78.1节：将字符串转换为整数

有多种方法可用于将字符串显式转换为整数，例如：

- 1. Convert.ToInt16();
- 2. Convert.ToInt32();
- 3. Convert.ToInt64();
- 4. int.Parse();

但是，如果输入字符串包含非数字字符，所有这些方法都会抛出 FormatException。为此，我们需要编写额外的异常处理（try..catch），以便在这种情况下处理它们。

### 示例说明：

因此，假设我们的输入为：

```csharp
string inputString = "10.2";
```

### 示例 1：Convert.ToInt32()

```csharp
int convertedInt = Convert.ToInt32(inputString); // Failed to Convert
// Throws an Exception "Input string was not in a correct format."
```

注意：其他提到的方法也同样如此，即 Convert.ToInt16(); 和 Convert.ToInt64();

### 示例 2：int.Parse()

```csharp
int convertedInt = int.Parse(inputString); // Same result "Input string was not in a correct format."
```

### 我们如何规避这个问题？

如前所述，为了处理异常，我们通常需要如下所示的 try..catch：

```csharp
try
{
    string inputString = "10.2";
    int convertedInt = int.Parse(inputString);
}
catch (Exception Ex)
{
    //Display some message, that the conversion has failed.
}
```

但是，在所有地方都使用 try..catch 并不是一个好做法，而且可能存在这样的场景：如果输入错误，我们希望给出 0（如果遵循上述方法，就需要从 catch 块中为 convertedInt 赋值为 0）。为了处理这类场景，我们可以使用一个特殊方法 .TryParse()。

TryParse() 方法具有内部异常处理，它会将输出提供给 out 参数，并返回一个布尔值来指示转换状态（如果转换成功则为 true；如果失败则为 false）。根据返回值，我们可以确定转换状态。让我们看一个示例：

### 用法 1：将返回值存储在布尔变量中

```csharp
int convertedInt; // Be the required integer
bool isSuccessConversion = int.TryParse(inputString, out convertedInt);
```

执行后，我们可以检查变量 isSuccessConversion 来确认转换状态。如果它为 false，那么 convertedInt 的值将为 0（如果你希望在转换失败时得到 0，则无需检查返回值）。

### 用法 2：使用 if 检查返回值

```csharp
if (int.TryParse(inputString, out convertedInt))
{
    // convertedInt will have the converted value
    // Proceed with that
}
else
{
    // Display an error message
}
```

### 用法 3：如果不关心返回值，可以不检查返回值，直接使用以下代码

（无论是否转换成功，0 都可以接受）

```csharp
int.TryParse(inputString, out convertedInt);
// use the value of convertedInt
// But it will be 0 if not converted
```

## 第79章：阅读并理解堆栈跟踪

调试程序时，堆栈跟踪是一个极大的帮助。当程序抛出异常时，你会得到堆栈跟踪；有时程序异常终止时也会得到堆栈跟踪。

### 第79.1节：Windows Forms 中一个简单 NullReferenceException 的堆栈跟踪

让我们创建一小段会抛出异常的代码：

```csharp
private void button1_Click(object sender, EventArgs e)
{
    string msg = null;
    msg.ToCharArray();
}
```

如果执行这段代码，我们会得到以下异常和堆栈跟踪：

```
System.NullReferenceException: "Object reference not set to an instance of an object."
    at WindowsFormsApplication1.Form1.button1_Click(Object sender, EventArgs e) in
    F:\WindowsFormsApplication1\WindowsFormsApplication1\Form1.cs:line 29
    at System.Windows.Forms.Control.OnClick(EventArgs e)
    at System.Windows.Forms.Button.OnClick(EventArgs e)
    at System.Windows.Forms.Button.OnMouseUp(MouseEventArgs mevent)
```

堆栈跟踪会继续这样下去，但对我们而言，这部分已经足够了。

在堆栈跟踪的顶部，我们看到这一行：

> 位于 WindowsFormsApplication1.Form1.button1_Click(Object sender, EventArgs e)，文件
> F:\WindowsFormsApplication1\WindowsFormsApplication1\Form1.cs:第 29 行

这是最重要的部分。它告诉我们异常发生的准确行：Form1.cs 中的第 29 行。因此，这就是你开始查找的位置。

第二行是

> 位于 System.Windows.Forms.Control.OnClick(EventArgs e)

这是调用 button1_Click 的方法。所以现在我们知道，发生错误的 button1_Click 是从 System.Windows.Forms.Control.OnClick 调用的。

由此，你可以弄清楚代码在遇到问题之前遵循了哪条执行路径！

请注意，堆栈跟踪包含来自 .Net 系统的调用；通常你不需要追踪所有 Microsoft 的 System.Windows.Forms 代码来找出问题所在，只需要追踪属于你自己应用程序的代码。

那么，为什么这被称为“堆栈跟踪”呢？

因为每当程序调用一个方法时，它都会记录自己当时所在的位置。它有一个称为“栈”的数据结构，用来保存上一次的位置。

如果方法执行完毕，它会查看栈，以确定在调用该方法之前所在的位置，并从那里继续执行。

因此，栈让计算机知道在调用新方法之前它在哪里暂停。

但它也可以作为调试的帮助。就像侦探追踪罪犯作案时采取的步骤一样，程序员可以使用栈来追踪程序崩溃之前所采取的步骤。

## 第80章：诊断

### 第80.1节：使用 TraceListeners 重定向日志输出

通过向 Debug.Listeners 集合添加 TextWriterTraceListener，可以将调试输出重定向到文本文件。

```csharp
public static void Main(string[] args)
{
    TextWriterTraceListener myWriter = new TextWriterTraceListener(@"debug.txt");
    Debug.Listeners.Add(myWriter);
    Debug.WriteLine("Hello");
    
    myWriter.Flush();
}
```

可以使用 ConsoleTraceListener 将调试输出重定向到控制台应用程序的 out 流。

```csharp
public static void Main(string[] args)
{
    ConsoleTraceListener myWriter = new ConsoleTraceListener();
    Debug.Listeners.Add(myWriter);
    Debug.WriteLine("Hello");
}
```

### 第80.2节：Debug.WriteLine

当应用程序以调试配置编译时，写入 Listeners 集合中的跟踪侦听器。

```csharp
public static void Main(string[] args)
{
    Debug.WriteLine("Hello");
}
```

在 Visual Studio 或 Xamarin Studio 中，这会显示在“应用程序输出”窗口中。这是因为 TraceListenerCollection 中存在默认的跟踪侦听器。

## 第81章：溢出

### 第81.1节：整数溢出

整数能够存储的容量是有上限的。当超过该限制时，它会回绕到负数一侧。对于 int，这个上限是 2147483647

```csharp
int x = int.MaxValue; //MaxValue is 2147483647
x = unchecked(x + 1); //make operation explicitly unchecked so that the example also works when the check for arithmetic overflow/underflow is enabled in the project settings
Console.WriteLine(x); //Will print -2147483648
Console.WriteLine(int.MinValue); //Same as Min value
```

对于超出此范围的任何整数，请使用 System.Numerics 命名空间，它包含 BigInteger 数据类型。更多信息请查看以下链接：https://msdn.microsoft.com/en-us/library/system.numerics.biginteger(v=vs.110).aspx

### 第81.2节：运算过程中的溢出

运算过程中也会发生溢出。在以下示例中，x 是 int，而 1 默认是 int。因此加法是 int 加法，结果也会是 int，并且会发生溢出。

```csharp
int x = int.MaxValue; //MaxValue is 2147483647
long y = x + 1; //It will be overflow
Console.WriteLine(y); //Will print -2147483648
Console.WriteLine(int.MinValue); //Same as Min value
```

可以通过使用 1L 来防止这种情况。现在 1 将是 long，加法也将是 long 加法

```csharp
int x = int.MaxValue; //MaxValue is 2147483647
long y = x + 1L; //It will be OK
Console.WriteLine(y); //Will print 2147483648
```

### 第81.3节：顺序很重要

以下代码会发生溢出

```csharp
int x = int.MaxValue;
Console.WriteLine(x + x + 1L); //prints -1
```

而以下代码不会溢出

```csharp
int x = int.MaxValue;
Console.WriteLine(x + 1L + x); //prints 4294967295
```

这是由于运算从左到右的顺序。在第一段代码中，x + x 会溢出，之后结果变为 long。另一方面，x + 1L 会变为 long，之后再将 x 加到该值上。
