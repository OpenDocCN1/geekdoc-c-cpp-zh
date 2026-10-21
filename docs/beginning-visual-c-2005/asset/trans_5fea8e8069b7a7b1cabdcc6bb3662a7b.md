
# 创建文档并改进视图

使用`MF_BYCOMMAND`，您就不必担心菜单项在弹出菜单中出现的顺序，甚至不必担心它们出现在哪个子菜单中。

用于勾选或取消勾选菜单项的可用标志值分别是`MF_CHECKED`和`MF_UNCHECKED`。

对于第二个上下文弹出菜单中的所有菜单项，勾选或取消勾选菜单项的代码本质上是相同的。下面看看如何正确设置`Black`菜单项的勾选状态。`CheckMenuItem()`函数的第一个参数是菜单ID，即`ID_COLOR_BLACK`。第二个参数是`MF_BYCOMMAND`与`MF_CHECKED`或`MF_UNCHECKED`的组合，具体取决于当前选择的颜色。您可以使用`GetElementColor()`函数从文档中获取当前颜色，语句如下：

```
COLORREF Color = GetDocument()->GetElementColor();
```

您可以使用`Color`变量通过条件运算符选择适当的标志，然后将结果与`MF_BYCOMMAND`标志组合，得到`CheckMenuItem()`函数的第二个参数。因此，设置该菜单项勾选状态的语句如下：

```
menu.CheckMenuItem(ID_COLOR_BLACK,
    (BLACK==Color?MF_CHECKED:MF_UNCHECKED) | MF_BYCOMMAND);
```

这里无需指定子菜单，因为菜单项在菜单中由其ID唯一确定。您只需更改此语句中的ID和颜色值，即可得到为其他颜色菜单项设置标志的语句。

为元素菜单项设置勾选状态本质上也是一样的。要勾选`Line`菜单项，您可以编写：

```
unsigned int ElementType = GetDocument()->GetElementType();
menu.CheckMenuItem(ID_ELEMENT_LINE,
    (LINE==ElementType?MF_CHECKED:MF_UNCHECKED) | MF_BYCOMMAND);
```

`OnContextMenu()`处理程序的完整代码如下：

```
void CSketcherView::OnContextMenu(CWnd* pWnd, CPoint point)
{
    CMenu menu;
    menu.LoadMenu(IDR_CURSOR_MENU);

    // Set check marks if it's the no element menu
    if(m_pSelected == 0)
    {
        // Check color menu items
        COLORREF Color = GetDocument()->GetElementColor();
        menu.CheckMenuItem(ID_COLOR_BLACK,
            (BLACK==Color?MF_CHECKED:MF_UNCHECKED) | MF_BYCOMMAND);
        menu.CheckMenuItem(ID_COLOR_RED,
            (RED==Color?MF_CHECKED:MF_UNCHECKED) | MF_BYCOMMAND);
        menu.CheckMenuItem(ID_COLOR_GREEN,
            (GREEN==Color?MF_CHECKED:MF_UNCHECKED) | MF_BYCOMMAND);
        menu.CheckMenuItem(ID_COLOR_BLUE,
            (BLUE==Color?MF_CHECKED:MF_UNCHECKED) | MF_BYCOMMAND);
        // Check element menu items
        unsigned int ElementType = GetDocument()->GetElementType();
        menu.CheckMenuItem(ID_ELEMENT_LINE,
                           (LINE==ElementType?MF_CHECKED:MF_UNCHECKED)|MF_BYCOMMAND);
        menu.CheckMenuItem(ID_ELEMENT_RECTANGLE,
                           (RECTANGLE==ElementType?MF_CHECKED:MF_UNCHECKED)|MF_BYCOMMAND);
        menu.CheckMenuItem(ID_ELEMENT_CIRCLE,
                           (CIRCLE==ElementType?MF_CHECKED:MF_UNCHECKED)|MF_BYCOMMAND);
        menu.CheckMenuItem(ID_ELEMENT_CURVE,
                           (CURVE==ElementType?MF_CHECKED:MF_UNCHECKED)|MF_BYCOMMAND);
    }
    CMenu* pPopup = menu.GetSubMenu(m_pSelected == 0 ? 1 : 0);
    ASSERT(pPopup != NULL);
    pPopup->TrackPopupMenu(TPM_LEFTALIGN | TPM_RIGHTBUTTON, point.x, point.y, this);
}
```

完成此修改后，重新构建并运行Sketcher时，上下文菜单项应能正确显示勾选状态。

# 突出显示元素

理想情况下，用户希望在右键单击获取上下文菜单之前知道光标下是哪个元素。当您要删除一个元素时，您需要知道正在操作哪个元素。同样，当您想使用另一个上下文菜单（例如更改颜色）时，您需要确保光标下方没有元素。为了准确显示光标下是哪个元素，您需要在发生右键单击之前以某种方式对其进行突出显示。

