

## 创建文档并改进视图

```
CPoint m_FirstPoint;      // First point recorded for an element
CPoint m_SecondPoint;     // Second point recorded for an element
CElement* m_pTempElement; // Pointer to temporary element
CElement* m_pSelected;    // Currently selected element
BOOL m_MoveMode;          // Move element flag
CPoint m_CursorPos;       // Cursor position
CPoint m_FirstPos;        // Original position in a move

// Rest of the class as before...
};
```

这些也必须在 CSketcherView 的构造函数中进行初始化，因此将其修改为：

```
CSketcherView::CSketcherView()
: m_FirstPoint(CPoint(0,0))
, m_SecondPoint(CPoint(0,0))
, m_pTempElement(NULL)
, m_pSelected(NULL)
, m_MoveMode(FALSE)
, m_CursorPos(CPoint(0,0))
, m_FirstPos(CPoint(0,0))
{
    // TODO: add construction code here
}
```

元素移动过程始于从上下文菜单中选择 Move 菜单项。现在可以向 Move 菜单项的消息处理程序添加代码，以设置操作所需的条件：

```
void CSketcherView::OnElementMove()
{
    CClientDC aDC(this);
    OnPrepareDC(&aDC);          // Set up the device context
    GetCursorPos(&m_CursorPos); // Get cursor position in screen coords
    ScreenToClient(&m_CursorPos); // Convert to client coords
    aDC.DPtoLP(&m_CursorPos);   // Convert to logical
    m_FirstPos = m_CursorPos;   // Remember first position
    m_MoveMode = TRUE;          // Start move mode
}
```

在此处理程序中你做了四件事：

+   1. 获取当前光标位置的坐标，因为移动操作从此参考点开始。
+   2. 将光标位置转换为逻辑坐标，因为你的元素是在逻辑坐标中定义的。
+   3. 记住初始光标位置，以防用户以后想中止移动。
+   4. 将移动模式设为开启，作为 OnMouseMove() 处理程序识别的标志。

GetCursorPos() 函数是 Windows API 函数，它将当前光标位置存储在 m_CursorPos 中。注意你向此函数传递一个指针。光标位置以屏幕坐标表示（即相对于屏幕左上角的坐标）。所有与光标的操作都使用屏幕坐标。你想要逻辑坐标中的位置，因此必须分两步进行转换。ScreenToClient() 函数（视图类的继承成员）将屏幕坐标转换为客户端坐标，然后你对结果应用 aDC 对象的 DPtoLP() 成员函数以转换为逻辑坐标。

在将初始光标位置保存到 m_FirstPos 之后，将 m_MoveMode 设置为 TRUE，以便 OnMouseMove() 处理程序可以处理元素的移动。

现在你已设置了移动模式标志，是时候更新鼠标移动消息处理程序以处理元素的移动了。

### 修改 WM_MOUSEMOVE 处理程序

元素移动仅在移动模式开启且光标正在移动时发生。因此，在 OnMouseMove() 中你只需添加在 m_MoveMode 为 TRUE 时才执行的代码块来处理元素的移动。执行此操作的新代码如下：

```
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
    CClientDC aDC(this);                // DC is for this view
    OnPrepareDC(&aDC);                  // Get origin adjusted

    // If we are in move mode, move the selected element and return
    if(m_MoveMode)
    {
        aDC.DPtoLP(&point);             // Convert to logical coordinates
        MoveElement(aDC, point);        // Move the element
        return;
    }

    // Rest of the mouse move handler as before...
}
```

这项添加其实不需要太多解释，对吧？if 语句验证你是否处于移动模式，然后调用 MoveElement() 函数，该函数执行移动所需的操作。现在你只需实现此函数即可。

通过在类定义中的适当位置添加以下内容，将 MoveElement() 的声明作为 CSketcherView 类的 protected 成员添加：

```
void MoveElement(CClientDC& aDC, CPoint& point);  // Move an element
```

如往常一样，如果你愿意，也可以通过在 Class View 中右键单击类名来完成此操作。该函数需要访问封装视图设备上下文的对象 aDC 以及当前光标位置 point，因此两者都是引用参数。SketcherView.cpp 文件中函数的实现为：

## 创建文档并改进视图

