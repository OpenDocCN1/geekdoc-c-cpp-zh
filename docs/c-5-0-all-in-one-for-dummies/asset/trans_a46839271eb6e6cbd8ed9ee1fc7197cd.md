
该示例显示了一个带有两个按钮和一个进度条的小型对话框样式窗口（参见图 9-1）。当你将解决方案示例加载到 Visual Studio 中，然后生成、运行它，并单击上方标有“单击开始”的按钮时，进度条会运行几秒钟。你会看到它逐渐填满，每次填充其长度的十分之一。当它完全填满时，你可以单击“关闭”按钮来结束程序，或再次单击“单击开始”。

## 整合应用

要自行创建示例应用，而不是仅从网站示例中加载它——并体验一点 Windows 图形编程——请按照以下步骤操作，首先在 *设计模式* 下工作，在该模式下你只是在布局应用的外观。

首先创建项目，并将必要的控件放置在你的“窗口”上：

- 1. **选择“文件”⇒“新建项目”**，在左侧 **C#** 下选择 **Windows**，但这次在右侧选择 **Windows 窗体应用程序**，而不是通常的 **控制台应用程序**；将项目命名为 **SimpleProgress**。
  
  你首先看到的是 *窗体*：一个由你使用若干控件自行布局的窗口。
- 2. **选择“视图”⇒“工具箱”**，从“工具箱”窗口的 **公共控件** 组中，将 **ProgressBar** 控件拖到窗体上并放下；然后将两个 **Button** 控件拖到窗体上。
- 3. **调整按钮和 **ProgressBar** 的位置，使它们看起来大致如图 9-1 所示。**
  
  注意有助于定位的便捷参考线。

接下来，为这些控件设置属性：选择“视图”⇒“属性”，在窗体上选择一个控件，然后设置该控件的属性：

- 1. 对于 **进度条**——在代码中名为 **progressBar1**——确保 **Minimum** 属性为 **0**，**Maximum** 属性为 **100**，**Step** 属性为 **10**，**Value** 属性为 **0**。
- 2. 对于上面的按钮，将 **Text** 属性改为 **“单击开始”**，并拖动按钮图像上的尺寸手柄，直到它看起来合适并显示全部文本。
- 3. 对于下面的按钮，将 **Text** 属性改为 **“关闭”**，并按你的喜好调整按钮大小。

在这个简单示例中，你把所有代码都放在 *窗体* 类中。（窗体就是你的窗口；它的类——这里名为 **Form1**——负责所有图形相关事务。）通常，你应该把所有“业务”代码——执行计算、数据访问和其他重要工作的代码——放在其他类中。窗体类应保留给与在窗体上显示元素以及响应其控件密切相关的代码。我在这里打破了那条规则——但无论委托的回调方法位于何处，委托都能正常工作。

![](img/80ff26f06fc9ab951e1cd4257b867366_384_0.png)

现在，仍在设计模式下，为每个按钮添加一个 *处理程序* 方法：

- 1. **在窗体上，双击新的“关闭”按钮。**
  
  此操作会在“窗体后台代码”（或简称为“代码隐藏”）中生成一个方法——即让窗体工作的代码。它看起来如下——你添加加粗的代码：
  
  ```csharp
  private void button2_Click(object sender, EventArgs e)
  {
      this.Close();  // 'this' refers to the Form1 class.
  }
  ```
  
  要在窗体的代码和其图像之间切换，只需更改主面板中的选项卡。
  
  ![](img/80ff26f06fc9ab951e1cd4257b867366_385_0.png)
  
- 2. **双击新的“单击开始”按钮以生成其处理程序方法，该方法在代码隐藏中如下所示：**
  
  ```csharp
  private void button1_Click(object sender, EventArgs e)
  {
      UpdateProgressCallback callback =
          new UpdateProgressCallback(this.DoUpdate);
      // Do something that needs periodic progress reports.
      // This passes a delegate instance that knows how to update the bar.
      DoSomethingLengthy(callback);
      // Clear the bar so that it can be used again.
      progressBar1.Value = 0;
  }
  ```
  
- 3. **将以下回调方法添加到窗体类中：**
  
  ```csharp
  private void DoUpdate()
  {
      progressBar1.PerformStep(); // Tells progress bar to update itself
  }
  ```

