

## 创建文档并改进视图

```cpp
m_pTempElement->Draw(&aDC);    // Now draw it
return;                         // We are done
}

aDC.SetROP2(R2_NOTXORPEN);      // Set drawing mode
// Redraw the old element so it disappears from the view
m_pTempElement->Draw(&aDC);
delete m_pTempElement;           // Delete the old element
m_pTempElement = 0;             // Reset the pointer to 0
}

// Create a temporary element of the type and color that
// is recorded in the document object, and draw it
m_pTempElement = CreateElement();  // Create a new element
m_pTempElement->Draw(&aDC);        // Draw the element
}
else
{ // We are not drawing an element so do highlighting...
    CSketcherDoc* pDoc = GetDocument();  // Get a pointer to the document
    CElement* pElement = 0;              // Store an element pointer
    CRect aRect(0,0,0,0);                // Store a rectangle
    POSITION aPos = pDoc->GetListHeadPosition();  // Get first element posn
    CElement* pOldSelection = m_pSelected;        // Save old selected element
    m_pSelected = 0;
    while(aPos)                        // Iterate through the list
    {
        pElement = pDoc->GetNext(aPos);
        aRect = pElement->GetBoundRect();
        aDC.LPtoDP(aRect);
        aRect.NormalizeRect();

        // Select the first element that appears under the cursor
        if(aRect.PtInRect(point))
        {
            m_pSelected = pElement;
            break;
        }
    }
    if(m_pSelected == pOldSelection)  // If new selection is same as old
        return;                        // we are done

    // Unhighlight old selection if there is one
    if(pOldSelection != 0)             // Verify there is one
    {
        aRect = pOldSelection->GetBoundRect();
        aDC.LPtoDP(aRect);             // Convert to device coords
        aRect.NormalizeRect();         // Normalize
        InvalidateRect(aRect, FALSE);  // Invalidate area
    }

    // Highlight new selection if there is one
    if(m_pSelected != 0)               // Verify there is one
    {
        aRect = m_pSelected->GetBoundRect();
        aDC.LPtoDP(aRect);             // Convert to device coords
        aRect.NormalizeRect();         // Normalize
        InvalidateRect(aRect, FALSE);  // Invalidate area
    }
}
```

你只需要在创建新元素的过程中不进行高亮元素处理。所有高亮代码都可以添加到主 if 语句的新 else 子句中。这涉及将你之前用来确定光标下元素的代码移动到新的 else 子句中并进行添加。

你必须跟踪任何先前被高亮的元素，因为如果有新的元素，就必须取消高亮旧元素。为此，你将 m_pSelected 的值保存在 pOldSelection 中。然后搜索光标下的元素，如果有，就将其地址存储在 m_pSelected 中。

如果 pOldSelection 和 m_pSelected 相等，则它们要么都包含同一元素的地址，要么都为零。如果它们相同且非零，则已高亮的元素应保持高亮，因此无需执行任何操作。如果它们都为零，则没有元素被高亮，也不需要高亮，在这种情况下也无需执行任何操作。无论哪种情况，你只需从函数返回即可。如果它们不同，则可能需要对两者进行操作。

如果 pOldSelection 不为空，则必须取消高亮旧元素。机制与之前相同（获取设备坐标中的边界矩形并将其传递给设备上下文的 InvalidateRect() 函数）。然后你检查 m_pSelected，如果它不为空，则需要高亮其地址所包含的元素。这同样涉及获取设备坐标中的边界矩形并将其传递给 InvalidateRect() 函数。

### 绘制高亮元素

你仍然需要安排高亮元素实际以高亮方式绘制。某个地方必须将 m_pSelected 指针传递给每个元素的绘制函数。唯一可以执行此操作的地方是在视图中的 OnDraw() 函数中：

```cpp
void CSketcherView::OnDraw(CDC* pDC)
{
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    if(!pDoc)
        return;

    POSITION aPos = pDoc->GetListHeadPosition();
    CElement* pElement = 0;          // Store for an element pointer
    while(aPos)                      // Loop while aPos is not null
    {
        pElement = pDoc->GetNext(aPos);  // Get the current element pointer
        // If the element is visible...
        if(pDC->RectVisible(pElement->GetBoundRect()))
            pElement->Draw(pDC, m_pSelected);// ...draw it
    }
}
```

