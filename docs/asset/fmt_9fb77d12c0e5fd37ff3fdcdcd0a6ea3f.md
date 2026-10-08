
`void CSketcherView::OnButtonDown(UINT nFlags, CPoint point)`

```
{
    m_FirstPoint = point; // 记录光标位置
}
```

该处理程序只是记录传入的参数。在这种情况下，你可以完全忽略第一个参数。

你还没有完成 `WM_MOUSEMOVE` 处理程序，但可以尝试概述其代码：

```cpp
void CSketcherView::MouseMove(UINT nFlags, CPoint point)
{
    if (nFlags & MK_LBUTTON) // 验证左键被按下
    {
        m_SecondPoint = point; // 保存当前光标位置
        // 测试之前的元素
        {
            // 如果有之前的鼠标移动
            // 添加删除旧元素的代码
        }
        // 添加新元素的代码
        // 并进行绘制
    }
}
```

验证左键被按下是重要的，因为你只想在这种情况下处理鼠标移动。如果没有这个检查，那么当右键被按下或未按下任何键移动鼠标时，你也会处理事件。

如果左键被按下，你保存当前光标位置。这是元素的第二个点。其余逻辑在术语上是的，但在完成函数之前，你需要建立一些事情。你还没有定义元素的方法——你会希望将元素定义为类，所以必须定义一些类。你还必须在创建新元素时设计一种删除元素并绘制元素的方法。这里需要一个简短的插叙。

## 客户区域重绘

绘制或擦除元素涉及重绘窗口的客户区域。正如你已经发现的，客户区域是由 `View` 类的 `OnDraw` 成员函数绘制的，当 `Sketch` 应用程序接收到 `WM_PAINT` 消息时就会调用该函数。所有重绘客户区域的基本消息，Windows 都提供了关于需要重绘区域的信息。当你显示只需要重绘的复杂图像时，这可以节省大量时间。你可以通过调用类的 `Invalidate()` 方法来告诉 Windows 特定区域应该重绘。该函数需要两个参数。第一个是指向 `RECT` 或 `CRect` 对象的指针，定义要重绘的客户区域矩形。传递 `nullptr` 会重绘整个客户区域。

你想要触发重绘某个区域的典型情况是某些内容发生了使其必须重绘的变化——例如移动在客户区域中显示的内容就是其中一种。在这种情况下，你需要在绘制新版本之前，先擦除背景以移除之前显示内容的旧表示。当你想要在现有背景上进行绘图时，向 `InvalidateRect()` 的第二个参数传递 `FALSE`。

调用 `InvalidateRect()` 不会直接导致窗口的任何部分重绘；它向 Windows 通信你需要重绘的矩形。Windows 会创建一个累积区域——实际上是一个矩形——用于标识窗口中需要重绘的总区域，这可能是由多次调用 `InvalidateRect()` 引起的。你调用 `InvalidateRect()` 时指定的区域会被添加到当前更新区域中，因此新的更新区域将包含旧区域加上你识别出的新矩形。当 `WM_PAINT` 消息发送到窗口时，更新区域将随消息一起传递给窗口对象。当 `WM_PAINT` 消息处理完成后，更新区域将重置为空状态。调用视图类中继承的 `UpdateWindow()` 函数会向视图发送 `WM_PAINT` 消息。

因此，要获取一个新创建的元素，你需要：

1. 确保视图中的 `OnDraw()` 函数在重绘窗口时包含了新创建的元素。
2. 调用 `InvalidateRect()`，并将指向要重绘的矩形元素的指针作为第一个参数。
3. 通过调用视图继承的 `UpdateWindow()` 函数向视图发送 `WM_PAINT` 消息。

同样地，如果你从视图的客户区域中删除了一个元素，你需要执行以下操作：

1. 从 `OnDraw()` 函数将绘制的元素列表中移除该项。
2. 调用 `InvalidateRect()`，并将第一个参数指向要移除的边界矩形。
3. 通过调用视图的 `UpdateWindow()` 函数向视图发送 `WM_PAINT` 消息。