在下一节中，我将带你了解剩余的代码，这些代码全都在窗体类中。在本章后面，我会向你展示所传递委托的其他变体。

## 查看代码

塞进 Form1 类的剩余代码片段由本章前面介绍过的委托生命周期各部分构成。我先向你展示这个类，然后向你展示这些部分分别在哪里。加粗的行是你在此前小节添加的项之外新增的代码：

![](img/80ff26f06fc9ab951e1cd4257b867366_386_0.png)

```csharp
using System;
using System.Windows.Forms;
namespace SimpleProgress
{
    public partial class Form1 : Form
    {
        // Declare the delegate. This one is void.
        delegate void UpdateProgressCallback();

        public Form1()
        {
            InitializeComponent();
        }
        // DoSomethingLengthy -- My workhorse method takes a delegate.
        private void DoSomethingLengthy(UpdateProgressCallback updateProgress)
        {
            int duration = 2000;
            int updateInterval = duration / 10;
            for (int i = 0; i < duration; i++)
            {
                Console.WriteLine("Something or other");
                // Update every tenth of the duration.
                if ((i % updateInterval) == 0 && updateProgress != null)
                {
                    updateProgress(); // Invoke the delegate.
                }
                if ( updateProgress != null ) updateProgress();
            }
        }
        // DoUpdate -- The callback method
        private void DoUpdate()
        {
            progressBar1.PerformStep();
        }
        private void button1_Click(object sender, EventArgs e)
        {
            // Instantiate the delegate, telling it what method to call.
            UpdateProgressCallback callback =
                new UpdateProgressCallback(this.DoUpdate);
            // Do something that needs periodic progress reports.
            // This passes a delegate instance that knows how to update the bar.
            DoSomethingLengthy(callback);
            // Clear the bar so that it can be used again.
            progressBar1.Value = 0;
        }
        private void button2_Click(object sender, EventArgs e)
        {
            this.Close();
        }
    }
}
```

![](img/80ff26f06fc9ab951e1cd4257b867366_386_1.png)

顺便提一下，这个类声明很有趣：

```csharp
public partial class Form1 : Form
```

partial 关键字表明这一行只是完整类的一部分。其余部分可以在解决方案资源管理器中列出的 Form1.Designer.cs 文件中找到。（看看它。）在本章后面的“事情发生——C# 事件”一节中，我会重新查看该文件，向你展示关于“事件”的几个要点。C# 2.0 引入的分部类允许你将一个类拆分到两个或多个文件中。编译器生成 Form1.Designer.cs 文件，因此不要直接修改其代码。不过，你可以通过更改窗体上的元素来间接修改它。Form1.cs 是你负责的部分。

## 跟踪委托的生命周期

通过委托生命周期的各个部分来看这个示例：

- 1. **你在类顶部附近定义 UpdateProgressCallback 委托：**
  
  `delegate void UpdateProgressCallback();`
  
  这个委托可以“指向”的方法将是 void，且没有参数。在 delegate 关键字之后，其余部分定义了该委托可以指向的任何方法的签名：其返回类型以及参数的数量、顺序和类型。委托不必是 void——你可以编写返回任意类型并接受任意参数的委托。
  
  定义委托就是定义一种类型，就像 class Student {...} 所做的那样。你可以根据需要将委托声明为 public、internal、protected，甚至 private。
  
  对于定义回调方法的委托类型，通常良好的做法是在其名称后附加 Callback 名称，不过 C# 并不在乎。
  
- 2. **你实例化委托，然后在 button1_Click() 方法中将该实例传递给 DoSomethingLengthy() 方法：**
  
  ```csharp
  UpdateProgressCallback callback =
      new UpdateProgressCallback(this.DoUpdate); // Instantiate the delegate.
  DoSomethingLengthy(callback); // Pass the delegate instance to a method.
  ```
  
  这个委托“指向”此类上的一个方法（而这是可选的）。要指向另一个类上的方法，你需要该类的实例（如果该方法为实例方法），并像这样传递该方法：
  
  ```csharp
  SomeClass sc = new SomeClass();
  UpdateProgressCallback callback =
      new UpdateProgressCallback(sc.DoUpdate);
  ```
  
  但如果该方法是静态方法（位于任何位置），请像这样传递它：
  
  ```csharp
  UpdateProgressCallback callback =
      new UpdateProgressCallback(SomeClass.DoUpdate);
  ```

