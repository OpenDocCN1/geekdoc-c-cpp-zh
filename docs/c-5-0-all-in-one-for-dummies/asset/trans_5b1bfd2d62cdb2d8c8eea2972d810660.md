
你可以使用 Graphics 类中的笔、画笔和字体直接在此图像上绘制，就像它是一块空白画布一样。我用它在将图像显示到网页上之前向图像添加文本，也用它即时修改图像的格式。

获取 Graphics 对象的另一种方法是从 Windows Forms 中获取。你需要的方法是 `System.Windows.Forms.Control.CreateGraphics`。此方法会为你提供一个新调色板，它基于所引用控件的绘图表面。如果它是一个窗体，它会继承窗体的高度和宽度，并具有窗体的背景色。你可以使用笔和画笔直接在窗体上绘制。

当你拥有一个 Graphics 对象时，可选项无穷无尽。复杂的绘图并非不可能，不过要想使用 Visual Studio 创建像你在 *光环* 中看到的那种图形，你得做大量工作。（并没有一个可以自动生成的 Master Chief 类。）

尽管如此，即使是最复杂的三维图形也不过是带颜色的多边形，而你可以使用 `System.Drawing` 类来制作它们。在接下来的几节中，我将使用 Graphics 对象、笔、画笔和字体构建一个克里比奇棋盘。

## 使用 System.Drawing 命名空间

好的应用程序往往来自奇怪的契机。加布里埃尔（我的妻子）和我喜欢游戏，我们最喜欢的游戏之一是纸牌游戏克里比奇。我们在迪士尼世界度假时，她突然很想玩，但我们没有克里比奇棋盘。我们有牌，但没有棋盘。

不过，我带了笔记本电脑、Visual Studio 和 `System.Drawing` 命名空间。仅仅工作了一两个小时后，我就构建了一个可用作克里比奇棋盘的程序！

我知道这很令人震惊，但不知怎么的，在看我编程两个小时后，她仍然想和我对战！

这个应用程序相当完整，而我没有足够的篇幅带你逐步完成它。请从本书网站加载该应用程序，并跟随本章剩余内容一起操作。这个应用程序并不复杂，但篇幅很长。

![](img/80ff26f06fc9ab951e1cd4257b867366_500_0.png)

第 III 册
第 5 章
创建图像

### 入门

克里比奇是一种纸牌游戏，玩家将一手牌计为分数，最先得到 121 分的玩家获胜。计分由玩家自己完成，分数记录在棋盘上。

克里比奇棋盘由两排用于插计分钉的孔组成，通常总共有 120 个孔，但有时使用 60 个孔，需要玩两轮。图 5-1 展示了一个典型的克里比奇棋盘。克里比奇棋盘有各种样式——如果你好奇，可以访问 www.cribbage.org；那里有一个很棒的图库，展示了近 100 种棋盘，从基础款到奇趣款应有尽有。

在这个示例中，我为记录克里比奇游戏分数的应用程序创建棋盘图像——不过用 C# 把纸牌也写进游戏中，也并非做不到！

因此，这个应用程序的棋盘在每对线中的每一排上各有 40 个孔，共三对线，这是两名玩家玩到 120 分的标准棋盘布局，如图 5-2 所示。第一项任务是绘制棋盘，然后随着玩家分数（在文本框中输入）的变化绘制计分钉。

![](img/80ff26f06fc9ab951e1cd4257b867366_501_0.png)

**图 5-1：**
一个传统的克里比奇棋盘。

![](img/80ff26f06fc9ab951e1cd4257b867366_502_0.png)

**图 5-2：**
数字克里比奇棋盘。

其前提是这样的：玩家玩一手牌，并将所得分数输入各自名字下方的文本框中（参见图 5-2）。输入每手牌的分数后，玩家名字旁边的分数会更新，棋盘上的计分钉也会移动。下一次同一玩家得分时，前面的计分钉向前移动，后面的计分钉移到它的位置。我提到后面的计分钉了吗？哦，提到了，克里比奇的发明者很多疑，怕人作弊——如果你不熟悉克里比奇，不妨访问 www.cribbage.org 查看规则。

## 设置项目

首先，创建一个游戏界面。我设置了图 5-2 所示的棋盘，但没有绘制棋盘本身——稍后我会向你展示如何使用 System.Drawing 将它画上去。当我准备开始处理业务规则时，我的棋盘看起来很像图 5-3。

![](img/80ff26f06fc9ab951e1cd4257b867366_502_1.png)

**图 5-3：**
基本棋盘。

我用一个小型子程序来处理分数变化，通过从两个文本框的 OnChange 事件中调用它来实现。下面是调用该子程序的代码：