```
void CSketcherView::MoveElement(CClientDC& aDC, CPoint& point)
{
    CSize Distance = point - m_CursorPos;    // Get move distance
    m_CursorPos = point;                    // Set current point as 1st for next time

    // If there is an element, selected, move it
    if(m_pSelected)
    {
        aDC.SetROP2(R2_NOTXORPEN);
        m_pSelected->Draw(&aDC,m_pSelected); // Draw the element to erase it
        m_pSelected->Move(Distance);         // Now move the element
        m_pSelected->Draw(&aDC,m_pSelected); // Draw the moved element
    }
}
```

要移动当前选中的元素的距离以 CSize 对象 Distance 的形式本地存储。CSize 类专门设计用于表示相对坐标位置，具有两个公共数据成员 cx 和 cy，对应于 x 和 y 增量。这些是通过当前光标位置 point 与上一次光标位置 m_CursorPos 保存的值之间的差值计算得出的。这使用了在 CPoint 类中重载的运算符 -。你在此处使用到的版本返回 CSize 对象，但也有返回 CPoint 对象的版本。你通常可以对 CSize 和 CPoint 对象组合操作。你将当前光标位置保存到 m_CursorPos 以便下次调用此函数时使用，这将在当前移动操作期间发生进一步的鼠标移动消息时发生。

你将使用 R2_NOTXORPEN 绘图模式在视图中实现元素的移动，因为它简单且快速。这与你在创建元素期间使用的一样。你以当前颜色（选中颜色）重绘选中的元素以将其重置为背景颜色，然后调用 Move() 函数将元素按 Distance 指定的距离重新定位。我们稍后会将此函数添加到元素类中。当元素自行移动后，你只需再次使用 Draw() 函数将其高亮显示在新位置。元素的颜色将在移动操作结束时恢复为正常，因为 OnLButtonUp() 处理程序将通过调用 UpdateAllViews() 正常重绘所有窗口。

### 让元素自行移动

将 Move() 函数作为基类 CElement 的虚成员添加。修改类定义为：

```
class CElement:public CObject
{
protected:
    COLORREF m_Color;          // Color of an element
    CRect m_EnclosingRect;     // Rectangle enclosing an element
    int m_Pen;                 // Pen width

public:
    virtual ~CElement(void);   // Virtual destructor

    // Virtual draw operation
    virtual void Draw(CDC* pDC, BOOL Select=FALSE){}
    virtual void Move(CSize& aSize){}  // Move an element
```

```
CRect GetBoundRect();        // Get the bounding rectangle for an element
protected:
    CElement(void);            // Here to prevent it being called
};
```

如前文关于 Draw() 成员所述，虽然此处 Move() 函数的实现没有任何意义，但由于序列化的要求，你不能将其设为纯虚函数。

现在你可以在从 CElement 派生的每个类的公共成员中添加 Move() 函数的声明。它们在每个类中都相同：

// Function to move an element
virtual void Move(CSize& aSize);
```

接下来你可以在 CLine 类中实现 Move() 函数：

```
void CLine::Move(CSize& aSize)
{
    m_StartPoint += aSize;        // Move the start point
    m_EndPoint += aSize;          // and the end point
    m_EnclosingRect += aSize;     // Move the enclosing rectangle
}
```

这很容易，因为 CPoint 和 CRect 类中重载了 += 运算符。它们都使用 CSize 对象，因此你只需将 aSize 指定的相对距离加到线的起点和终点以及包围矩形上。

移动 CRectangle 对象甚至更简单：

```
void CRectangle::Move(CSize& aSize)
{
    m_EnclosingRect+= aSize;      // Move the rectangle
}
```

因为矩形由 m_EnclosingRect 成员定义，所以移动它就足够了。

CCircle 类的 Move() 成员是相同的：

```
void CCircle::Move(CSize& aSize)
{
    m_EnclosingRect+= aSize;      // Move rectangle defining the circle
}
```

移动 CCurve 对象稍微复杂一些，因为它由任意数量的点定义。你可以按如下方式实现该函数：

```
void CCurve::Move(CSize& aSize)
{
    m_EnclosingRect += aSize;     // Move the rectangle

    // Get the 1st element position
```
