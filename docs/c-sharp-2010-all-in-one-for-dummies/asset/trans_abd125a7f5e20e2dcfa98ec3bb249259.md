
## 打印窗体

在 VB6 及更早版本中，将信息输出到纸张上最常见的方法之一就是打印窗体。.NET 缺少这项功能，但它在 Power Pack 中重新出现，如今已内置于 Visual Studio 2008 中。所有语言都可以使用它，但 VB 程序员最怀念它。

如果需要生成报表，应使用 Microsoft Report Viewer，本书不涉及该内容。不过，如果只是想把一些文本和图像发送到用户的打印机，PrintForm 组件应该能胜任。

要使用 PrintForm 组件，请在“设计”视图中将它从“工具箱”拖到窗体上。它会出现在组件托盘中。

在打印函数的事件处理程序（例如 `MenuItem.Click` 函数）中，设置该组件的 Form 属性、Print Action，然后调用 Print 命令。如下所示：

```
Using PrintForm printForm = new PrintForm
    .Form = TheFormIWantPrinted
    .PrintAction = PrintToPrinter
    .Print()
End Using
```

窗体将被发送到 Windows 打印功能，就像你使用“打印”对话框打印文件一样。

## 绘图类如何融入框架

System.Drawing 命名空间将绘图分为两步：

- 1. 创建一个 System.Drawing.Graphics 对象。
- 2. 使用 System.Drawing 命名空间中的工具在其上绘图。

这似乎很直接，事实也确实如此。第一步是获取一个 Graphics 对象。Graphics 对象主要来自两个地方——现有图像和 Windows 窗体。

要从现有图像获取 Graphics 对象，可以看看 Bitmap 对象。Bitmap 对象是一个很好的工具，它使你能够使用现有图像文件创建对象。这会为你提供一个基于硬盘上已有位图图像（例如 JPEG 文件）的新绘图表面。它是一个方便的工具，尤其适用于 Web 图像。

```
Bitmap currentBitmap = new Bitmap(@"c:\images\myImage.jpg");
Graphics palette = Graphics.FromImage(currentBitmap);
```

现在，myPalette 对象是一个 Graphics 对象，其高度和宽度基于 myBitmap 中的图像。此外，myPalette 图像的基底外观与 myBitmap 对象中引用的图像完全一样。

你可以使用 Graphics 类中的钢笔、画笔和字体直接在该图像上绘图，就像它是一块空白画布一样。我用它在网页上显示图像之前向图像添加文本，也用它即时修改图像格式。

获取 Graphics 对象的另一种方法是从 Windows 窗体获取。你需要的方法是 System.Windows.Forms.Control.CreateGraphics。此方法会为你提供一个新绘图表面，它基于所引用控件的绘图表面。如果该控件是窗体，则它继承窗体的高度和宽度，并具有窗体的背景色。你可以使用钢笔和画笔直接在窗体上绘图。

当你拥有 Graphics 对象后，选择是无穷无尽的。复杂的绘图也并非不可能，不过要用 Visual Studio 创建像《光环 2》中看到的那种图形，你得做大量的工作。（并没有一个可以自动生成的 Master Chief 类。）

尽管如此，即使是最复杂的三维图形也不过是彩色多边形，而你可以用 System.Drawing 类来制作它们。在接下来的几节中，我将使用 Graphics 对象、钢笔、画笔和字体构建一个克里比奇棋盘。

## 使用 System.Drawing 命名空间

好的应用程序可能来自奇怪的地方。Gabrielle（我的妻子）和我喜欢游戏，我们最喜欢的游戏之一是克里比奇纸牌游戏。我们在迪士尼世界度假时，她突然想玩，但我们没有克里比奇棋盘。我们有牌，但没有棋盘。

不过，我确实带着笔记本电脑、Visual Studio 和 System.Drawing 命名空间。仅仅工作了一两个小时，我就构建了一个可作为可用克里比奇棋盘的应用程序！

我知道这很令人震惊，但不知何故，她看我编程两小时后仍然想和我玩！

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_498_0.png)

这个应用程序相当完整，我没有足够的篇幅带你一步步完成它。请从本书网站加载该应用程序，并跟随本章其余内容学习。这个应用程序并不复杂，但篇幅很长。

## 开始