你只需要更改一行。元素的 Draw() 函数添加了第二个参数来传达要高亮元素的地址。

### 测试高亮

这就是使高亮始终有效所需的所有内容。它并不简单，但也不算特别困难。你可以构建并执行 Sketcher 来尝试它。只要光标下有元素，该元素就会以洋红色绘制。这使得在右键单击鼠标之前很明显上下文菜单将作用于哪个元素，并且你事先就知道显示的是哪个上下文菜单。

### 处理菜单消息

下一步是在你之前添加的 Move 和 Delete 菜单项的处理程序体中提供代码。你可以先添加 Delete 的代码，因为那是两者中更简单的。

#### 删除元素

在 CSketcherView 类的 OnElementDelete() 处理程序中删除当前选定元素的代码很简单：

```cpp
void CSketcherView::OnElementDelete()
{
    if(m_pSelected)
    {
        CSketcherDoc* pDoc = GetDocument();// Get the document pointer
        pDoc->DeleteElement(m_pSelected);    // Delete the element
        pDoc->UpdateAllViews(0);             // Redraw all the views
        m_pSelected = 0;                     // Reset selected element ptr
    }
}
```

只有当 m_pSelected 包含有效地址时，才会执行删除元素的代码，表示有元素需要删除。你获取文档指针并调用文档对象的 DeleteElement() 函数；你将在稍后将此成员添加到 CSketcherDoc 类中。当元素已从文档中移除后，你调用 UpdateAllViews() 以在没有已删除元素的视图中重绘所有视图。最后，你将 m_pSelected 设置为零以表示没有元素被选中。

你可以将 DeleteElement() 声明为 CSketcherDoc 类的公共成员：

```cpp
class CSketcherDoc : public CDocument
{
protected: // create from serialization only
    CSketcherDoc();
    DECLARE_DYNCREATE(CSketcherDoc)

// Attributes
public:

// Operations

public:
    void DeleteElement(CElement* pElement); // Delete an element
    unsigned int GetElementType()
        { return m_Element; }    // Get the element type

// Rest of the class as before...
};
```

它接受要删除的元素的指针作为参数且不返回任何内容。你可以在 SketcherDoc.cpp 中实现它，如下所示：

```cpp
void CSketcherDoc::DeleteElement(CElement* pElement)
{
    if(pElement)
    {
        // If the element pointer is valid,
        // find the pointer in the list and delete it
        POSITION aPosition = m_ElementList.Find(pElement);
        m_ElementList.RemoveAt(aPosition);
        delete pElement;                // Delete the element from the heap
    }
}
```

你不应该对它的工作原理有任何疑问。在确保你有一个非空指针后，你使用列表对象的 Find() 成员查找列表中指针的 POSITION 值。你使用它与 RemoveAt() 成员一起从列表中删除指针，然后从堆中删除参数 pElement 指向的元素。

这就是你需要删除元素的所有内容。现在你应该有一个 Sketcher 程序，可以在多个滚动视图中绘制，并从任何视图中删除草图中的任何元素。

#### 移动元素

移动选定元素稍微复杂一些。由于元素必须随鼠标光标一起移动，因此你必须在 OnMouseMove() 方法中添加代码来处理此行为。由于此函数也用于绘制元素，因此你需要一种机制来指示何时处于“移动”模式。最简单的方法是在视图类中设置一个标志，可以称为 m_MoveMode。如果将其设为 BOOL 类型，则使用 TRUE 表示移动模式开启，使用 FALSE 表示关闭。当然，你也可以将其定义为基本类型 bool，值分别为 true 和 false。

你还必须在移动过程中跟踪光标，因此可以在视图中添加另一个数据类型成员。可以将其称为 m_CursorPos，其类型为 CPoint。另一个需要提供的是中止移动的可能性。为此，你必须记住移动操作开始时光标的第一个位置，以便在必要时将元素移回。这是一个类型为 CPoint 的另一个成员，称为 m_FirstPos。将这三个新成员添加到视图类的 protected 部分：

```cpp
class CSketcherView: public CScrollView
{
    // Rest of the class as before...

protected:
```

