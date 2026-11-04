
## 第 I 部分：C# 基础

首先，通过向 Timer 类传递一个值来实例化该类。该值是 Timer 类触发（引发）其 Elapsed 事件之间的时间间隔（以毫秒为单位）。接着，将 Elapsed 事件与事件处理程序 t_Elapsed 关联，该处理程序在控制台窗口中显示当前时间。Timer 类的 Start() 方法会激活 Timer 对象，使其可以开始触发 Elapsed 事件。由于该事件每秒触发一次，控制台实际上每秒更新一次时间（见图 7-8）。

![](img/a977a875c7c627b45d939729705a252e_253_0.png)

图 7-8

.NET Framework 类库中另一个有用的类是 FileSystemWatcher 类（位于 System.IO 命名空间中）。它监视文件系统的更改，并通过引发事件使你能够监视这些更改。例如，可以使用 FileSystemWatcher 类监视硬盘驱动器上的更改，例如文件/目录被删除、被创建或其内容发生更改时。

要了解 FileSystemWatcher 类如何工作，请考虑以下程序：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Runtime.Remoting.Messaging;
using System.IO;

namespace Events
{
    class Program
    {
        static void Main(string[] args)
        {
            FileSystemWatcher fileWatcher = new FileSystemWatcher()
            {
                Path = @"c:\",
                Filter = "*.txt"
            };

            //--wire up the event handlers--
            fileWatcher.Deleted += new FileSystemEventHandler(fileWatcher_Deleted);
            fileWatcher.Renamed += new RenamedEventHandler(fileWatcher_Renamed);
            fileWatcher.Changed += new FileSystemEventHandler(fileWatcher_Changed);
            fileWatcher.Created += new FileSystemEventHandler(fileWatcher_Created);

            //--begin watching--
            fileWatcher.EnableRaisingEvents = true;
            Console.ReadLine();
        }

