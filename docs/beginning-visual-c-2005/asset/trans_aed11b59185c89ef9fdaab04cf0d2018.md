

## 实现多页打印

要设置文档中的第一页编号，需要在 CPrintInfo 对象中调用 SetMinPage() 函数，该函数接受类型为 UINT 的页码作为参数。没有返回值。要设置文档中的最后一页编号，需要调用 SetMaxPage() 函数，该函数同样接受类型为 UINT 的页码作为参数且不返回数值。如果以后想要检索这些值，可以为 CPrintInfo 对象调用 GetMinPage() 和 GetMaxPage() 函数。

你提供的页码存储在 CPrintInfo 的 m_pPD 成员指向的 CPrintDialog 对象中，并在从菜单中选择 File > Print... 时弹出的对话框中显示。然后用户能够指定要打印的第一页和最后一页的编号，你可以通过调用 CPrintInfo 对象的 GetFromPage() 和 GetToPage() 成员来检索这些编号。在每种情况下，返回的值的类型都是 UINT。对话框会自动验证要打印的第一页和最后一页的编号是否在你通过指定文档的最小页码和最大页码所提供的范围内。

你现在知道可以在视图类中实现哪些函数来为自己管理打印，框架完成大部分工作。你也知道通过传递给与打印相关的函数的 CPrintInfo 对象可以获得哪些信息。如果你为 Sketcher 文档实现一个基本的多页打印功能，你将对打印的详细机制有更清晰的理解。

Sketcher 程序中使用 MM_LOENGLISH 映射模式进行设置，然后切换到 MM_ANISOTROPIC。这意味着形状和视图范围以英寸的百分之一为单位进行测量。当然，由于尺寸单位是固定的物理度量，理想情况下你希望以实际尺寸打印对象。

文档大小指定为 3000 x 3000 单位，你可以创建最大为 30 英寸见方的文档，如果填满整个区域的话会跨越相当多的纸张。与典型的文本文档相比，计算打印草图所需的页数需要付出更多努力，因为在大多数情况下，你需要一个二维的页数组来打印完整的草图文档。

为了避免使问题过于复杂，假设你正在打印一张普通的纸张（A4 尺寸或 8 1/2 x 11 英寸），并且为纵向方向（这意味着长边为垂直）。对于任何一种纸张尺寸，你都将在测量为 6 英寸 x 9 英寸的纸张中央部分打印文档。在这些假设下，你无需担心实际的纸张尺寸；你只需要将文档切成 600 x 900 单位的块。对于超过一页的文档，你将按图 17-6 中的示例所示划分文档。

正如你所见，你将按行对页进行编号，因此在这种情况下，第 1 到 4 页在第一行，第 5 到 8 页在第二行。

![](img/2359b0c604600c58fba3539c738a356e_930_0.png)

图 17-6

## 获取整体文档大小

要确定特定文档占用多少页，你需要知道草图有多大，为此你需要包含文档中所有内容的矩形。你可以通过向文档类 CSketcherDoc 添加一个 GetDocExtent() 函数来轻松完成此操作。将以下声明添加到 CSketcherDoc 的公共接口中：

```
CRect GetDocExtent();      // Get the bounding rectangle for the whole document
```

实现并不复杂。其代码为：

```
// Get the rectangle enclosing the entire document
CRect CSketcherDoc::GetDocExtent()
{
    CRect DocExtent(0,0,1,1);          // Initial document extent
    CRect ElementBound(0,0,0,0);       // Space for element bounding rectangle

    POSITION aPosition = m_ElementList.GetHeadPosition();

    while(aPosition)                   // Loop through all the elements in the list
    {
        // Get the bounding rectangle for the element
        ElementBound=(m_ElementList.GetNext(aPosition))->GetBoundRect();

        // Make coordinates of document extent the outer limits
        DocExtent.UnionRect(DocExtent, ElementBound);
    }
    DocExtent.NormalizeRect();
    return DocExtent;
}
```

你可以将此函数定义添加到 SketcherDoc.cpp 文件中，或者如果你使用 Class View 中的弹出窗口的 Add > Add Function 功能，则只需添加代码。该过程遍历文档中的每个元素，使用 aPosition 变量逐步遍历列表并获取每个元素的边界矩形。CRect 类的 UnionRect() 成员计算包含作为参数传递的两个矩形的最小矩形，并将该值放入调用该函数的 CRect 对象中。因此，DocExtent 会不断增大，直到所有元素都被包含在其中为止。请注意，你将 DocExtent 初始化为 (0,0,1,1)，因为 UnionRect() 函数在高度或宽度为零的矩形上不能正常工作。

