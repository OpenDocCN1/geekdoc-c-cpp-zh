
生成的代码不是粗体。这里有一个对基类 `OnCreate()` 的调用，它负责视图窗口的定义。这一点是，你不要删除此函数调用；否则窗口将不会创建。

为 `CStatusBar` 对象调用 `Create()` 函数会创建状态栏。你将当前 `CChildFrame` 对象的指针传递给 `Create` 函数，以建立连接。定义状态栏和窗口之间格的指示器通常定义为 `UINT` 元素数组。在这里，你将指示器定义为一个数组，并用分隔符 ID 和你的状态栏 ID 进行初始化。当你想向状态栏添加更多窗格时，可以在指示器数组之间包含 `ID_SEPARATOR` 符号来分隔。你调用状态栏对象的 `SetIndicators()` 函数，并将 `indicators` 的地址作为第一个参数，并将数组元素的个数作为第二个参数。这会在状态栏右侧创建一个窗格。

当第一个窗格是 `ID_SEPARATOR` 时，它会自动拉伸以对齐状态栏中的后续窗格。你可以通过指示器数组中的索引引用窗格，并调用 `SetPaneStyle()` 来设置窗格样式。`SetPaneStyle()` 的第一个参数是窗格索引，第二个是指定要设置的样式或样式的 `UINT` 值。只有一个窗格可以拥有 `SBPS_STRETCH` 样式，该样式会将窗格拉伸以填充状态栏中的可用空间。你还可以为窗格设置其他样式有：

| 样式 | 说明 |
| --- | --- |
| `SBPS_NORMAL` | 未设置描边、边框或弹出样式。 |
| `SBPS_POPUP` | 边框反转，使文本弹出。 |
| `SBPS_NOBORDERS` | 无 3D 边框。 |
| `SBPS_DISABLED` | 窗格内不绘制文本。 |

# 第 16 章 使用对话框和控件

当你想要为一个窗格设置多个样式时，只需使用逻辑或（OR）操作将样式组合在一起即可。

## 更新状态栏

如果你编译并运行代码，状态栏会出现，但它们只显示比例因子为 1，无论实际的比例因子是多少——这并不很有用。这是因为没有更新状态栏的机制。你需要在某处添加代码，以便每次选择比例时都更改状态栏中的文本。显而易见的地方是 `ContentView` 类，因为当前比例记录在那里。

你可以通过添加与该窗格指示器符号关联的 `UPDATE_COMMAND_UI` 来更新状态栏中的窗格。在类视图中右键点击 `ContentView`，从弹出菜单中选择“类向导”。你会看到 MFC 类向导对话框。如你所见，这允许你在类中创建和编辑大量的函数，并提供了访问任何类成员的替代方案。

如果尚未选择，选择对话框中的“命令”（Commands）选项卡：这允许你向类添加命令处理器。在“对象 ID”（Object IDs）中选择 `ID_INDICATOR_SCALE`；这标识了你要更新的状态栏。然后在“消息”（Messages）格中选择 `UPDATE_COMMAND_UI`。对话框应该看起来如图 16-12。

![](img/80f387749861c6bfa7acfcf4c2583ff5_841_0.png)

图 16-12

点击“添加处理器”（Add Handler）按钮将命令处理器添加到类中。将显示另一个对话框，让你有机会将处理器函数更改为 `OnUpdateScale`，这比默认的简洁一点。然后你可以点击 OK 关闭对话框，再次点击 OK 关闭 MFC 类向导对话框。

你只需要完成已添加处理器的定义，因此请将以下代码添加到 `SketcherView.cpp` 中的函数中。

```cpp
void SketcherView::OnUpdateScale(CCmdUI *pcmdUI)
{
    pcmdUI->Enable();
    CString scaleString;
    scaleString.Format(_T("View Scale: %d"), m_Scale);
    pcmdUI->SetText(scaleString);
}
```

参数是指向 `CCmdUI` 对象的指针，该对象将状态栏作为命令目标进行封装。你创建一个 `CString` 对象并调用其 `Format()` 函数来生成要显示的文本字符串。`Format()` 的第一个参数是格式字符串，你可以在其中嵌入后续参数的格式占位符。嵌入占位符的格式字符串与 C 函数 `printf()` 相同。随后的每个参数都会转换为相应的格式。`%d` 占位符会将 `m_Scale` 转换为十进制字符串。`%f` 可用于浮点值，`%s` 用于字符串值。调用 `SetText()` 用于 `CCmdUI` 对象可以设置窗格文本。`Enable()` 用于 `CCmdUI` 对象会导致窗格正常显示，因为 BOOL 参数默认为 `TRUE`。显式传递 `FALSE` 会使窗格变灰。这就是状态栏所需的所有。如果你再次构建 Sketcher，你应该拥有具有不同比例的每个视图的可滚动窗口。