        static void fileWatcher_Created(object sender, FileSystemEventArgs e)
{
    Console.WriteLine("File created: " + e.FullPath);
}

static void fileWatcher_Changed(object sender, FileSystemEventArgs e)
{
    Console.WriteLine("File changed: " + e.FullPath);
}

static void fileWatcher_Renamed(object sender, RenamedEventArgs e)
{
    Console.WriteLine("File renamed: " + e.FullPath);
}

static void fileWatcher_Deleted(object sender, FileSystemEventArgs e)
{
    Console.WriteLine("File deleted: " + e.FullPath);
}
}
```

首先，通过初始化 FileSystemWatcher 类的 Path 和 Filter 属性来创建该类的实例：

```
FileSystemWatcher fileWatcher = new FileSystemWatcher()
{
    Path = @"C:\",
    Filter = "*.txt"
};
```

这里，你正在监视 C:\ 驱动器及其所有以 .txt 扩展名结尾的文件。

然后，将所有事件与其各自的事件处理程序关联：

```
//---wire up the event handlers---
fileWatcher.Deleted += new FileSystemEventHandler(fileWatcher_Deleted);
fileWatcher.Renamed += new RenamedEventHandler(fileWatcher_Renamed);
fileWatcher.Changed += new FileSystemEventHandler(fileWatcher_Changed);
fileWatcher.Created += new FileSystemEventHandler(fileWatcher_Created);
```

这些语句处理四个事件：

- Deleted — 当文件被删除时触发
- Renamed — 当文件被重命名时触发
- Changed — 当文件内容发生更改时触发
- Created — 当文件被创建时触发

## 第 I 部分：C# 基础

最后，为这四个事件定义事件处理程序：

```
static void fileWatcher_Created(object sender, FileSystemEventArgs e)
{
    Console.WriteLine("File created: " + e.FullPath);
}

static void fileWatcher_Changed(object sender, FileSystemEventArgs e)
{
    Console.WriteLine("File changed: " + e.FullPath);
}

static void fileWatcher_Renamed(object sender, RenamedEventArgs e)
{
    Console.WriteLine("File renamed: " + e.FullPath);
}

static void fileWatcher_Deleted(object sender, FileSystemEventArgs e)
{
    Console.WriteLine("File deleted: " + e.FullPath);
}
```

要测试该程序，可以在 C:\ 驱动器中新建一个文本文件，对其内容做一些更改，重命名它，然后删除它。输出窗口将如图 7-9 所示。

![](img/a977a875c7c627b45d939729705a252e_255_0.png)

图 7-9

## 实现事件

到目前为止，你一直通过编写事件处理程序来订阅事件。现在，你将在自己的类中实现事件。对于此示例，创建一个名为 AlarmClock 的类。AlarmClock 允许你设置特定的日期和时间，以便在时间到时（通过事件）收到通知。为此，你使用 Timer 类。

首先，按如下方式定义 AlarmClock 类：

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Timers;

class AlarmClock
{
}
```

声明一个 Timer 变量，并定义 AlarmTime 属性，以允许该类的用户设置日期和时间：

```
class AlarmClock
{
    Timer t;
    public DateTime AlarmTime { get; set; }
}
```

接下来，定义 Start() 方法，以便用户可以通过启动 Timer 对象来开始监视：

```
class AlarmClock
{
    //...
    public void Start()
    {
        t.Start();
    }
}
```

接下来，在 AlarmClock 类中定义一个公共事件成员：

```
public event EventHandler TimesUp;
```

EventHandler 是一个预定义委托，该语句将 TimesUp 定义为你的类的事件。

在 AlarmClock 类中定义一个受保护的虚方法，该类将在内部使用它来引发 TimesUp 事件：

```
protected virtual void onTimesUp(EventArgs e)
{
    if (TimesUp != null)
        TimesUp(this, e);
}
```

EventArgs 类是包含事件数据的类的基类。该类不会将任何数据传回事件处理程序。

*下一节将说明如何创建另一个从该 EventArgs 基类派生的类，以便将信息传回事件处理程序。*

定义 AlarmClock 类的构造函数，使 Timer 对象 (t) 每 100 毫秒触发其 Elapsed 事件。此外，将 Elapsed 事件与事件处理程序关联。该事件
## 第 I 部分：C# 基础
处理程序将检查当前时间与该类用户设置的时间。如果时间等于或超过用户设置的时间，事件处理程序将调用你在上一步中定义的 onTimesUp() 方法：

```csharp
public AlarmClock()
{
    t = new Timer(100);
    t.Elapsed += new ElapsedEventHandler(t_Elapsed);
}

void t_Elapsed(object sender, ElapsedEventArgs e)
{
    if (DateTime.Now >= this.AlarmTime)
    {
        onTimesUp(new EventArgs());
        t.Stop();
    }
}
```

就是这样！完整的 AlarmClock 类如下：

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

using System.Timers;

class AlarmClock
{
    Timer t;
    public DateTime AlarmTime { get; set; }

    public void Start()
    {
        t.Start();
    }

    public AlarmClock()
    {
        t = new Timer(100);
        t.Elapsed += new ElapsedEventHandler(t_Elapsed);
    }

    void t_Elapsed(object sender, ElapsedEventArgs e)
    {
        if (DateTime.Now >= this.AlarmTime)
        {
            onTimesUp(new EventArgs());
```
```
t.Stop();
}

public event EventHandler TimesUp;
protected virtual void onTimesUp(EventArgs e)
{
    if (TimesUp != null)
        TimesUp(this, e);
}
```

要使用 AlarmClock 类，首先创建 AlarmClock 类的实例，然后使用 AlarmTime 属性设置闹钟时间。接着，将 TimesUp 事件与事件处理程序关联，以便在设定时间到时打印一条消息：

```
class Program
{
    static void Main(string[] args)
    {
        AlarmClock c = new AlarmClock()
        {
            //---alarm to sound off at 16 May 08, 9.50am---
            AlarmTime = new DateTime(2008, 5, 16, 09, 50, 0, 0),
        };
        c.Start();
        c.TimesUp += new EventHandler(c_TimesUp);

        Console.ReadLine();
    }

    static void c_TimesUp(object sender, EventArgs e)
    {
        Console.WriteLine("Times up!");
    }
}
```

## 事件与委托的区别

事件是使用委托实现的，那么事件与委托之间有什么区别？区别在于，对于事件，不能使用 = 运算符直接为其分配委托；必须使用 += 运算符。
