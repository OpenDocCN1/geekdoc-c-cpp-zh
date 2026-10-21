

## 第14章

class 还定义了操作 CPoint 和 POINT 对象的成员函数。这看起来可能很奇怪，因为 CPoint 看起来会使 POINT 对象过时，但请记住 Windows API 是在 MFC 出现之前构建的，而 POINT 对象在 Windows API 中使用，并且迟早必须处理。CPoint 对象在示例中使用，因此您有机会看到一些成员函数的实际运行情况。

MoveTo() 函数的返回值是一个 CPoint 对象，该对象指定移动前的当前位置。你可能会觉得这有点奇怪，但考虑一下你想要移动到新位置、绘制某些内容，然后再移回来的情况。在移动之前，你可能不知道当前位置，而在移动发生后，它就会丢失，因此返回移动前的当前位置可以确保在需要时它仍然可用。

### 绘制线条

你可以在 OnDraw() 函数中对 MoveTo() 的调用之后加上对 LineTo() 函数的调用，该函数在客户端区域内从当前位置绘制一条线到 LineTo() 函数参数指定的点，如图 14-4 所示。

![](img/2359b0c604600c58fba3539c738a356e_755_0.png)

CDC 类还定义了 LineTo() 函数的两个版本，其原型如下：

BOOL LineTo(int x, int y); // Draw a line to position x,y
BOOL LineTo(CPoint aPoint); // Draw a line to position defined by aPoint

这为你指定函数参数提供了与 MoveTo() 相同的灵活性。你可以使用 CPoint 对象作为第二个版本函数的参数。函数在绘制线条时返回 TRUE，否则返回 FALSE。

当执行 LineTo() 函数时，当前位置会更改为指定线条末端的点。这使你只需为每条线调用 LineTo() 函数即可绘制一系列连接的线条。看一下 OnDraw() 函数的以下版本：

### 在窗口中绘制

```cpp
void CSketchView::OnDraw(CDC* pDC)
{
	CSketchDoc* pDoc = GetDocument();
	ASSERT_VALID(pDoc);
	if(!pDoc)
		return;
	pDC->MoveTo(50,50); // Set the current position
	pDC->LineTo(50,200); // Draw a vertical line down 150 units
	pDC->LineTo(150,200); // Draw a horizontal line right 100 units
	pDC->LineTo(50,50); // Draw a vertical line up 150 units
	pDC->LineTo(50,50); // Draw a horizontal line left 100 units
}
```

如果你将此代码放入 Sketcher 程序并执行它，它会显示如图 14-5 所示的文档窗口。

![](img/2359b0c604600c58fba3539c738a356e_756_0.png)

对 LineTo() 函数的四次调用按逆时针方向绘制了所示的矩形，从左上角开始。第一次调用使用 MoveTo() 函数设置的当前位置；后续调用使用前一次 LineTo() 函数调用设置的当前位置。你可以用此方法绘制由一系列线段组成的任意图形，每条线都与前一条线连接。当然，你也可以随时使用 MoveTo() 来更改当前位置。

### 绘制圆圈

CDC 类中提供了多种用于绘制圆圈的函数成员，但它们都设计用于绘制椭圆。正如你从高中几何学中所知，圆是椭圆的一种特殊情况，

其长轴和短轴相等。因此，你可以使用成员函数 Ellipse() 来绘制圆。与 CDC 类支持的其他封闭形状一样，Ellipse() 函数会用你设置的颜色填充形状的内部。内部颜色由选入设备上下文的画刷决定。设备上下文中的当前画刷决定了任何封闭形状的填充方式。

MFC 提供了 CBrush 类，可用于定义画刷。你可以设置 CBrush 对象的颜色，还可以定义填充封闭形状时产生的图案。如果你想绘制一个不填充的封闭形状，可以使用空画刷，使形状内部保持为空。我将在本章稍后再次讨论画刷。

另一种绘制未填充圆圈的方法是使用 Arc() 函数，该函数不涉及画刷。这具有这样的优点：你可以绘制椭圆的任意弧段，而不仅仅是完整的曲线。CDC 类中提供了该函数的两个版本，声明如下：

```
BOOL Arc(int x1, int y1, int x2, int y2, int x3, int y3, int x4, int y4);
BOOL Arc(LPRECT lpRect, POINT StartPt, POINT EndPt);
```

在第一个版本中，(x1,y1) 和 (x2,y2) 定义了包含完整曲线的矩形的左上角和右下角。如果你将这些坐标设为正方形的角落，所绘制的曲线就是圆的一部分。点 (x3,y3) 和 (x4,y4) 定义了要绘制的线段的起点和终点。线段按逆时针方向绘制。如果你使 (x4,y4) 与 (x3,y3) 相同，你将生成一个完整的、看似封闭的曲线。

在 Arc() 的第二个版本中，包围矩形由 RECT 对象定义，并将指向该对象的指针作为第一个参数传递。该函数还接受指向 CRect 类对象的指针，该类有四个公共数据成员：left、top、right 和 bottom。它们分别对应矩形的左上角和右下角的 x 和 y 坐标。该类还提供了一系列操作 CRect 对象的函数成员，我们稍后会用到其中的一些。

第二个版本 Arc() 中的 POINT 对象 StartPt 和 EndPt 定义了要绘制的弧的起点和终点。

以下是同时使用 Arc() 函数两个版本的代码：

```
void CSketcherView::OnDraw(CDC* pDC)
{
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    if (!pDoc)
        return;

    pDC->Arc(50,50,150,150,100,50,150,100);  // Draw the 1st (large) circle

    // Define the bounding rectangle for the 2nd (smaller) circle
    CRect* pRect = new CRect(250,50,300,100);
    CPoint Start(275,100);                  // Arc start point
    CPoint End(250,75);                     // Arc end point
    pDC->Arc(pRect,Start, End);             // Draw the second circle
    delete pRect;
}
```

请注意，你使用了 CRect 类对象而不是 RECT 结构来定义包围矩形，并且使用了 CPoint 类对象而不是 POINT 结构。你稍后还会使用 CRect 对象，但它们有一些限制，如你将看到的那样。Arc() 函数不需要设置当前位置，因为弧的位置和大小完全由你提供的参数定义。绘制弧不会影响当前位置——它仍然完全保持在绘制弧之前的原位置。虽然坐标可以是 _32K，但包围形状的矩形的最大宽度或高度为 32,767，因为这是有符号 16 位整数可以表示的最大正值。

现在尝试使用此代码运行 Sketcher 中的 OnDraw() 函数。你应该得到如图 14-6 所示的结果。

![](img/2359b0c604600c58fba3539c738a356e_758_0.png)

图 14-6

尝试重新调整边框大小。随着你覆盖或显示图片中的弧线，客户端区域会自动重绘。请记住，屏幕分辨率会影响显示的比例。你使用的屏幕分辨率越低，弧线在客户端区域中就越大，并且离左上角越远。

### 彩色绘制

到目前为止，我们绘制的所有内容都以黑色出现在屏幕上。绘制意味着使用具有颜色和粗细的画笔对象，而你一直在使用设备上下文中提供的默认画笔对象。当然，你不必这样做——你可以创建具有给定粗细和颜色的自己的画笔。MFC 定义了 CPen 类来帮助你做到这一点。

你绘制的所有封闭曲线都用设备上下文中的当前画刷填充。如前所述，你可以将画刷定义为 CBrush 类的实例。看看 CPen 和 CBrush 对象的一些特性。

