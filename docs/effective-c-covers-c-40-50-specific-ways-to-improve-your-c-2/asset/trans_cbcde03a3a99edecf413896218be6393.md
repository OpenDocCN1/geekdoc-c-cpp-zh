

多态地。注意任何将值类型转换为 System.Object 或接口类型的结构：将值放入集合、调用在 System.Object 中定义的方法，以及转换为 System.Object。尽可能避免这些。

## 项目 46：创建完整的应用程序特定异常类

异常是报告错误的机制，这些错误可能在远离错误发生位置的位置进行处理。关于错误原因的所有信息都必须包含在异常对象中。在此过程中，你可能希望将低级错误转换为更应用程序特定的错误，而不会丢失任何关于原始错误的信息。你需要非常谨慎地考虑在 C# 应用程序中何时创建自己的特定异常类。

第一步是了解何时以及为何创建新的异常类，以及如何构建信息丰富的异常层次结构。当使用你库的开发人员编写 catch 子句时，他们会根据异常的特定运行时类型来区分操作。每个不同的异常类可以采用一组不同的操作：

```
try
{
    Foo();
    Bar();
}
catch (MyFirstApplicationException e1)
{
    FixProblem(e1);
}
catch (AnotherApplicationException e2)
{
    ReportErrorAndContinue(e2);
}
catch (YetAnotherApplicationException e3)
{
    ReportErrorAndShutdown(e3);
}
catch (Exception e)
{
ReportGenericError(e);
throw;
}
finally
{
CleanupResources();
}
```

不同的运行时异常类型可以存在不同的 catch 子句。作为应用程序作者，当 catch 子句可能采取不同操作时，你必须创建或使用不同的异常类。请注意，上面的每个不同异常都以不同的方式处理。开发人员只希望在处理方式不同时才为不同的异常类提供不同的 catch 子句。否则，这只是额外的工作。因此，只有当你认为开发人员会为导致异常的问题采取不同操作时，才应考虑创建不同的异常类。如果你不这样做，你的用户就只能选择一些不太理想的选项。你不能在每次抛出异常时就推脱并终止应用程序。这当然工作量较少，但不会赢得用户的赞赏。或者，他们可以深入异常内部，尝试确定错误是否可以纠正：

```
private static void SampleTwo()
{
try
{
Foo();
Bar();
}
catch (Exception e)
{
switch (e.TargetSite.Name)
{
case "Foo":
FixProblem(e);
break;
case "Bar":
ReportErrorAndContinue(e);
break;
// some routine called by Foo or Bar:
default:
ReportErrorAndShutdown(e);
        throw;
    }
    finally
    {
        CleanupResources();
    }
}
```

这比使用多个 catch 子句要不吸引人得多。这是非常脆弱的代码：如果你更改例程的名称，它就会出错。如果你将生成错误的调用移动到共享实用函数中，它就会出错。异常在调用栈中越深，这种结构就越脆弱。

在深入探讨这个话题之前，让我补充两点免责声明。首先，异常并非适用于你遇到的每种错误情况。没有严格的准则，但我倾向于对那些如果不立即处理或报告就会导致持久性问题的错误情况抛出异常。例如，数据库中的数据完整性错误应该生成异常。如果被忽略，问题只会变得更严重。无法正确写入用户的窗口位置偏好设置不太可能产生深远的后果。返回一个指示失败的返回码就足够了。

其次，编写 throw 语句并不意味着是时候创建新的异常类了。我关于创建异常类的建议源于正常的人性：人们似乎在抛出异常时总是倾向于过度使用 System.Exception。这为调用代码提供了最少的有用信息。相反，应仔细考虑并创建必要的异常类，以使调用代码能够理解原因并提供最佳的恢复机会。

我再说一遍：不同异常类的原因——事实上，唯一的原因——是为了让你的用户在编写 catch 处理程序时更容易采取不同的操作。寻找那些可能成为某种恢复操作候选项的错误情况，并创建特定的异常类来处理这些操作。你的应用程序能否从丢失的文件和目录中恢复？能否从不足的安全权限中恢复？缺少网络资源呢？当你遇到可能导致不同操作和恢复机制的错误时，创建新的异常类。

