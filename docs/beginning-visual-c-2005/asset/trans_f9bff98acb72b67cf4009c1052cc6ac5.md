

# 第 14 章

添加函数的规范，如图所示，然后单击 Finish 按钮。函数的声明将被添加到类定义中，并且你将被直接带到 `CSketcherView.cpp` 中的函数骨架。如果你在类定义中手动添加了声明，你需要将函数的完整定义添加到 `.cpp` 文件中。这就是：

```cpp
// Create an element of the current type
CElement* CSketcherView::CreateElement(void)
{
    // Get a pointer to the document for this view
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);                 // Verify the pointer is good

    // Now select the element using the type stored in the document
    switch(pDoc->GetElementType())
    {
        case RECTANGLE:
            return new CRectangle(m_FirstPoint, m_SecondPoint,
                                  pDoc->GetElementColor());

        case CIRCLE:
            return new CCircle(m_FirstPoint, m_SecondPoint,
                               pDoc->GetElementColor());

        case CURVE:
            return new CCurve(pDoc->GetElementColor());

        case LINE:
            return new CLine(m_FirstPoint, m_SecondPoint,
                             pDoc->GetElementColor());

        default:
            // Something's gone wrong
            AfxMessageBox(_T("Bad Element code"), MB_OK);
            AfxAbort();
            return NULL;
    }
}
```

未着色的行是如果使用 Add > Add Function 对话框将函数添加到类，则会自动提供的行。你在这里做的第一件事是通过调用 `GetDocument()` 获取文档指针，就像你以前见过的那样。为了安全起见，你使用 `ASSERT_VALID()` 宏来确保返回的是一个良好的指针。在应用程序的调试版本中使用的 MFC 调试版本中，此宏调用作为宏参数指定的对象的 `AssertValid()` 成员。这会检查当前对象的有效性，如果指针为 `NULL` 或对象以某种方式出现缺陷，则会显示错误消息。在 MFC 的发布版本中，`ASSERT_VALID()` 宏不执行任何操作。

switch 语句根据文档类中的函数返回的类型选择要创建的元素，`GetElementType()`。文档类中的另一个函数用于获取当前元素颜色。你可以直接将这两个函数的定义添加到 `CSketcherDoc` 类定义中，因为它们非常简单：

```cpp
class CSketcherDoc: public CDocument
{
    // Rest of the class definition as before...
    // Operations
public:
    unsigned int GetElementType()      // Get the element type
    { return m_Element; }
    COLORREF GetElementColor()         // Get the element color
    { return m_Color; }
    // Rest of the class definition as before...
};
```

每个函数都返回存储在相应数据成员中的值。记住，将成员函数定义放在类定义中相当于请求使函数内联，因此除了简单之外，这些函数还应该很快。

## 处理 WM_LBUTTONUP 消息

WM_LBUTTONUP 消息完成了创建元素的过程。此消息处理程序的工作是将创建的元素的最终版本传递给文档对象，然后清理视图对象数据成员。你可以以与之前相同的方式访问和编辑此处理程序的代码。向该函数添加以下行：

```cpp
void CSketcherView::OnLButtonUp(UINT nFlags, CPoint point)
{
    // Make sure there is an element
    if(m_pTempElement)
    {
        // Call a document class function to store the element
        // pointed to by m_pTempElement in the document object
        delete m_pTempElement;      // This code is temporary
        m_pTempElement = 0;         // Reset the element pointer
    }
}
```

if 语句在处理之前验证 m_pTempElement 不为零。用户完全有可能在不移动鼠标的情况下按下并释放鼠标左键，在这种情况下不会创建任何元素。只要有元素，元素指针就会传递给文档对象；你将在下一章中添加此代码的代码。在此期间，你只是在这里删除元素，以免污染堆。最后，m_pTempElement 指针被重置为 0，以便用户下次绘制元素时做好准备。

## 使用 Sketcher

在你可以使用鼠标消息处理程序运行示例之前，你必须更新 CSketcherView 类实现中的 OnDraw() 函数，以去掉之前添加的任何旧代码。

