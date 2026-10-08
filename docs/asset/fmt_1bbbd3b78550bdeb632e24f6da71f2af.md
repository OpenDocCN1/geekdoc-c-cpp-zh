
```cpp
CheckDlgButton(IDC_PENWIDTHTH4,1);

break;

case 5:

CheckDlgButton(IDC_PENWIDTHTH5,1);

break;

default:

CheckDlgButton(IDC_PENWIDTHTH0,1);

}

return TRUE; // 除非设置控件焦点，否则返回 TRUE

// 异常：OCX属性页应返回 FALSE

}
```

你应该保留对基类函数的调用，因为对话框有一些必要的设置。`switch`语句根据`m_PenWidth`数据成员设置的值检查单选按钮。这意味着你需要在执行`DoModal()`之前安排为`m_PenWidth`设置适当的值，因为`DoModal()`函数会导致`WM_INITDIALOG`消息的发送，从而调用你的`OnInitDialog()`版本。

`CheckDlgButton`函数继承自`CWnd`。第一个参数标识按钮，第二个`UINT`参数检查其状态。如果是 1，则会勾选你在第一个参数中指定的按钮；如果是 0，则按钮未勾选。此函数可用于复选框和单选按钮。

## 处理单选按钮消息

对话框显示后，每当你点击单选按钮，就会生成并向应用程序发送消息。你可以为`CPDialog`类添加处理器来处理这些消息。回到你创建的对话框资源，依次点击每个单选按钮，并从菜单中选择“添加处理器”（Add Handler）来为`BN_CLICKED`消息创建处理器。图 16-5 显示了`IDC_PENWIDTH0`按钮的事件处理器对话框。注意我修改了处理器的名称，因为默认名称有些繁琐。

![](img/382e3fc55bbc8265)

图 16-5：具有`IDC_PENWIDTH0`按钮的事件处理器对话框。

# 782 | 第 16 节 与对话框和控件的交互

`CRectangle`构造函数实现了：

```cpp
CRectangle::CRectangle (const CPoint& start, const CPoint& end,
    COLORREF color, int penWidth);
    Element(start, color, penWidth)
{
    // 归一化矩形的定义点
    m_StartPoint = CPoint(std::min(start.x, end.x),
                         std::min(start.y, end.y));
    m_BottomRight = CPoint(std::max(start.x, end.x),
                         std::max(start.y, end.y));
    // 确保点的高宽至少为 2
    if((m_BottomRight.x - m_StartPoint.x) < 2)
        m_BottomRight.x = m_StartPoint.x + 2;
    if((m_BottomRight.y - m_StartPoint.y) < 2)
        m_BottomRight.y = m_StartPoint.y + 2;
    // 定义外围矩形
    m_EnclosingRect = CRect(m_StartPoint, m_BottomRight);
    int width(penWidth == 0 ? 1 : penWidth); // 矩形至少扩大 1 
    m_EnclosingRect.Inflate(width, width);
}
```

不要忘记在类定义处的构造函数声明以及其他元素类中添加`penWidth`参数。

`CCircle`构造函数的定义变为：

```cpp
CCircle::CCircle(const CPoint& start, const CPoint& end,
    COLORREF color, int penWidth);
    Element(start, color, penWidth)
{
    // 代码逻辑与之前相同...
    // 定义外围矩形
    m_EnclosingRect = CRect(m_StartPoint.x, m_StartPoint.y,
                         m_BottomRight.x, m_BottomRight.y);
    int width(penWidth == 0 ? 1 : penWidth); // 矩形至少扩大 1 
    m_EnclosingRect.Inflate(width, width);
}
```

你必须修改`CCerve`构造函数和`AddSegment`成员。以下是修改后的构造函数定义：

```cpp
CCCurve::CCCurve(const CPoint& first, const CPoint& second,
    COLORREF color, int penWidth);
    Element(first, color, penWidth)
{
    // 将第二个点存储在 vector 中
    m_Points.push_back(second);
    m_EnclosingRect = CRect(
        (std::min)(first.x, second.x),
        (std::min)(first.y, second.y),
        (std::max)(first.x, second.x),
        (std::max)(first.y, second.y));
    int width = penWidth == 0 ? 1 : penWidth; // 矩形至少扩大 1
    m_EnclosingRect.InflateRect(width, width);
}
```

`AddSegment()`成员实现应更改为：

```cpp
void CCCurve::AddSegment(const CPoint& point)
{
    m_Points.push_back(point);
    // 将点添加到末尾
    // 为新点修改外围矩形
    int width(m_PenWidth == 0 ? 1 : m_PenWidth); // 矩形至少缩小 1
    m_EnclosingRect.DeflateRect(width, width);
    m_EnclosingRect = CRect((std::min)(point.x, m_EnclosingRect.left),
                             (std::min)(point.y, m_EnclosingRect.top),
                             (std::max)(point.x, m_EnclosingRect.right),
                             (std::max)(point.y, m_EnclosingRect.bottom));
    m_EnclosingRect.InflateRect(width, width);
}
```

这些类已经处理完毕。现在你必须修改 Sketcher 的其余部分以使用新的元素构造函数。

# 在视图中创建元素

你需要做的的最后一个更改是`CSketcherView`的`CreateElement()`成员。因为你为所有形状的构造函数都添加了`penWidth`作为参数，你必须更新构造函数以反映这一点。将`CSketcherView::CreateElement()`的定义更改如下内容：

```cpp
CElement* CSketcherView::CreateElement() const
{
    // 获取此视图对应的文档指针
    CSketchDoc* pDoc = GetDocument();
    ASSERT_VALID(pDoc); // 验证指针有效
    // 获取当前元素的颜色
    COLORREF color = static_cast<COLORREF>(pDoc->GetElementColor());
    int penWidth = pDoc->GetPenWidth(); // 获取当前画笔宽度
    // 现在使用文档中存储的类型选择元素
    switch(pDoc->ElementType())
    {
        case ElementType::RECTANGLE:
            return new CRect(m_FirstPoint, m_SecondPoint, color, penWidth);
        case ElementType::CIRCLE:
            return new CCircle(m_FirstPoint, m_SecondPoint,
                              color, penWidth);
        case ElementType::CURVE:
            return new CCCurve(m_FirstPoint, m_SecondPoint,
                              color, penWidth);
        case ElementType::LINE:
            return new CLine(m_FirstPoint, m_SecondPoint,
                              color, penWidth);
        default:
            // 出现错误
            AfxMessageBox("Bad Element"), MB_OK);
            AfxAbort();
            return nullptr;
    }
}
```
