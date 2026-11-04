
```xml
<endpoint address="registration"
  binding="customBinding"
  bindingConfiguration="poxBinding"
  contract="SHARPService.IRegistration" />
</service>
<behaviors>
  <serviceBehaviors>
    <behavior>
      <!-- To avoid disclosing metadata information, set the value below to
      false and remove the metadata endpoint above before deployment -->
      <serviceMetadata httpGetEnabled="true" />
      <!-- To receive exception details in faults for debugging purposes, set
      the value below to true.  Set to false before deployment to avoid disclosing
      exception information -->
      <serviceDebug includeExceptionDetailInFaults="false" />
    </behavior>
  </serviceBehaviors>
</behaviors>
<system.serviceModel>
  <serviceHostingEnvironment>
    <modules runAllManagedModulesForAllRequests="true" />
  </serviceHostingEnvironment>
</system.serviceModel>
<connectionStrings>
  <add name="ConferenceDBEntities" connectionString="metadata=res://*/Sharp.cdl|res://*/Sharp.ssdl|res://*/Sharp.msl;provider=System.Data.SqlClient;provider connection string=&quot;Data Source=.\SQLEXPRESS;AttachDbFilename='C:\Program Files\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA\ConferenceDB.mdf';Integrated Security=True;Connect Timeout=30;User Instance=True;MultipleActiveResultSets=True&quot;" providerName="System.Data.EntityClient" />
</connectionStrings>
</configuration>
```

第七卷
第4章
使用 REST 构建 Web 服务

## 第八卷
## C# 4.0 的新特性
## 第五波
里奇·坦南特 作

> 有了面向对象编程，我理解了“封装”和“继承”的部分。但正是那个该死的“杂乱多态”难住了我。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_792_0.png)

## 内容一览
- 第1章：动态编程！................................ 769
- 第2章：使用命名参数和可选参数提高生产力 ................................ 781
- 第3章：在 Interop 方面提供帮助 ................................ 789
- 第4章：修订泛型 ................................ 795

COM 期望使用它的语言（如 VB Classic 和 C++）具有动态类型。这让 C# 程序员难以针对 Microsoft Office 进行开发，而这恰恰与微软的期望相反。最终结果是什么？动态类型。

## C# 转向动态类型
所谓的“动态语言”是一种不断卷土重来的趋势，就像褶皱燕尾服衬衫一样。动态语言是允许松散类型而非静态类型的语言。这一概念始于 20 世纪 60 年代的 LISP。动态语言在 20 世纪 80 年代末卷土重来，原因有二：网络管理脚本和人工智能热潮。感谢 Web，这个流行语又一次回来了。

对于各位还年轻、不记得那些事的人来说，万维网（World Wide Web）是建立在“查看源代码”和动态语言之上的。微软最初的 Web 开发语言 Active Server Pages 就是建立在 VBScript 之上——一种动态语言。

有了动态编程环境，Web 会变得更好，所以这次趋势可能会持续下去（至少在下一个重大事物出现之前）。C# 并不是唯一在增添动态语言特性的语言，动态类型也不是为了吸引 Web 程序员而添加的唯一语言特性。

一些动态语言已经存在了一段时间，例如：
- Perl
- Visual Basic
- Smalltalk
- LISP
- Scheme

虽然其中一些已不像从前那么流行，但它们仍然存在，并推动了新语言中的这一趋势。在过去十年中涌现出的所有新的或翻新的动态语言中，你都可以看到这一趋势。其中许多源于 Web，而另一些则是新近用于 Web 的：
- PHP
- Ruby
- JavaScript
- Cold Fusion
- Python
- Cobra（我的新宠）
- Groovy
- Boo
- Newspeak

使用动态语言的程序员——我该怎么说委婉一点——对自己的工具选择有强烈的感情。相关社区非常强大。使用动态语言的开发者几乎会在所有事情上使用它们，除了高度结构化的团队构建类环境，比如：
- 为系统维护编写脚本基础设施
- 构建测试
- 一次性实用工具
- 服务器场维护
- 编写其他应用程序的脚本
- 构建网站
- 文件维护

动态语言之所以在这些任务中流行，有两个原因。首先，它们提供即时反馈，因为你可以在正在编写的程序其余部分的约束之外尝试一段代码。其次，你无需先构建底层管道就可以开始构建更高级别的代码块。