## 存储打印数据

视图类中的 OnPreparePrinting() 函数由应用程序框架调用，以便你可以初始化文档的打印过程。所需的基本初始化是为显示的打印对话框提供文档中页数的相关信息。你需要存储文档所需的页面的相关信息，以便稍后在打印过程中涉及的其他视图函数中使用。你将在视图类的 OnPreparePrinting() 成员中发起此操作，将其存储在为此目的而定义的你自己的类对象中，并将指向该对象的指针存储在框架提供的 CPrintInfo 对象中。这种方法主要是为了向你展示该机制的工作原理；在大多数情况下，你会发现将数据存储在视图对象中更容易，主要是因为引用数据的记法更简单。

你需要存储文档宽度的页数 m_nWidths，以及文档长度方向的页行数 m_nLengths。你还将文档内容包围矩形的左上角存储为 CPoint 对象 m_DocRefPoint，因为你将在根据页码计算要打印的页面的位置时使用它。你可以将文档的文件名存储在 CString 对象 m_DocTitle 中，以便将其作为标题添加到每一页。用于容纳这些内容的类的定义为：

```
#pragma once

class CPrintData
{
public:
    UINT m_nWidths;                // Page count for the width of the document
    UINT m_nLengths;               // Page count for the length of the document
    CPoint m_DocRefPoint;          // Top left corner of the document contents
    CString m_DocTitle;            // The name of the document
};
```

你可以通过在 Solution Explorer 窗格中右键单击 Header Files 文件夹，然后从弹出窗口中选择 Add > New Item 来向项目添加一个名为 PrintData.h 的新头文件。现在你可以在新文件中输入类定义。

此类的实现文件不是必需的。默认构造函数（自动生成）在这里已经足够。因为此类对象仅用于临时使用，所以你不需要使用 CObject 作为基类，也不需要考虑其他复杂性。

打印过程始于对视图类成员 OnPreparePrinting() 的调用，因此请查看你应如何实现它。

## 准备打印

Application 向导在开始时为 CSketcherView 添加了 OnPreparePrinting()、OnBeginPrinting() 和 OnEndPrinting() 的版本。OnPreparePrinting() 提供的基代码在 return 语句中调用 DoPreparePrinting()，正如你所见：

```
BOOL CSketcherView::OnPreparePrinting(CPrintInfo* pInfo)
{
    // default preparation
    return DoPreparePrinting(pInfo);
}
```

DoPreparePrinting() 函数使用 CPrintInfo 对象中定义的待打印页数的信息显示打印对话框。只要可能，你应该在调用此函数之前计算待打印的页数并将其存储在 CPrintInfo 对象中。当然，在许多情况下，你可能需要在调用 OnPreparePrinting() 之前需要打印机设备上下文的信息——例如，当打印的文档页数会受所用字体大小影响时——在这种情况下，在调用 OnPreparePrinting() 之前无法获取页数。在这种情况下，你可以在 OnBeginPrinting() 成员中计算页数，该成员接收指向设备上下文的指针。该函数由框架在 OnPreparePrinting() 之后调用，因此打印对话框中输入的信息是可用的。这意味着你也可以考虑用户在打印对话框中选择的纸张尺寸。

假设页面尺寸足够容纳 6 英寸 x 9 英寸的区域来绘制文档数据，因此你可以在 OnPreparePrinting() 中计算页数。其代码为：

```
BOOL CSketcherView::OnPreparePrinting(CPrintInfo* pInfo)
{
    pInfo->m_lpUserData = new CPrintData;      // Create a print data object
    CSketcherDoc* pDoc = GetDocument();       // Get a document pointer

    // Get the whole document area
    CRect DocExtent = pDoc->GetDocExtent();

    // Save the reference point for the whole document
    ((CPrintData*)(pInfo->m_lpUserData))->m_DocRefPoint =
        CPoint(DocExtent.left, DocExtent.bottom);

    // Get the name of the document file and save it
    ((CPrintData*)(pInfo->m_lpUserData))->m_DocTitle = pDoc->GetTitle();

    // Calculate how many printed page widths of 600 units are required
    // to accommodate the width of the document
    ((CPrintData*)(pInfo->m_lpUserData))->m_nWidths =
        static_cast<UINT>(ceil((static_cast<double>(DocExtent.Width()))/600.0));

    // Calculate how many printed page lengths of 900 units are required
    // to accommodate the document length
    ((CPrintData*)(pInfo->m_lpUserData))->m_nLengths =
        static_cast<UINT>(ceil((static_cast<double>(DocExtent.Height()))/900.0));

    // Set the first page number as 1 and
```

