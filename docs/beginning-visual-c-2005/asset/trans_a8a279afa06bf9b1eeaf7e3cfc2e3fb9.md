

## 使用对话框和控件

使用指向对话框的 `CListBox` 对象的指针，然后重复使用 `AddString()` 成员来添加定义比例因子列表的行。它们会按你输入的顺序出现在列表框中，因此对话框显示如 Figure 16-19 所示。

![](img/2359b0c604600c58fba3539c738a356e_896_0.png)

**Figure 16-19**

列表中的每个条目都与一个从零开始的索引值相关联，该值会通过 DDX 机制自动存储在 `CScaleDialog` 的 `m_Scale` 成员中。因此，如果你从列表中选择第三个条目，`m_Scale` 将被设置为 2。

### 显示对话框

对话框由你在 Sketcher 的前一版本中添加到 `CSketcherView` 的 `OnViewScale()` 处理程序显示。你只需要对其进行修改以处理使用列表框的新对话框。其代码如下：

```
void CSketcherView::OnViewScale()
{
    CScaleDialog aDlg;                 // Create a dialog object
    aDlg.m_Scale = m_Scale;             // Pass the view scale to the dialog
    if(aDlg.DoModal() == IDOK)
    {
        m_Scale = 1 + aDlg.m_Scale;     // Get the new scale

        // Get the frame that wraps this view
        CChildFrame* childFrame = static_cast<CChildFrame*>(GetParentFrame());

        // Build the message string
        CString StatusMsg("View Scale:");
        StatusMsg += static_cast<char>('1' + m_Scale - 1);
        // Set the status bar
        childFrame->m_StatusBar.GetStatusBarCtrl().SetText(StatusMsg, 0, 0);

        ResetScrollSizes();             // Adjust scrolling to the new scale
        InvalidateRect(0);              // Invalidate the whole window
    }
}
```

由于从列表中选择的条目的索引值是从零开始的，你只需向其添加 1 即可得到要存储在视图中的实际比例值。显示此值在视图状态栏中的代码与之前完全相同。处理比例因子的其余代码已经完成，无需更改。在添加回 `ScaleDialog.h` 的 `#include` 指令后，你可以构建并执行此版本的 Sketcher 来查看列表框的运行情况。

![](img/2359b0c604600c58fba3539c738a356e_898_0.png)

Figure 16-20

当你完成编辑框属性的设置后，关闭其属性窗口。确保编辑框在选项卡顺序中排在首位，可以通过选择 Format > Tab Order 菜单项或按 Ctrl+D 来实现。然后你可以通过选择 Test Dialog 菜单项或按 Ctrl+T 来测试对话框。对话框显示在 Figure 16-21 中。

![](img/2359b0c604600c58fba3539c738a356e_898_1.png)

Figure 16-21

你甚至可以在测试模式下向对话框中输入文本以查看其工作原理。单击 OK 或 Cancel 按钮可关闭对话框。

## Chapter 16

### 创建对话框类

保存对话框资源后，你可以为资源创建一个合适的对话框类，可以将其命名为 CTextDialog。在资源视图中右键单击对话框并从弹出菜单中选择 Add Class 来执行此操作。基类应为 CDialog。接下来，你可以通过在类视图中右键单击类名并从弹出菜单中选择 Add > Add Variable 来添加一个控件变量。选择 IDC_EDITTEXT 作为控件 ID，类别为 Value。将新变量命名为 m_TextString，并将其类型保留为 CString —— 你将在完成对话框类后查看此类。你还可以在 Max chars: 编辑框中指定其最大长度，如 Figure 16-22 所示。

![](img/2359b0c604600c58fba3539c738a356e_899_0.png)

Figure 16-22

长度 100 对于你的需求来说已经足够了。你在此处添加的变量会通过 DDX 机制自动从控件中输入的数据进行更新。你可以单击 Finish 在 CTextDialog 类中创建变量并关闭 Add Member Variable 向导。

### CString 类

CString 类提供了一种非常方便且易于使用的机制来处理字符串，你可以在几乎任何需要字符串的地方使用它。更准确地说，你可以在类型为 const char* 的字符串或类型为 LPCTSTR 的字符串的位置使用 CString 对象，后者是原生 C++ 中字符字符串的常用类型，也是 Windows API 函数中经常出现的类型。

