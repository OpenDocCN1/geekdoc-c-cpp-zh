

The Limits > Upper and Limits > Lower 菜单项允许使用更受限制的值范围来生成条目。这里也需要进行检查；该范围必须在给定彩票允许的范围内，并且范围必须足够宽，以允许生成所需数量的不同值。

最后，Help > About 菜单项应显示一个消息框，其中显示有关应用程序的信息。

使应用程序按前面所述运行的第一步是为显示彩票条目值的按钮添加上下文菜单。这出乎意料地容易。

## Adding a Context Menu

CLR Forms 应用程序中的上下文菜单只是一个控件。它是工具箱窗口中“菜单和工具栏”组中的 ContextMenuStrip 控件。单击 ContextMenuStrip 控件，然后单击编辑器窗口底部灰色区域以将控件添加到应用程序。上下文菜单显示在现有菜单下方的窗体中。如果单击第一个菜单，您可以插入项目名称。您可以为菜单项的文本输入 &Choose，这使得 Alt+C 成为该项目的加速键。最好为上下文菜单提供更有意义的名称，因此打开 ContextMenuStrip 控件的属性窗口并将其 (Name) 属性值更改为 buttonContextMenu。您也可以将 Choose 菜单项的 (Name) 属性值更改为 chooseValue。

现在您可以将 buttonContextMenu 控件启用为两个彩票条目选项卡上的每个按钮的上下文菜单。为此，将每个按钮的 ContextMenuStrip 属性值设置为 ContextMenuStrip 控件的名称 buttonContextMenu。名称出现在属性值单元格的下拉列表中，因此您只需单击它即可设置值。

## Creating Event Handlers

使用 Form Design 功能以图形方式构建 GUI 的过程已自动为添加的控件生成代码。Form1 类现在为添加到窗体的每个控件都有一个成员，并且已将初始化这些控件的代码添加到 InitializeComponent() 函数中。如果查看该函数，您会看到它现在包含大量设置单个控件属性并将控件组装到其容器中的代码。以图形方式创建 GUI 轻而易举——您需要动用更多脑细胞才能在此基础上推进应用程序。

为了使程序按您想要的方式工作，您必须为应用程序要识别和处理的事件创建事件处理程序函数，并实现这些函数以使用户与 GUI 的交互按您想要的方式进行。虽然无法自动生成处理事件的代码，但 IDE 仍可以通过生成事件处理程序函数的骨架并将其注册到事件委托来提供帮助。

您可以通过单击控件的属性窗口中的事件按钮来查看控件的事件。这会显示控件的所有可能事件，您可以在事件名称右侧的单元格中设置要处理特定事件的函数的名称。当然，您只为想要识别的事件标识处理程序函数，而在大多数情况下，这只是控件可能事件的很小一部分。您需要为所有菜单项的菜单项和选项卡上的每个按钮的 Click 事件创建处理程序函数。创建处理程序函数以使控件响应 Click 事件有一个快捷方式；您只需在编辑器窗口中双击控件，代码就会被创建并显示，并且该函数会被注册为事件对象的处理程序。这为控件创建了唯一的事件处理程序，但有时您希望让单个函数处理多个控件的同类事件。在这种情况下，属性窗口的方式是可行的方法。

## Event Handlers for Menu Items

您可以先为 Play 菜单项创建一个事件处理程序函数。双击菜单项会创建以下处理程序函数代码：

```
private: System::Void playMenuItem_Click(System::Object^ sender,
    System::EventArgs^ e)
{
}
```

这是一个骨架处理程序，函数体中没有任何代码。第一个参数是引用事件源控件的句柄，第二个参数提供与事件相关的信息。当调用处理程序时，第一个参数的类型对应于产生事件的控件的类型，在本例中为 ToolStripMenuItem^，因为在单击 Play 菜单项时调用处理程序函数；菜单项句柄存储在 Form1 类的 playMenuItem 成员中，您可以在类定义中查看其类型。同样，Click 事件处理程序的第二个参数的实际类型取决于控件的类型。

默认生成的处理程序函数名为 playMenuItem_Click。您不得在代码中更改函数名。事实上，我建议您不要更改自动生成的代码中的任何名称；始终通过属性窗口进行更改。如果您不喜欢为事件处理程序函数创建的名称，可以通过控件的属性窗口中的 Click 事件属性值来更改它。

处理程序函数名已通过 InitializeComponent() 函数中的以下语句注册到事件对象：

```
this->playMenuItem->Click +=
    gcnew System::EventHandler(this, &Form1::playMenuItem_Click);
```

此语句将函数名添加到 Form1 类的成员 playMenuItem 对象的 Click 委托中。您已在第 9 章中了解了委托以及如何注册事件处理程序函数。

您可以通过双击每个菜单项来为 Limits > Upper、Limits > Lower 和 Help > About 菜单项添加处理程序。您也可以对上下文菜单中的 Choose 菜单项执行相同的操作。

## Adding Members to the Form1 Class

在开始实现菜单项的处理程序之前，您需要一些额外的字段来存储与彩票条目值约束相关的数据。您知道如何向 Form1 类添加新字段；这就是您已经大量使用的方式向类添加成员。切换到 Class View，右键单击 Form1 类，并从上下文菜单中选择 Add > Add Variable。或者，您也可以手动添加代码，但请确保您不会侵入为 Form Design 操作保留的类定义区域。您需要将以下变量作为私有成员添加：

```
private:
    int lottoValuesCount;              // Number of values in Lotto entry
    int euroValuesCount;               // Number of values in Euromillions entry
    int euroStarsCount;                // Number of stars in Euromillions entry
    int lottoLowerLimit;               // Minimum value allowed in Lotto
    int lottoUpperLimit;               // Maximum value allowed in Lotto
    int lottoUserMinimum;              // Lower lotto range limit from user
    int lottoUserMaximum;              // Upper lotto range limit from user

    int euroLowerLimit;                // Minimum value allowed in Euromillions
    int euroUpperLimit;                // Maximum value allowed in Euromillions
    int euroStarsLowerLimit;           // Minimum stars value allowed in Euromillions
    int euroStarsUpperLimit;           // Maximum stars value allowed in Euromillions
    int euroUserMinimum;               // Lower euro range limit from user
    int euroUserMaximum;               // Upper euro range limit from user
    int euroStarsUserMinimum;          // Lower euro stars range limit from user
    int euroStarsUserMaximum;          // Upper euro stars range limit from user
```

您还需要在 Form1 类中添加一个类型为 Random 的私有字段：

```
Random^ random;                     // Generates pseudo-random numbers
```

Random 类型的对象可以生成各种类型的伪随机值。您将使用它来生成彩票条目的值。

所有这些字段都必须在类构造函数中初始化。确保 Form1 构造函数定义看起来与此类似：

```
public ref class Form1 : public System::Windows::Forms::Form
{
public:
    Form1(void)
    : lottoValuesCount(6),
      euroValuesCount(5), euroStarsCount(2),
      lottoLowerLimit(1), lottoUpperLimit(49),
      lottoUserMinimum(lottoLowerLimit), lottoUserMaximum(lottoUpperLimit),
      euroLowerLimit(1), euroUpperLimit(50),
      euroStarsLowerLimit(1), euroStarsUpperLimit(9),
      euroUserMinimum(euroLowerLimit), euroUserMaximum(euroUpperLimit),
      euroStarsUserMinimum(euroStarsLowerLimit), euroStarsUserMaximum(euroStarsUpperLimit)
    {
        InitializeComponent();
        //
        random = gcnew Random;
        //
    }
```

就目前而言，您需要的就是这些新的类数据成员，回到事件处理。