您可以在元素的`Draw()`成员函数中实现这一点。您需要做的就是向`Draw()`函数传递一个参数来指示元素何时应该被突出显示。如果将视图的`m_pSelected`成员中保存的当前选中元素的地址传递给`Draw()`函数，就能将其与`this`指针进行比较，以判断它是否是当前元素。

所有元素的突出显示方式都是相同的，因此以`CLine`成员为例。您可以向其他元素类型的每个类添加类似的代码。在开始修改`CLine`之前，必须首先修改基类`CElement`的定义：

```
class CElement : public CObject
{
protected:
    COLORREF m_Color;                  // Color of an element
    CRect m_EnclosingRect;             // Rectangle enclosing an element
    int m_Pen;                         // Pen width

public:
    virtual ~CElement(void);
    // Virtual draw operation
    virtual void Draw(CDC* pDC,CElement* pElement=0) { }

    CRect GetBoundRect();              // Get the bounding rectangle for an element

protected:
    CElement(void);                    // Here to prevent it being called
};
```

# 创建文档并改进视图

这一改动是向虚函数`Draw()`添加第二个参数，它是指向元素的指针。将第二个参数初始化为零的原因是为了允许该函数仅使用一个参数调用；第二个参数将默认提供为0。

您需要以完全相同的方式修改从`CElement`派生的每个类中`Draw()`函数的声明。例如，您应将`CLine`类的定义改为：

```
class CLine :
    public CElement
{
    public:
        ~CLine(void);
        // Function to display a line
        virtual void Draw(CDC* pDC, CElement* pElement=0);

        // Constructor for a line object
        CLine(CPoint Start, CPoint End, COLORREF aColor);

    protected:
        CPoint m_StartPoint;              // Start point of line
        CPoint m_EndPoint;                // End point of line

        CLine(void);                      // Default constructor - should not be used
};
```

从`CElement`派生的各个类的`Draw()`函数实现都需要以相同方式进行扩展。`CLine`类的函数如下：

```
void CLine::Draw(CDC* pDC, CElement* pElement)
{
    // Create a pen for this object and
    // initialize it to the object color and line width of 1 pixel
    CPen aPen;
    COLORREF aColor = m_Color;             // Initialize with element color
    if(this == pElement)                    // This element selected?
        aColor = SELECT_COLOR;             // Set highlight color
    if(!aPen.CreatePen(PS_SOLID, m_Pen, aColor))
    {
        // Pen creation failed. Abort the program
        AfxMessageBox(_T("Pen creation failed drawing a line"), MB_OK);
        AfxAbort();
    }

    CPen* pOldPen = pDC->SelectObject(&aPen);  // Select the pen

    // Now draw the line
    pDC->MoveTo(m_StartPoint);
    pDC->LineTo(m_EndPoint);

    pDC->SelectObject(pOldPen);              // Restore the old pen
}
```

# 第15章

这是一个非常简单的改动。您将新的局部变量`aColor`设置为存储在`m_Color`中的当前颜色，当`pElement`等于`this`时（即当前元素与选中元素相同的情况），`if`语句会将`aColor`的值重置为`SELECT_COLOR`。您还需要将`SELECT_COLOR`的定义添加到`OurConstants.h`文件中：

```
//Definitions of constants
#pragma once

// Element type definitions
// Each type value must be unique
const unsigned int LINE = 101U;
const unsigned int RECTANGLE = 102U;
const unsigned int CIRCLE = 103U;
const unsigned int CURVE = 104U;

// Color values for drawing
const COLORREF BLACK = RGB(0,0,0);
const COLORREF RED = RGB(255,0,0);
const COLORREF GREEN = RGB(0,255,0);
const COLORREF BLUE = RGB(0,0,255);
const COLORREF SELECT_COLOR = RGB(255,0,180);
```

现在，您应该在`CElements.cpp`文件中添加一条针对`OurConstants.h`的`#include`指令，以使`SELECT_COLOR`的定义可用。至此，突出显示功能已基本实现。`CElement`类的派生类如今能够以选中状态绘制自身——您只需要一种机制来实现元素的选择。那么应该在何处实现呢？您是在`CSketcherView`类的`OnMouse()`处理程序中确定光标下是否有元素，因此这显然是着手实现突出显示的地方。

对`OnMouseMove()`处理程序的修改如下：

```
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
// Define a Device Context object for the view
CCilentDC aDC(this); // DC is for this view
OnPrepareDC(&aDC); // Get origin adjusted
aDC.SetROP2(R2_NOTXORPEN); // Set the drawing mode
if((nFlags&MK_LBUTTON) && (this==GetCapture()))
{
aDC.DPtoLP(&point); // convert point to Logical
m_SecondPoint = point; // Save the current cursor position
if(m_pTempElement)
{
if(CURVE == GetDocument()->GetElementType()) // Is it a curve?
{
// We are drawing a curve
// so add a segment to the existing curve
static_cast<CCurve*>(m_pTempElement)->AddSegment(m_SecondPoint);
}
}
}
```