由于更新区域的背景会被自动擦除，只要 `OnDraw()` 函数不再再次绘制该元素，该元素就会消失。当然，这意味着你必须能够获取你所创建的边界元素，因此你需要在定义 `Sketcher` 元素的类中编写一个函数，作为成员返回此矩形。

## 定义元素类

考虑一下，由于你要以某种方式在文档中绘制草图元素，如果草图要具有任何持久性，你将将文档存储在文件中以便后续取回。我稍后处理文件操作的细节，但现在知道 MFC 类 `COb` 包含了你执行此操作的工具即可，因此你把 `COb` 作为定义草图元素的基类。

你无法预知用户将创建什么类型的元素序列，因此 `Sketcher` 必须能够处理任何元素序列。这表明使用基类指针来存储最新创建元素的地址可能会简化工作。你可以在不需要确切知道它是什么类型元素的情况下调用元素函数。例如，你不需要知道它是什么元素就可以进行绘图。只要你通过基类指针访问元素，你始终可以通过调用虚拟函数让元素自己绘制自己。要实现这一点，你只需要确保定义元素的类共享一个公共基类，并且在基类中将所有希望在运行时以多态方式调用的函数声明为 `virtual`。你可以像图 14-12 所示组织元素类。

![](img/382e3fc55bbc8265676aa869d85a0e73_751_0.png)

图 14-12

图中的每个箭头都指向基类。如果你需要添加另一种类型的元素，可以从 `CElement` 派生另一个类。你可以通过在类视图中右键点击 `Sketcher` 并从弹出窗口中选择“添加类”来创建 `CElement` 类。从安装的模板列表中选择 MFC，然后在中间面板中选择 MFC 类。当你点击对话框中的添加按钮时，会显示另一个对话框，在其中你可以指定类名并选择基类，如图 14-13 所示。

## 鼠标编程

![](img/382e3fc55bbc8265676aa869d85a0e73_752_0.png)

图 14-13

我已经将类名填入为 `CElement`，并从下拉列表中选择了 `CObject` 作为基类。当你点击“完成”按钮时，就会生成类定义的代码：

```
#pragma once
// CElement command target
class CElement : public CObject
{
public:
    CElement();
    virtual ~CElement();
}
```

为你声明的成员是一个 `.cpp` 构造函数和一个虚拟析构函数，这些函数的骨架定义出现在 `Element.cpp` 文件中。你看到向导包含了 `#pragma once` 指令，以确保头文件的内容不会被包含到另一个文件的多次。

你可以使用相同的过程添加其他元素类。由于其他元素类的基类是 `CElement` 而不是基类，你应该将类类别设置为 C++。

## 在窗口中绘图

![](img/382e3fc55bbc8265676aa869d85a0e73_753_0.png)

图 14-14

更新区域的背景会被自动擦除，只要 `OnDraw()` 函数不再再次绘制该元素，该元素就会消失。当然，这意味着你必须能够获取你所创建的边界元素，因此你需要在定义 `Sketcher` 元素的类中编写一个函数，作为成员返回此矩形。

## 在视图中存储临时元素

更新区域的背景会被自动擦除，只要 `OnDraw()` 函数不再再次绘制该元素，该元素就会消失。当然，这意味着你必须能够获取你所创建的边界元素，因此你需要在定义 `Sketcher` 元素的类中编写一个函数，作为成员返回此矩形。

## CElement 类

随着你增加 `Sketcher` 的功能，你将增量地开发元素类——某些数据项（如颜色和位置）是所有元素共，因此你可以将它们放在 `CElement` 基类中。定义特定属性的其他数据成员将在派生类中声明。

`CElement` 类将包含将在派生类中实现的虚拟函数，以及所有派生类共有的数据成员。虚拟函数将是通过 `CElement*` 指针针对特定对象进行多态选择的函数。