## CString 类

你在上一节使用了 `CString` 对象，但它远比你所看到的更多。`CString` 类提供了一种方便易用的字符串处理机制，可以用于任何需要字符串的地方。准确地说，你可以用 `CString` 对象代替 `const char*` 或 `LPCTSTR` 类型，这些类型出现在 Windows API 函数中。如果你在使用 DDX 机制，则必须使用 `CString`。

`CString` 类提供了下表所示的重载运算符。

| 运算符 | 用法 |
| --- | --- |
| `=` | 将一个字符串拷贝到另一个，例如：<br>`str1 = str2;`<br>`str1 = _T("A normal string");` |
| `+` | 连接两个或多个字符串，例如：<br>`str1 = str2 + str3 + _T("* more");` |
| `+=` | 将字符串追加到现有的 `CString` 对象中，例如：<br>`str1 += str2;` |
| `==` | 比较两个字符串的相等性，例如：<br>`if(str1 == str2) // 执行...` |
| `<` | 测试一个字符串是否小于另一个。 |
| `<=` | 测试一个字符串是否小于等于另一个。 |
| `>` | 测试一个字符串是否大于另一个。 |
| `>=` | 测试一个字符串是否大于等于另一个。 |

表中变量 `str1` 和 `str2` 是 `CString` 对象。
`CString` 对象会根据需要增长，因此当你向现有对象末尾添加额外的字符串时。例如：

```cpp
CString str = _T("A fool and your money");
str += _T("are soon partners.");
```

## 使用编辑框控件

编辑框控件用于管理应用程序中的文本。你将使用编辑框控件为 Sketch 添加注释。你需要一个新的封装文本字符串的 Sketch 类型 `CText`，以及一个为元素设置 TEXT 模式的菜单项。因为文本只需要一个引用点，你可以在视图类的 `OnButtonClick()` 处理器中创建它。你还需要在元素添加一个新项来设置 TEXT。你将按照以下顺序为 Sketcher 添加此功能：

1. 创建一个带有编辑框控件的对话框资源及其关联类。
2. 添加新的菜单项。
3. 添加用于为 `CText` 元素打开对话框的代码。
4. 添加对创建 `CText` 元素的支持。

### 创建编辑框资源

在资源视图（Resource View）中，右键点击对话框文件夹并选择插入对话框（Insert Dialog），创建一个新的对话框资源。将新对话框的 ID 更改为 `ID_TEXT_DLG`，并将对话框的 Caption 属性设置为 Enter True。

要添加编辑框，从工具箱中选择编辑控件（Edit Control）图标，点击对话框中你想放置的位置。你可以通过拖动边界来调整编辑控件的大小，通过拖动整个控件更改其在对话框中的位置。右键点击它并从弹出菜单中选择属性（Properties），可以显示编辑框的属性。你可以先将其 ID 更改为 `IDC_EDIT_TEXT`，如图 16-13 所示。

此时控件的一些属性值得关注。首先，选择“多行”（Multiline）属性。将值设置为 True 会创建一个多行编辑框，文本可以跨越多行。“对齐”（Align）属性决定了文本在多行编辑框中的位置。此处值为 Left（左），但你也有 Center（中）和 Right（右）选项。

如果你想将“返回”（Return）属性更改为 True，在控件中输入文本时按键盘的回车键会在字符串中插入一个字符。如果你想将字符串拆分为多行显示，这允许你分析该字符串。如果你不需要这种效果，请将属性值保留为 False。在这种情况下，选择默认控件（即 OK 按钮）后按回车键将关闭对话框。

![](img/80f387749861c6bfa7acfcf4c2583ff5_844_0.png)

| Name | `IDC_EDIT_TEXT` (Edit Control) |
| --- | --- |
| Accept Focus | False |
| Align Text | Left |
| AutoScroll | False |
| Auto VScroll | True |
| Border | True |
| Client Edge | False |
| Disabled | False |
| Group | False |
| Help ID | False |
| Horizontal Scroll | False |
| ID | `IDC_EDIT_TEXT` |
| Left Scroll | False |
| Lowercase | False |
| Modal Frame | False |
| Multiline | True |
| No SelectSelect | False |
| Number | False |
| OEM Convert | False |
| Password | False |
| Read Only | False |
| Right Align Text | False |
| Right To Left False | False |
| Static Edge | False |
| Tabstop | True |
| Transparent | False |
| Uppercase | False |
| Vertical Scroll | False |
| Visible | True |
| Want Return | False |