CString 类提供了多个重载运算符，使处理字符串变得容易：

| Operator | Usage |
|---|---|
| = | 将一个字符串复制到另一个字符串，如： **Str1 = Str2;** // 将 Str1 的内容复制到 Str2 **Str1 = "A normal string";** // 将右侧字符串复制到 Str1 |
| + | 连接两个或多个字符串，如： **Str1 = Str2 + Str3 + " more";** // 从 3 个字符串形成 Str1 |
| += | 将字符串追加到现有的 CString 对象。 |
| == | 比较两个字符串是否相等，如： **if(Str1 == Str2)** // 执行某事... |
| < | 测试一个字符串是否小于另一个字符串。 |
| <= | 测试一个字符串是否小于或等于另一个字符串。 |
| > | 测试一个字符串是否大于另一个字符串。 |
| >= | 测试一个字符串是否大于或等于另一个字符串。 |

上表中变量 Str1 和 Str2 是 CString 对象。CString 对象会根据需要自动增长，例如当你向现有对象的末尾添加额外字符串时。例如，在以下语句中，

```
CString Str = "A fool and your money ";
Str += "are soon partners.";
```

第一条语句声明并初始化对象 Str。第二条语句将额外字符串追加到 Str，因此 Str 的长度会自动增加。

> 通常，你应尽可能避免在堆上创建 CString 对象。它们增长所需的内存管理意味着操作会很慢。

### 添加文本菜单项

添加新菜单项现在应该很容易了。你只需在资源视图中双击它打开 ID 为 IDR_SketcherTYPE 的菜单资源，并在 Element 菜单中添加一个新菜单项 Text。项目属性窗口中出现的默认 ID ID_ELEMENT_TEXT 是可以的，因此你可以保持不变。你可以为菜单项添加要在状态栏上显示的提示，并且由于你还希望为此菜单项添加一个额外的工具栏按钮，因此你可以使用 \n 将提示和工具提示分开，在提示行的末尾添加工具提示。

不要忘记上下文菜单。你可以从 IDR_SketcherTYPE 复制菜单项。右键单击 Text 菜单项并从弹出菜单中选择 Copy。打开菜单 IDR_CURSOR_MENU，展开 no element 菜单，右键单击底部的空项目并选择 Paste。你所需要做的就是将项目拖动到适当的 __分隔符上方__ 的位置 —— 并保存资源文件。

## Chapter 16

将工具栏按钮添加到 IDR_MAINFRAME 工具栏并将其 ID 设置为与菜单项相同，即 ID_ELEMENT_TEXT。你可以将新按钮拖动到定义其他类型元素的块末尾的位置。当你保存资源后，可以为新菜单项添加事件处理程序。

在 Class View 窗格中，右键单击 CSketcherDoc 并显示其属性窗口。为 ID_ELEMENT_TEXT ID 添加一个 COMMAND 处理程序并按如下方式添加代码：

```
void CSketcherDoc::OnElementText()
{
    m_Element = TEXT;
}
```

只需一行代码即可将文档中的元素类型设置为 TEXT。

你还需要添加一个函数来在它是当前模式时检查菜单项，因此添加一个对应于 ID_ELEMENT_TEXT ID 的 UPDATE_COMMAND_UI 处理程序，并按如下方式实现其代码：

```
void CSketcherDoc::OnUpdateElementText(CCmdUI* pCmdUI)
{
    // Set checked if the current element is text
    pCmdUI->SetCheck(m_Element == TEXT);
}
```

这与其它 Element 弹出菜单项的操作方式相同。

你还必须在 OurConstants.h 头文件中添加一行：

```
const unsigned int TEXT = 105U;
```

你可以将此语句添加到头文件中其它元素类型定义末尾。下一步是为类型为 TEXT 的对象定义 CText 类。

### 定义文本元素

你可以按如下方式从 CElement 类派生 CText 类：

```
// Class defining a text object
class CText: public CElement
{
public:
    // Function to display a text element
    virtual void Draw(CDC* pDC, CElement* pElement=0);

    // Constructor for a text element
    CText(CPoint Start, CPoint End, CString aString, COLORREF aColor);
    virtual void Move(CSize& aSize);      // Move a text element

protected:

