

## 存储和打印文档

已修改的文档。SetModifiedFlag() 函数的参数是 BOOL 类型的值，默认值为 TRUE。如果你需要指定文档未被修改，可以调用此函数并传入参数 FALSE，虽然这种情况很少见。

只有三种情况会更改文档对象：

-   调用 CSketcherDoc 的 AddElement() 成员来添加新元素时。
-   调用 CSketcherDoc 的 DeleteElement() 成员来删除元素时。
-   移动元素时。

这三种情况很容易处理。你只需要在这些操作涉及的每个函数中添加对 SetModifiedFlag() 的调用。AddElement() 的定义出现在 CSketcherDoc 类定义中。你可以将其扩展为：

```
void AddElement(CElement* pElement)      // Add an element to the list
{
    m_ElementList.AddTail(pElement);
    SetModifiedFlag();                  // Set the modified flag
}
```

你可以通过在类视图窗格中单击函数名称来转到 CSketcherDoc 中 DeleteElement() 的定义。你应该在其中添加一行，如下所示：

```
void CSketcherDoc::DeleteElement(CElement* pElement)
{
    if(pElement)
    {
        // If the element pointer is valid,
        // find the pointer in the list and delete it
        SetModifiedFlag();                 // Set the modified flag
        POSITION aPosition = m_ElementList.Find(pElement);
        m_ElementList.RemoveAt(aPosition);
        delete pElement;                   // Delete the element from the heap
    }
}
```

注意，只有在 pElement 不为空时才必须设置标志，所以你不能把函数调用随便放在任何地方。

在视图对象中，移动元素发生在 WM_MOUSEMOVE 消息的处理程序调用的 MoveElement() 成员中，但只有在按下鼠标左键时你才更改文档。如果单击了右键，元素会放回其原始位置，因此你只需要将对文档的 SetModifiedFlag() 函数的调用添加到 OnLButtonDown() 函数中，如下所示：

```
void CSketcherView::OnLButtonDown(UINT nFlags, CPoint point)
{
    CClientDC aDC(this);                 // Create a device context
    OnPrepareDC(&aDC);                   // Get origin adjusted
    aDC.DPtoLP(&point);                  // convert point to Logical

    if(m_MoveMode)
{
    // In moving mode, so drop the element
    m_MoveMode = FALSE;                  // Kill move mode
    m_pSelected = 0;                     // De-select element
    GetDocument()->UpdateAllViews(0);    // Redraw all the views
    GetDocument()->SetModifiedFlag();    // Set the modified flag
}
// Rest of the function as before...
}
```

你调用视图类继承的 GetDocument() 成员来获取指向文档对象的指针，然后使用该指针调用 SetModifiedFlag() 函数。现在，你更改文档的所有位置都已覆盖。

如果你构建并运行 Sketcher，修改文档或向其中添加元素，现在退出程序时会提示保存文档。当然，“文件 > 保存”菜单选项除了清除修改标志并将一个空文件保存到磁盘外，暂时不会执行任何操作。你必须实现序列化才能将文档正确写入磁盘，这是下一步。

## 序列化文档

第一步是实现 CSketcherDoc 类的 Serialize() 函数。在此函数中，你必须添加代码来序列化 CSketcherDoc 的数据成员。你在类中声明的数据成员如下：

```
class CSketcherDoc : public CDocument
{
protected: // create from serialization only
    CSketcherDoc();
    DECLARE_DYNCREATE(CSketcherDoc)

// Attributes
public:

protected:

    COLORREF m_Color;                                   // Current drawing color
    unsigned int m_Element;                             // Current element type
    CTypedPtrList<CObList, CElement*> m_ElementList;    // Element list
    int m_PenWidth;                                     // Current pen width
    CSize m_DocSize;                                    // Document size

    // Rest of the class...
};
```

注意，你目前不需要添加前面任何代码，因为这些代码已经存在了。只需要在类的 Serialize() 成员中插入用于存储和检索这五个数据成员的语句即可。你可以使用以下代码来完成：