第 III 册
第 5 章
创建图像

```csharp
private void HandleScore(TextBox scoreBox, Label points, Label otherPlayer)
{
    try {
        if (0 > (int)scoreBox.Text || (int)scoreBox.Text > 27) {
            ScoreCheck.SetError(scoreBox, "Score must be between 0 and 27");
            scoreBox.Focus();
        }
        else {
            ScoreCheck.SetError(scoreBox, "");
            //Add the score written to the point
            points.Text = (int)points.Text + (int)scoreBox.Text;
        }
    }
    catch (System.InvalidCastException ex) {
        //Something other than a number
        if (scoreBox.Text.Length > 0) {
            ScoreCheck.SetError(scoreBox, "Score must be a number");
        }
    }
    catch (Exception ex) {
        //Eek!
        MessageBox.Show("Something went wrong!  " + ex.Message);
    }
    //Check the score
    if ((int)points.Text > 120) {
        if ((int)points.Text / (int)otherPlayer.Text > 1.5) {
            WinMessage.Text = scoreBox.Name.Substring(0, scoreBox.Name.Length - 6) + " Skunked 'em!!!";
        }
        else {
            WinMessage.Text = scoreBox.Name.Substring(0, scoreBox.Name.Length - 6) + " Won!!!";
        }
        WinMessage.Visible = true;
    }
}
```

所有这些屏幕值的变化都会触发表单的 Paint 事件——每当 C# 因任何原因需要改变窗体外观时，该事件都会触发——所以我只是在该事件处理程序中放入了一点代码，让它为我绘制棋盘：

```csharp
private void CribbageBoard_Paint(object sender, PaintEventArgs e)
{
    PaintBoard(BillsPoints, GabriellesPoints);
}
```

从那时起，我最大的关注点就是绘制棋盘本身。

## 绘制棋盘

我需要直接在窗体上绘制，以便为我的克里比奇应用程序创建棋盘图像，因此我使用窗体控件的 CreateGraphics 方法。接下来，我需要完成以下任务：

- 使用画笔将棋盘涂成棕色。
- 使用笔绘制六排小圆圈。
- 如果分数正确，则填充该孔。
- 清理我的绘图工具。

为此，我设计了一个 PaintBoard 方法，它接受包含两名玩家当前分数的标签。该方法见代码清单 5-1。

### 代码清单 5-1：PaintBoard 方法

```csharp
private void PaintBoard(ref Label Bill, ref Label Gabrielle)
{
    Graphics palette = this.CreateGraphics();
    SolidBrush brownBrush = new SolidBrush(Color.Brown);
    palette.FillRectangle(brownBrush, new Rectangle(20, 20, 820, 180));
    //OK, now I need to paint the little holes.
    //There are 244 little holes in the board.
    //Three rows of 40 times two, with the little starts and stops on either end.
    //Let's start with the 240.
    int rows = 0;
    int columns = 0;
    int scoreBeingDrawn = 0;
    Pen blackPen = new Pen(System.Drawing.Color.Black, 1);
    SolidBrush blackBrush = new SolidBrush(Color.Black);
    SolidBrush redBrush = new SolidBrush(Color.Red);

    //There are 6 rows, then, at 24 and 40, 80 and 100, then 140 and 160.
    for (rows = 40; rows <= 160; rows += 60) {
        //They are 40 columns. They are every 20
        for (columns = 40; columns <= 820; columns += 20) {
            //Calculate score being drawn
            scoreBeingDrawn =
                ((columns - 20) / 20) + (((rows + 20) / 60) - 1) * 40;
            //Draw Bill
            //If score being drawn = bill fill, otherwise draw
            if (scoreBeingDrawn == (int)Bill.Text) {
                palette.FillEllipse(blackBrush, columns - 2, rows - 2, 6, 6);
            }
            else if (scoreBeingDrawn == BillsLastTotal) {
                palette.FillEllipse(redBrush, columns - 2, rows - 2, 6, 6);
            }
            else {
                palette.DrawEllipse(blackPen, columns - 2, rows - 2, 4, 4);
            }

            //Draw Gabrielle
            //If score being drawn = Gabrielle fill, otherwise draw
            if (scoreBeingDrawn == (int)Gabrielle.Text) {
                palette.FillEllipse(blackBrush, columns - 2, rows + 16, 6, 6);
            }
            else if (scoreBeingDrawn == GabriellesLastTotal) {
                palette.FillEllipse(redBrush, columns - 2, rows + 16, 6, 6);
            }
            else {
                ...
            }
        }
    }
}
```