```
class CElement: public COb
protected:
    CPoint m_StartPosition; // 元素位置
    int m_PenWidth; // 笔画
    COLORREF m_Color; // 元素的颜色
    CRect m_EnclosingRect; // 包含元素的矩形
public:
    virtual ~CElement();
    virtual void Draw(CDC* pDC); // 虚拟绘制操作
// 获取元素的边界矩形
CRect &GetEnclosingRect() const { return m_EnclosingRect; }
// 保护，以便在类外无法调用
CElement();
CElement(const CPoint& start, COLORREF color, int penWidth = 1);
```

## 第 14 章 在窗口中绘图

你可能会想在 `CElement` 类中将 `Draw()` 成员声明为纯虚函数，并让派生类去定义——毕竟，在这里它没有意义的内容。通常情况下你会这样做，但 `CElement` 继承了 `COject` 的名为“序列化”（serialization）的功能，你之后将用它将元素对象存储到文件中。序列化要求 `CElement` 不能是抽象类，并且能够创建该类型的对象。如果你使用 MFC 的序列化功能，你的类不能是抽象的，并且它们必须有一个无参数构造函数。

> 注意：序列化是将对象写入文件的一个通用术语。

你可以在 `Element.cpp` 中为新构造函数添加定义：

```
CElement::CElement(const CPoint& start, COLORREF color, int penWidth) :
    m_StartPoint(start), m_PenWidth(penWidth), m_Color(color) {}
```

所有成员变量都在初始化列表中初始化；构造函数体不需要代码。

## CLine 类

你可以将 `CLine` 类的定义修改如下所示：

```
class CLine : public CElement
{
public:
    virtual ~CLine();
    virtual void Draw(CDC* pdc) override; // 显示线条的函数
    // 线对象的构造函数
    CLine(const CPoint& start, const CPoint& end, COLORREF aColor);
protected:
    CPoint m_EndPoint; // 线的终点
protected:
    CLine(); // 默认构造函数不应被使用
};
```

线由两个点定义：从 `CElement` 继承的 `m_StartPoint` 和 `m_EndPoint`。该类有一个公共构造函数，其参数用于定义线条的数值，而无参数构造函数已移动到类的 `protected` 部分以防止在外部使用。构造函数参数是 `const` 引用，以避免拷贝参数。在 `OnDraw()` 成员声明中使用 `override` 关键字可以确保编译器验证它是否正确重写了基类。

## 实现 CLine 类

你将 `CLine` 成员函数的实现放在由类向导创建的 `Line.cpp` 文件中。在该文件的 `stdafx.h` 文件使得标准系统头文件可用，`stdafx.h` 的内容是预编译的。你预计任何头文件都会包含 `stdafx.h`。现在你可以为 `Line.cpp` 添加 `CLine` 构造函数的基本代码。

## CLine 构造函数

构造函数的代码如下：

```
// CLine 类构造函数
CLine::CLine(const CPoint& start, const CPoint& end, COLORREF col) :
Element(start, color), m_EndPoint(end) {
```

通过调用 `Element` 构造函数来初始化继承的 `m_StartPoint` 和 `m_Color` 成员。省略第三个参数时，`m_EndPoint` 成员在构造函数的初始化列表中进行初始化。你还需要添加一些代码来完成此。

## 绘制线条

你用于绘制线条的 `CPen` 对所有元素都是相同的。你可以轻松地在 `CElement` 类中添加一个函数：

```
// 创建画笔
void CreatePen(CPen& apen)
{
    if(!apen.CreatePen(PS_SOLID, m_PenWidth, m_Color))
    {
        // 创建画笔失败
        AfxMessageBox("Pen creation failed.", MB_OK);
        AfxAbort();
    }
}
```