例如，Ruby 有一个命令行界面，你可以简单地将一个函数粘贴进去，甚至脱离上下文，然后看看它如何运行。甚至还有一个 Web 版本，网址是 http://tryruby.hobix.com/。你可以直接在那里输入代码，即使引用了未定义的类也没关系，因为 Ruby 会自行猜测。

这自然引出了下一点：动态语言使你能构建一个引用其他地方未定义类型的类。例如，你可以创建一个类来调度事件，而不必真正先构建底层的 Event 类型。

所有这些都使语言更加适应变化。你可以只在一处进行逻辑更改，而不必翻遍大量代码去修复所有地方的类型声明。再结合可选参数和命名参数（参见第2章），你在更改程序时需要输入的内容就少多了。

随着你更多地使用动态语言，其他好处也会显现出来。例如，宏语言通常是动态类型的。如果你曾尝试在旧版 Visual Studio 中构建宏，你就会知道使用静态语言有多痛苦。

让 C#（就此而言，也包括 VB.NET）变得更动态，不仅使其成为扩展 Visual Studio 的更好语言，还让程序员能够在他们编写的程序中嵌入这种语言，从而使其他开发者能够进一步扩展这些应用程序。

## 动态编程
到现在，你一定会问：“我们到底在谈什么？”问得好。当你定义一个新变量时，可以使用 dynamic 关键字，而 C# 会让你对变量的成员做一些假设。

大体上，我要说的就是这样。如果你想声明一个新的 Course 对象，可以这样做：

```
Course newCourse = new Course();
newCourse.Schedule();
```

当然，这假设你在程序的其他地方定义了一个 Course 类，如下所示：

```
class Course {
    public void Schedule()
    {
        //Something fancy here
    }
}
```

但如果你不知道新对象会是哪个类，该怎么办？你会怎么处理？你可以将它声明为 Object，因为一切皆派生自 Object，对吗？代码如下：

```
Object newCourse = new Object();
```

别急，朋友，如果你的下一行是这样：

```
newCourse.Schedule();
```

注意，几乎立刻会出现波浪线，并且在设计时的“错误列表”中会看到著名的“object does not contain a definition for Schedule...”错误。

然而，我们可以这样做：

```
dynamic newCourse = SomeFunction();
newCourse.Schedule();
```

这段代码只需要有一个返回某个值的函数存根，我们就能顺利运行。如果 SomeFunction() 返回一个字符串呢？嗯，我们会得到一个运行时错误。但它仍然能编译！

现在，如果你和我一样，你一定会想：“这是好事吗？怎么会？！”我理解你，相信我。目前，你可以把这归咎于 COM。

你看，COM 主要是用 C++ 构建的，而 C++ 有一种 variant 类型。在 C++ 中，你可以像这样声明一个变量为动态类型：

```
VARIANT newCourse;
```

它的工作方式与动态类型一样，只不过当时 C# 还没有发明出来。总之，因为 COM 中的许多对象使用 Variant 输出参数，所以使用 .NET 处理互操作（Interop）非常困难。

因为 Microsoft Office 主要由 COM 对象构成，而且它短期内不会改变，再加上微软希望我们有一天都能成为 Office 开发者——砰！于是我们就有了动态类型。

例如，假设我们的 newCourse 是某个 COM 类中方法的一个 variant 输出参数。为了获取该值，我们不得不将其声明为 Object，如下所示：

```
CourseMarshaller cm = new CourseMarshaller(); //a COM object
int courseId = 4;
Object newCourse;
cm.MakeCourse(courseId, newCourse);
//and now we are back to square one
newCourse.Schedule(); //This causes a 'member not found exception'
```

即使 Schedule 方法存在，第六行也无法编译，因为我们不能假定 newCourse 总是以 Course 对象的形式返回，因为它被声明为 variant。我们被卡住了。

不过，有了动态类型，这段代码让我们再次如鱼得水：

```
CourseMarshaller cm = new CourseMarshaller(); //a COM object
int courseId = 4;
dynamic newCourse;
cm.MakeCourse(courseId, newCourse);
newCourse.Schedule(); //This now compiles
```