ID
指定控件的标识符。

图 16-13

如果你将“自动水平滚动”（Auto HScroll）属性的值设置为 False，当输入文本时到达控件边缘，编辑框会自动滚动到该行。然而，这只是为了编辑框内的可见性——对字符串的内容没有影响。你也可以将“自动垂直滚动”（Auto VScroll）属性的值设置为 True，允许文本超出可见行数继续。如果你将“垂直滚动”（Vertical Scroll）属性设置为 True，编辑控件将提供一个滚动条，允许你滚动。

### 创建对话框类

保存对话框资源后，你可以创建一个响应资源的合适对话框类，可以命名为 `CTextDialog`。在编辑器面板中右键点击对话框并选择添加类（Add Class）。基类为 `CDialog`。

类定义将如下：

```cpp
class CTextDialog : public CDialog
{
public:
    CTextDialog(CWnd* pParent = nullptr);
    virtual ~CTextDialog();

protected:
    virtual void DoDataExchange(CDataExchange* pDX);
    DECLARE_MESSAGE_MAP()
};
```

在类头文件中，你应该添加一个变量来存储文本：

```cpp
CString m_str;
```

然后，实现 `DoDataExchange` 函数将变量与控件关联：

```cpp
void CTextDialog::DoDataExchange(CDataExchange* pDX)
{
    CDialog::DoDataExchange(pDX);
    DDX_Text(pDX, IDC_EDIT_TEXT, m_str);
}
```

现在，你可以在代码中使用该对话框类：

```cpp
CTextDialog dlg(ID_TEXT_DLG);
if (dlg.DoModal() == IDOK)
{
    // 使用来自 dlg.m_str 的文本
}
```

### 实现 CText 类

你需要为 `CText` 类实现三个函数：

- `CText` 对象的构造函数
- 用于显示它的虚拟函数 `Draw()`
- 用于支持通过鼠标拖拽移动文本的虚拟函数 `Move()`

我已将这些内容直接添加到 `Text.cpp` 文件中。

#### CText 构造函数

`CText` 对象的构造函数需要初始化类和基类数据成员：

```cpp
CText::CText(const CPoint& start, const CPoint& end,
             const CString& aString, COLORREF color) :
    CElement(start, color)
{
    m_String = aString; // 存储字符串
    m_EnclosingRect = CRect(start, end);
    m_EnclosingRect.NormalizeRect();
    m_EnclosingRect.InflateRect(m_PenWidth, m_PenWidth);
}
```

基类调用了起点和颜色，并默认将笔宽初始化为 1。你需要计算当字符串从起点和终点显示时，包围字符串的矩形。

### 创建文本元素

如果元素类型已设置为 `ElementType::TEXT`，每当你点击左键并输入你想要显示的文本时，都应该在光标位置创建一个文本对象。因此，你需要在 `OnButtonDown` 处理器中显示允许输入文本的对话框，但仅当元素类型为 `ElementType::TEXT` 时如此。在 `CScrollView` 的此处理函数中添加以下代码：

```cpp
void CScrollView::OnButtonDown(UINT flags, CPoint point)
{
    CClientDC dc(this); // 创建设备上下文
    OnPrepareDC(&dc); // 获取调整后的原点
    dc.DPToLP(&point); // 将点转换为逻辑坐标
    CTextScrollView* pDoc = GetDocument(); // 获取文档指针

    if (m_Moving)
    { // 在移动模式下，释放元素
        m_Moving = false; // 停止鼠标移动
        auto pElement(m_pSelected); // 存储选中元素
        m_pSelected.reset(); // 取消选择元素
        pDoc->UpdateAllViews(nullptr, 0, pElement->get()); // 重新绘制所有视图
    }
    else if (pDoc->GetElementType() == ElementType::TEXT)
    {
        CTextDialog dlg;
        if (dlg.DoModal() == IDOK)
        {
            // 点击 OK 后创建文本元素
            CSize textExtent = dlg.GetTextExtent(dlg.m_str);
            textExtent.cx *= m_Scale;
            textExtent.cy *= m_Scale;
            std::shared_ptr<CText> pElement = std::make_shared<CText>(point, point + textExtent, dlg.m_str,
                static_cast<COLORREF>(static_cast<CDoc*>(pDoc)->GetElementColor()));
            pDoc->AddElement(pElement); // 将元素添加到文档
            pDoc->UpdateAllViews(nullptr, 0, pElement.get()); // 更新所有视图
        }
    }
    else
    {
        m_FirstPoint = point; // 记录光标位置
        SetCursor(); // 捕获部分鼠标移动
    }
}
```