```
void CSketcherDoc::Serialize(CArchive& ar)
{
    m_ElementList.Serialize(ar);        // Serialize the element list

    if (ar.IsStoring())
    {
        ar << m_Color                // Store the current color
           << m_Element             // the current element type,
           << m_PenWidth            // and the current pen width
           << m_DocSize;            // and the current document size
    }
    else
    {
        ar >> m_Color                // Retrieve the current color
           >> m_Element             // the current element type,
           >> m_PenWidth            // and the current pen width
           >> m_DocSize;            // and the current document size
    }
}
```

对于其中四个数据成员，你只需使用 CArchive 类中重载的提取和插入运算符。这对数据成员 m_Color 也适用，即使它的类型是 COLORREF，因为 COLORREF 类型与 long 类型相同。你不能对 m_ElementList 使用提取和插入运算符，因为该运算符不支持其类型，但只要 CTypedPtrList 类像你在 m_ElementList 的声明中那样，是使用 CObList 从集合类模板定义的，该类就会自动支持序列化。因此，你只需调用该对象的 Serialize() 函数即可。

你不需要将调用 m_ElementList 的 Serialize() 成员的语句放在 if-else 语句中，因为执行的操作类型由 CArchive 参数 ar 自动确定。调用 m_ElementList 的 Serialize() 成员的单个语句同时处理输入和输出。

这就是序列化文档类数据成员所需的全部内容，但序列化元素列表 m_ElementList 会导致调用元素类的 Serialize() 函数来存储和检索元素本身，因此你还需要为这些类实现序列化。

## 序列化元素类

所有形状类都是可序列化的，因为你从它们的基类 CElement 派生它们，而 CElement 又派生自 CObject。你选择 CObject 作为 CElement 的基类的唯一原因是为了获得序列化支持。现在，你可以通过向类定义和实现添加适当的宏，并在每个类的 Serialize() 函数成员中添加代码来序列化其数据成员，从而为每个形状类添加序列化支持。你可以从基类 CElement 开始，需要像下面这样修改其类定义：

```
class CElement: public CObject
{
    DECLARE_SERIAL(CElement)

protected:
```

```
COLORREF m_Color;              // Color of an element
CRect m_EnclosingRect;          // Rectangle enclosing an element
int m_Pen;                      // Pen width

public:
    virtual ~CElement(){}        // Virtual destructor

    // Virtual draw operation
    virtual void Draw(CDC* pDC, CElement* pElement=0){}
    virtual void Move(CSize& aSize){}    // Move an element
    CRect GetBoundRect();               // Get the bounding rectangle for an element

    virtual void Serialize(CArchive& ar);// Serialize function for the class

protected:
    CElement(void);                 // Here to prevent it being called
};
```

你添加了 DECLARE_SERIAL() 宏和虚函数 Serialize() 的声明。

你已经有了由应用程序向导创建的默认构造函数。你已将其在类中改为 protected，但它的访问说明符并不重要，只要它显式出现在类定义中即可。它可以是 public、protected 或 private，序列化仍然有效。但是，如果你忘记在类中包含默认构造函数，那么编译 IMPLEMENT_SERIAL() 宏时会出现错误消息。

你应该使用相关的类名作为参数，将 DECLARE_SERIAL() 宏添加到每个派生类 CLine、CRectangle、CCircle、CCurve 和 CText 中。你还应该为每个类添加 Serialize() 函数的声明作为其公共成员。

在文件 Elements.cpp 中，你必须在开头添加以下宏：

```
IMPLEMENT_SERIAL(CElement, CObject, VERSION_NUMBER)
```

你可以通过在 OurConstants.h 文件中添加以下行来定义常量 VERSION_NUMBER：

```
// Program version number for use in serialization
const UINT VERSION_NUMBER = 1;
```

然后，当你为其他形状类添加宏时，可以使用相同的常量。例如，对于 CLine 类，你应该添加该行：

```
IMPLEMENT_SERIAL(CLine, CElement, VERSION_NUMBER)
```

其他形状类也类似。当你修改任何与文档相关的类时，只需更改 OurConstants.h 文件中的 VERSION_NUMBER 定义，新的版本号就会应用到所有 Serialize() 函数中。如果你愿意，可以将所有 IMPLEMENT_SERIAL() 语句放在文件开头。完整集合是：

```
IMPLEMENT_SERIAL(CElement, CObject, VERSION_NUMBER)
IMPLEMENT_SERIAL(CLine, CElement, VERSION_NUMBER)
```