现在你正在创建自己的异常类。当你创建新的异常类时，你确实有非常具体的责任。你的异常类必须以“Exception”结尾。你应该始终从 System.Exception 类或其他适当的异常类派生你的异常类。你很少会向这个基类添加功能。不同异常类的目的是在 catch 子句中具有区分错误原因的能力。

但也不要从你创建的异常类中移除任何内容。

Exception 类包含四个构造函数：

```
// Default constructor
public Exception();
```

```
// Create with a message.
public Exception(string);
```

```
// Create with a message and an inner exception.
public Exception(string, Exception);
```

```
// Create from an input stream.
protected Exception(
SerializationInfo, StreamingContext);
```

当你创建新的异常类时，请创建所有这四个构造函数。请注意，最后一个构造函数意味着你的异常类必须是可序列化的。不同的情况需要不同的构造异常的方法。（如果你选择从其他异常类派生，你应该包含该特定基类的所有适当构造函数。）你将工作委托给基类实现：

```
[Serializable]

public class MyAssemblyException :
Exception
{
public MyAssemblyException() :
base()
{
}

public MyAssemblyException(string s) :
base(s)
{
}
```

```
public MyAssemblyException(string s, Exception e) :
base(s, e)
{
}
```

```
protected MyAssemblyException(
SerializationInfo info, StreamingContext cxt) :
base(info, cxt)
{
}
```

接受异常参数的构造函数值得进一步讨论。有时，你使用的某个库会生成异常。当你只是传递所使用实用程序的异常时，调用你库的代码将获得关于可能纠正操作的最少信息：

```
public double DoSomeWork()
{
// This might throw an exception defined
// in the third party library:
return ThirdPartyLibrary.ImportantRoutine();
}
```

生成异常时，你应该提供你自己库的信息。抛出你自己的特定异常，并将原始异常作为其 InnerException 属性包含在内。你可以提供尽可能多的额外信息：

```
public double DoSomeWork()
{
try {
// This might throw an exception defined
// in the third party library:
return ThirdPartyLibrary.ImportantRoutine();
} catch(ThirdPartyException e)
{
string msg =
string.Format("Problem with {0} using library",
ToString());
throw new DoingSomeWorkException(msg, e);
}
}
```

这个新版本在问题生成的位置创建了更多信息。只要你创建了适当的 ToString() 方法（参见项目 5），你就创建了一个描述生成问题的对象的完整状态的异常。不仅如此，内部异常还显示了问题的根本原因：你使用的第三方库中的某个东西。

这种技术称为异常转换，即将低级异常转换为提供更多错误上下文的更高级异常。当发生错误时，你生成的信息越多，用户就越容易诊断并可能纠正错误。通过创建自己的异常类型，你可以将低级通用问题转换为包含所有应用程序特定信息的特定异常，这些信息足以完全诊断并可能纠正问题。

你的应用程序会抛出异常——希望不经常，但会发生。如果你不做任何特定的操作，当你在核心框架上调用的方法出错时，你的应用程序将生成默认的 .NET Framework 异常。提供更详细的信息将大大有助于你和你的用户在现场诊断并可能纠正错误。当可能采取不同的纠正操作时，才创建不同的异常类，并且只有在可能采取不同操作时才创建。通过提供基础异常类支持的所有构造函数，创建功能齐全的异常类。你使用 InnerException 属性来携带由较低级别错误条件生成的所有错误信息。

## 项目 47：优先使用强异常保证

当你抛出异常时，你向应用程序中引入了一个破坏性事件。控制流已被破坏。预期的操作没有发生。更糟的是，你将清理操作留给了最终编写捕获异常代码的程序员。捕获异常时可用的操作与你在抛出异常时管理程序状态的程度直接相关。幸运的是，C#

