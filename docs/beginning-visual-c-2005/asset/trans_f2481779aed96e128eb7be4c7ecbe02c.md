
## 第14章

文件中可用的标准系统头文件的定义。如果你在代码中使用了任何由应用程序向导生成的类，可能需要为包含这些类定义的文件添加#include指令。

当然，由于类定义过程中没有使用类向导（ClassWizard），你必须手动将每个成员函数的定义添加到该文件中。现在可以准备将CLine类的构造函数添加到Elements.cpp文件中了。

```cpp
// CLine class constructor
CLine::CLine(CPoint Start, CPoint End, COLORREF aColor)
{
    m_StartPoint = Start;               // Set line start point
    m_EndPoint = End;                   // Set line end point
    m_Color = aColor;                   // Set line color
}
```

首先，将起点存储在从CElement类继承的m_StartPoint成员中。稍后，你将添加代码以允许移动元素，并使得只需改变起点即可移动直线，而终点必须相对于起点来定义。为此，你需要用End的x和y坐标值减去Start的x和y坐标值。x和y都是CPoint类的公共成员，因此可以直接引用它们。最后，将颜色存储在从CElement类继承的m_Color成员中。

CLine类的Draw()函数也不算太难，尽管你确实需要考虑绘制直线时使用的颜色：

```cpp
// Draw a CLine object
void CLine::Draw(CDC* pDC)
{
    // Create a pen for this object and
    // initialize it to the object color and line width of 1 pixel
    CPen aPen;
    if(!aPen.CreatePen(PS_SOLID, m_Pen, m_Color))
    {
        // Pen creation failed. Abort the program
        AfxMessageBox(_T("Pen creation failed drawing a line"), MB_OK);
        AfxAbort();
    }
    CPen* pOldPen = pDC->SelectObject(&aPen); // Select the pen
    // Now draw the line
    pDC->MoveTo(m_StartPoint);
    pDC->LineTo(m_EndPoint);
    // Restore the old pen
    pDC->SelectObject(pOldPen);
}
```

我将用于绘制形状的矩形称为“包围矩形”（enclosing rectangle），而将考虑画笔宽度的矩形称为“边界矩形”（bounding rectangle）以示区分。图14-17展示了带有包围矩形的形状，以及按线条粗细偏移后的边界矩形。这里显然进行了夸张处理，以便你能看清发生了什么。

在不同映射模式下计算边界矩形坐标的差异仅涉及y坐标；x坐标的计算在所有映射模式下都是相同的。要在MM_TEXT映射模式下获得边界矩形的角点，需要从定义矩形左上角的y坐标中减去线条粗细，并将其加到右下角的y坐标上。然而，在MM_LOENGLISH（以及所有其他映射模式）中，y轴沿相反方向增大，因此需要将线条粗细加到定义矩形左上角的y坐标上，并从右下角的y坐标中减去它。对于所有映射模式，都需要从定义矩形左上角的x坐标中减去线条粗细，并将其加到右下角的x坐标上。

为了在Sketcher中尽可能一致地实现元素类型，可以在基类的成员中为每个形状存储一个包围矩形。包围矩形需要在构造形状时计算。基类中GetBoundRect()函数的任务将是通过按画笔宽度偏移包围矩形来计算边界矩形。你可以通过添加两个数据成员来修改CElement类定义，如下所示：

```cpp
class CElement: public CObject
{
protected:
    COLORREF m_Color;                  // Color of an element
    CRect m_EnclosingRect;             // Rectangle enclosing an element
    int m_Pen;                         // Pen width

public:
    virtual ~CElement();               // Virtual destructor
    virtual void Draw(CDC* pDC) {}     // Virtual draw operation

    CRect GetBoundRect();              // Get the bounding rectangle for an element

protected:
    CElement();                        // Here to prevent it being called
};
```

你可以通过右键单击类名并从弹出菜单中选择“添加成员变量”来添加这些成员，也可以直接在编辑器窗口中连同注释一起添加语句。

你还必须更新CLine构造函数，使其具有正确的画笔宽度：

```cpp
// CLine class constructor
CLine::CLine(CPoint Start, CPoint End, COLORREF aColor)
{
    m_StartPoint = Start;              // Set line start point
    m_EndPoint = End;                  // Set line end point
    m_Color = aColor;                  // Set line color
    m_Pen = 1;                         // Set pen width
}
```