为了确保 OnDraw() 函数是干净的，请转到类视图并双击函数名称以转到 SketcherView.cpp 中的实现。删除你添加的任何旧代码，但保留向导提供的用于获取文档对象指针的前四行。你稍后需要它来访问存储在文档中的元素。函数的代码现在应该是：

```cpp
void CSketcherView::OnDraw(CDC* pDC)
{
    CSketcherDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc);
    if (!pDoc)
        return;
}
```

由于你目前文档中还没有元素，因此你现在不需要向此函数添加任何内容。当你在下一章开始在文档中存储数据时，你将添加代码以响应 WM_PAINT 消息绘制元素。如果没有它，元素在调整视图大小时就会消失，正如你将看到的那样。

## 运行示例

在确保已保存所有源文件后，构建程序。如果你在输入代码时没有犯任何错误，你将获得干净的编译和链接，因此你可以执行程序。你可以用程序支持的四种颜色中的任何一种绘制线条、圆圈和矩形。典型的窗口如图 14-20 所示。

![](img/2359b0c604600c58fba3539c738a356e_795_0.png)

图 14-20

尝试使用用户界面进行实验。请注意，你可以移动窗口，并且只要你不将其移动到超出应用程序窗口边界的位置，形状就会保留在窗口中。如果这样做，元素在移回后不会重新出现。这是因为现有元素从未被重绘。当客户端区域被覆盖和取消覆盖时，Windows 会向应用程序发送 WM_PAINT 消息，导致调用视图对象的 OnDraw() 成员。如你所知，视图的 OnDraw() 函数目前什么也不做。当你使用文档存储元素时，这将被修复。

当你调整视图窗口大小时，形状会立即消失，但当你移动整个视图时，它们会保留下来（只要它们不滑过应用程序窗口边界）。为什么？好吧，当你调整窗口大小时，Windows 会使整个客户端区域无效，并期望你的应用程序响应 WM_PAINT 消息重绘它。如果你移动视图，Windows 会负责重新定位客户端区域。你可以通过移动视图使形状部分被遮挡来演示这一点。当你将其滑回时，你仍然有一个部分形状，被遮挡的部分被擦除了。

如果你尝试在拖动光标超出客户端视图区域的同时绘制形状，你会注意到一些奇怪的效果。在视图窗口之外，你会丢失鼠标的跟踪，这往往会破坏橡皮筋机制。发生了什么？

## 捕获鼠标消息

问题是由 Windows 将鼠标消息发送到光标下的窗口引起的。一旦光标离开应用程序视图窗口的客户端区域，WM_MOUSEMOVE 消息就会被发送到其他地方。你可以通过使用 CSketcherView 类继承的某些成员来修复此问题。

视图类继承了一个函数 SetCapture()，你可以调用它来告诉 Windows 你希望你的视图窗口在你通过调用视图类中的另一个继承函数 ReleaseCapture() 另行说明之前获取所有鼠标消息。你可以在按下左按钮后立即捕获鼠标，通过修改 WM_LBUTTONDOWN 消息的处理程序：

```cpp
// Handler for left mouse button down message
void CSketcherView::OnLButtonDown(UINT nFlags, CPoint point)
{
    m_FirstPoint = point;        // Record the cursor position
    SetCapture();                // Capture subsequent mouse messages
}
```

现在你必须在 WM_LBUTTONUP 处理程序中调用 ReleaseCapture() 函数。如果你不这样做，只要你的程序继续运行，其他程序就无法接收任何鼠标消息。当然，你应该只在之前捕获了鼠标时才释放鼠标。视图类继承的 GetCapture() 函数返回捕获了鼠标的窗口的指针，这为你提供了一种判断是否已捕获鼠标消息的方法。你只需向 WM_LBUTTONUP 的处理程序添加以下内容：

```cpp
void CSketcherView::OnLButtonUp(UINT nFlags, CPoint point)
{
    if(this == GetCapture())
        ReleaseCapture();        // Stop capturing mouse messages

    // Make sure there is an element
```

