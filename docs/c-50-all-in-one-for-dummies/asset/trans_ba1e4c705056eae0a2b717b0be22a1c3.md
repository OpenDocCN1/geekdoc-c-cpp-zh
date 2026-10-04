

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
            // Add the score written to the points
            points.Text = (int)points.Text + (int)scoreBox.Text;
        }
    }
    catch (System.InvalidCastException ext) {
        // Something other than a number
        if (scoreBox.Text.Length > 0) {
            ScoreCheck.SetError(scoreBox, "Score must be a number");
        }
    }
    catch (Exception ex) {
        // Eek!
        MessageBox.Show("Something went wrong!  " + ex.Message);
    }
    // Check the score
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

所有这些屏幕值的更改会导致表单的 `Paint` 事件触发——每当 C# 因为任何需要改变表单的外观时，该事件就会触发——所以我只是在那个事件处理器中丢了一小段代码，用来为我画出棋板：

```csharp
private void CribbageBoard_Paint(object sender, PaintEventArgs e)
{
    PaintBoard(BillsPoints, GabriellesPoints);
}
```

从那时起，我最关注的问题就是绘制棋板本身。

## 绘制棋板

我需要在表单上直接绘制，为我的纸骨牌应用程序创建一个棋板图像，因此我使用了控件的 `CreateGraphics` 方法。从那里开始，我需要完成这些任务：

## 使用 System.Drawing 命名空间 479

- 使用画刷绘制棋板。
- 使用画笔画六行小圆。
- 如果分数正确，则填充线条。
- 清理我的工具。

为了这一目的，我设计了 `PaintBoard` 方法，它接受包含两个玩家分数的标签。如列表 5-1 所示。

## 列表 5-1：PaintBoard 方法

```csharp
private void PaintBoard(ref Label Bill, ref Label Gabrielle)
{
    Graphics palette = this.CreateGraphics();
    SolidBrush brown = new SolidBrush(Color.Brown);
    palette.FillRectangle(brush, new Rectangle(20, 20, 20, 180));
    // 好，我需要画那些孔
    // 棋板上有 244 个小孔
    // 三行，每行 40 个，两端有小起点和终点。
    int rows = 0;
    int columns = 0;
    int scoreDrawing = 0;
    Pen blackPen = new Pen(System.Drawing.Color.Black, 1);
    SolidBrush black = new SolidBrush(Color.Black);
    SolidBrush red = new SolidBrush(Color.Red);
    // 有 6 行，分别在 24、40、80、100、140 和 160 位置。
    for (rows = 0; rows <= 160; rows += 60) {
        // 有 40 列——每隔 20 画一个
        for (columns = 0; columns <= 820; columns += 20) {
            // 计算绘制分数
            scoreDrawing = (columns / 20) + (((rows + 20) / 60) * 40);
            // 绘制 Bill
            if (scoreDrawing == (int)Bill.Text) {
                palette.FillEllipse(blackBrush, columns - 2, 2, 6, 6);
            } else if (scoreDrawing == Bill.LastTotal) {
                palette.FillEllipse(redBrush, columns - 2, 2, 6, 6);
            } else {
                palette.FillEllipse(blackPen, columns - 2, 2, 4, 4);
            }
            // 绘制 Gabrielle
            if (scoreDrawing == (int)Gabrielle.Text) {
                palette.FillEllipse(blackBrush, columns - 2, rows + 16, 6, 6);
            } else if (scoreDrawing == GabrielleLastTotal) {
                palette.FillEllipse(redBrush, columns - 2, rows + 16, 6, 6);
            } else {
            }
        }
    }
```

![](img/6df7bb88e9302e98442acc219cfbd7fc_504_0.png)

（续）

## 列表 5-1（续）

```csharp
palette.DrawEllipse(blackPen, columns - 2, rows + 16, 6, 6);
}
palette.Dispose();
brown.Dispose();
black.Dispose();
red.Dispose();
blackPen.Dispose();
palette.Dispose();
```

## 第6 章：动态

- 理解动态
- 定义变量
- 使用动态

## 使 C# 转向动态类型

所谓的“动态语言”是一种不断反复的趋势，就像夏威夷衫一样。动态语言允许松散类型，而不是静态类型。这个概念始于 20 世纪 60 年代的 LISP。动态语言在 20 世纪 80 年代再次回归，原因有两个：网络管理脚本和人工智能热潮。多亏于网络，热度再次高涨。