克里比奇是一种纸牌游戏，每手牌会计分，最先得到 121 分的玩家获胜。玩家需要自行计算分数，分数记录在棋盘上。

克里比奇棋盘由两排用于插棋子的孔组成，通常总共 120 个孔，但有时使用 60 个孔，需要玩两遍。图 5-1 显示了一个典型的克里比奇棋盘。克里比奇棋盘有多种样式——如果你好奇，可以访问 www.cribbage.org；那里有一个很棒的图库，展示了近 100 个棋盘，从基础款到奇思妙想款应有尽有。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_499_0.png)

图 5-1：
一个传统的克里比奇棋盘。

在本例中，我为记录克里比奇游戏分数的应用程序创建棋盘图像——但用 C# 把纸牌也写进游戏也并非不可能！

因此，此应用程序的棋盘有三对线，每对线上有 40 个孔，这是两名玩家玩到 120 分的标准棋盘布局，如图 5-2 所示。第一项任务是绘制棋盘，然后随着玩家分数（在文本框中输入）变化绘制棋子。

其前提如下：玩家玩一手牌，并将所得分数输入各自姓名下方的文本框中（参见图 5-2）。输入每手牌的分数后，玩家姓名旁的分数会更新，棋盘上的棋子也会移动。下一次同一玩家得分时，前面的棋子向前移动，后面的棋子移到它的位置。我提到过后面的棋子吗？哦，是的，克里比奇的发明者多疑，怕人作弊——如果你不熟悉克里比奇，不妨到 www.cribbage.org 查看规则。

图 5-2：
数字克里比奇棋盘。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_500_0.png)

## 设置项目

首先，创建一个游戏界面。我搭建了图 5-2 所示的棋盘，但没有绘制棋盘本身——稍后我会向你展示如何使用 System.Drawing 绘制它。当我准备开始处理业务规则时，我的棋盘看起来很像图 5-3。

![](img/1b3d2e7c2a257973c8a9dd11ef5f13cd_500_1.png)

图 5-3：
基础棋盘。

我用一个小型子例程来处理分数变化，通过从两个文本框的 OnChange 事件中调用它来实现。以下是调用该子例程的代码：

```
private void HandleScore(TextBox scoreBox, Label points, Label otherPlayer)
{
    try {
        if (0 > (int)scoreBox.Text || (int)scoreBox.Text > 27) {
            ScoreCheck.SetError(scoreBox, "Score must be between 0 and 27");
            scoreBox.Focus();
        }
    }
else {
    ScoreCheck.SetError(scoreBox, "");
    //Add the score written to the points
    points.Text = (int)points.Text + (int)scoreBox.Text;
}
catch (System.InvalidCastException ext) {
    //Something other than a number
    if (scoreBox.Text.Length > 0) {
        ScoreCheck.SetError(scoreBox, "*Score must be a number*");
    }
}
catch (Exception ex) {
    //Eek!
    MessageBox.Show("Something went wrong! " + ex.Message);
}
//Check the score
if ((int)points.Text > 120) {
    if ((int)points.Text > (int)otherPlayer.Text > 1.5) {
        WinMessage.Text = scoreBox.Name.Substring(0, scoreBox.Name.Length - 6) + " Skunked 'em!!!";
    }
    else {
        WinMessage.Text = scoreBox.Name.Substring(0, scoreBox.Name.Length - 6) + " Won!!";
    }
    WinMessage.Visible = true;
}
```

所有这些屏幕值的更改都会触发表单的 Paint 事件——每当 C# 因任何原因需要更改窗体的外观时，此事件都会触发——因此我只是在该事件处理程序中加入了一小段代码，让它为我绘制棋盘：

```
private void CribbageBoard_Paint(object sender, PaintEventArgs e)
{
    PaintBoard(BillsPoints, GabriellesPoints);
}
```

从那时起，我最关心的是绘制棋盘本身。

## 绘制棋盘

我需要直接在窗体上绘制，以为我的克里比奇应用程序创建棋盘图像，因此我使用窗体控件的 CreateGraphics 方法。接下来，我需要完成以下任务：

- 使用画笔将棋盘涂成棕色。
- 使用钢笔绘制六行小圆圈。
- 如果该分数正确，则填充孔。
- 清理我的绘图资源。