现在，假设使用`MM_TEXT`映射模式，你可以实现基类的`GetBoundRect()`成员：

```cpp
// Get the bounding rectangle for an element
CRect CElement::GetBoundRect()
{
    CRect BoundingRect;              // Object to store bounding rectangle
    BoundingRect = m_EnclosingRect;  // Store the enclosing rectangle

    // Increase the rectangle by the pen width
    BoundingRect.InflateRect(m_Pen, m_Pen);
    return BoundingRect;             // Return the bounding rectangle
}
```

这将返回任何派生类对象的边界矩形。你通过修改存储在基类数据成员中的包围矩形的坐标来定义边界矩形，使其四周按画笔宽度扩大，使用的是`CRect`类的`InflateRect()`方法。

`CRect`类为矩形提供了operator +运算符，你也可以使用它。例如，你可以在return之前将语句写成：

```cpp
BoundingRect = m_EnclosingRect + CRect(m_Pen, m_Pen, m_Pen, m_Pen);
```

同样，你也可以直接为构成矩形的每个x和y值加上（或减去）画笔宽度。你可以用以下语句替换赋值语句：

```cpp
BoundingRect = m_EnclosingRect;
BoundingRect.top -= m_Pen;
BoundingRect.left -= m_Pen;
BoundingRect.bottom += m_Pen;
BoundingRect.right += m_Pen;
```

> 提醒一下，CRect对象的各个数据成员是left和top（存储左上角的x和y坐标）以及right和bottom（存储右下角的坐标）。这些都是公共成员，因此你可以直接访问它们。一个常见的错误（尤其是我常犯的）是将坐标对写成(top,left)，而不是正确的顺序(left,top)。

这种方法与`InflateRect()`选项都存在一个隐患：它们内置了映射模式为`MM_TEXT`的假设，这意味着正y轴被假定为从上到下。如果更改映射模式，这两种方法都无法正常工作，尽管它们无法正常工作这一点并不明显。

### 规范化矩形

`InflateRect()`函数的工作方式是从矩形的top和left成员中减去你给定的值，并将这些值加到bottom和right上。这意味着，如果你不确保矩形是规范化的，你可能会发现矩形实际上在缩小。规范化矩形是指left值小于或等于right值，且top值小于或等于bottom值的矩形。你可以通过调用对象的`NormalizeRect()`成员来确保`CRect`对象是规范化的。大多数CRect成员函数都要求对象规范化后才能按预期工作，因此你需要确保在将包围矩形存储到`m_EnclosingRect`中时，它是规范化的。

### 计算直线的包围矩形

现在你只需要在直线的构造函数中添加代码来计算包围矩形：

```cpp
CLine::CLine(CPoint Start, CPoint End, COLORREF aColor)
{
    m_StartPoint = Start;                // Set line start point
    m_EndPoint = End;                    // Set line end point
    m_Color = aColor;                    // Set line color
    m_Pen = 1;                           // Set pen width

    // Define the enclosing rectangle
    m_EnclosingRect = CRect(Start, End);
    m_EnclosingRect.NormalizeRect();
}
```

你在这里使用的CRect构造函数的参数是直线的起点和终点。为了确保无论直线起点和终点的相对位置如何，边界矩形的top值都小于bottom值，你需要调用m_EnclosingRect对象的NormalizeRect()成员。

### CRectangle类

尽管你将使用与定义直线相同的数据（矩形对角线上的起点和终点）来定义矩形对象，但你不需要存储这些定义点。从基类继承的数据成员中的包围矩形完全定义了形状，因此你不需要任何数据成员。因此，你可以像这样定义该类：

```cpp
// Class defining a rectangle object
class CRectangle: public CElement
{
public:
    ~CRectangle(void);
    virtual void Draw(CDC* pDC);        // Function to display a rectangle

    // Constructor for a rectangle object
    CRectangle(CPoint Start, CPoint End, COLORREF aColor);

protected:
    CRectangle(void);                   // Default constructor - should not be used
};
```

无参构造函数现在被设为protected，以防止它被使用。矩形的定义变得非常简单——只需一个构造函数、虚Draw()函数，以及位于类protected部分的无参构造函数。

### CRectangle类构造函数

新的CRectangle类构造函数的代码与CLine构造函数的代码有些相似：

```cpp
// CRectangle class constructor
CRectangle::CRectangle(CPoint Start, CPoint End, COLORREF aColor)
{
```