这仅适用于派生类，你可以将定义放在类的 `protected` 部分。在类定义中定义该函数将使其内联。调用 `CreatePen()` 为 `CPen` 创建画笔并将其附加到对象。你创建一个由 `m_PenWidth` 指定适当宽度的画笔，并确保创建成功。在极少数情况下，可能是内存耗尽，这是一个严重问题。这几乎是由程序错误引起的，所以你编写了调用 `AfxMessageBox()` 的函数，这是一个显示消息的全局函数，然后调用 `AfxAbort()` 终止程序。`AfxMessageBox()` 的第一个参数指定要显示的消息，然后调用 `AfxAbort()` 终止程序。（由于 OCR 重复模式导致文本已截断）

## 第 14 章 在窗口中绘制

```cpp
CRectangle(const CPoint& start, const CPoint& end, COLORREF color);
```

```cpp
protected:
    CPoint m_bottomRight; // 矩形的右下点
    CRectangle(void); // 默认构造函数 - 不应使用
```

无参数构造函数被设置为保护属性，以防止外部使用。矩形类的定义非常简单——仅包含一个构造函数、虚函数 `Draw()`，以及类中保护区域的无参数构造函数。

## CRectangle 构造函数

新的 `CRectangle` 类构造函数的代码比 `CLine` 稍微复杂一点：

```cpp
// CRectangle 构造函数
CRectangle::CRectangle (
    const CPoint& start, const CPoint& end, COLORREF color) :
    CElement(start, color)
{
    // 规范化矩形点
    m_StartPoint = CPoint(std::min(start.x, end.x), std::min(start.y, end.y));
    m_BottomRight = CPoint(std::max(start.x, end.x), std::max(start.y, end.y));
    // 确保点的宽度的高度至少为 2
    if(m_BottomRight.x - m_StartPoint.x < 2)
        m_BottomRight.x = m_StartPoint.x + 2;
    if(m_BottomRight.y - m_StartPoint.y < 2)
        m_BottomRight.y = m_StartPoint.y + 2;
    // 定义外接矩形
    m_EnclosingRect = CRect(m_StartPoint, m_BottomRight);
    m_EnclosingRect.Inflate(m_PenWidth, m_PenWidth);
}
```

初始化列表中调用 `CElement` 构造函数来获取初始颜色和画笔宽度。`CElement` 构造函数也会初始化 `m_StartPoint`，但它会被替换。你只能绘制宽度和高度至少为 2 的 `CRect` 对象，因此在安排好点定义了一个矩形区域后，必要时调整两个点的坐标。因为你已经调整了点，所以不需要调用 `NormalizeRect()`。`std::min()` 和 `std::max()` 是定义在 `algorithm` 头文件中的模板函数，分别返回参数的最小值和最大值。为 `Rectangle.cpp` 添加对 `algorithm` 头文件的 `#include` 指令。

> 警告 代码中 `std::min` 和 `std::max` 周围的括号是必要的。这在其他 C++ 编译器中并不典型，但是 Visual C++ 的一个特性。`windows.h` 头文件定义了 `min` 和 `max` 宏，如果没有括号，预处理器将在编译器启动之前对这些宏进行替换。这将导致编译器生成错误信息。括号可以防止预处理器宏替换。

## 绘制矩形

`CDC` 类的 `Rectangle()` 成员绘制一个矩形。该函数绘制一个封闭图形并用当前画刷进行填充。如果你想将矩形作为轮廓，只需为设备上下文选择一个 `NULL_BRUSH` 即可。需要的是，`CDC` 还有一个 `PolyLine()` 函数，它可以根据点数组绘制出由多个线段组成的形状。你也可以使用 `LineTo()` 来绘制矩形的四边，但简单的方法是使用 `Rectangle()` 函数：

```cpp
// 绘制一个 CRect 对象
void CRect::Draw(CDC* pDC)
{
    // 为此对象创建一个画笔并初始化
    CPen pen;
    CreatePen(pen);
    // 选择画笔和空画刷
    CPen* pOld = pDC->SelectObject(&pen);
```
