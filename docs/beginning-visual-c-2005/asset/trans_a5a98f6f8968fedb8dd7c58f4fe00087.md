

## 第17章：存储和打印文档

```cpp
m_pSelected->Draw(&aDC,m_pSelected);  // Draw highlighted

return;
}

// ...otherwise, use this method
aDC.SetROP2(R2_NOTXORPEN);
m_pSelected->Draw(&aDC,m_pSelected);    // Draw the element to erase it
m_pSelected->Move(Distance);            // Now move the element
m_pSelected->Draw(&aDC,m_pSelected);    // Draw the moved element
}
```

你可以看到，用于移动文本时必须使用的矩形无效化代码，比用于其他所有元素的那种 ROP 代码优雅得多。它确实有效，正如你如果做出此修改然后构建并运行应用程序后自己会看到的那样。如果你想尝试使用 typeid() 机制来测试类型，只需更改 if 语句中的条件并在 SketcherView.cpp 中添加对 `<typeinfo>` 的 #include 指令即可。

### 打印文档

现在来看一下打印文档。Sketcher 程序中已经通过应用程序向导和框架实现了基本的打印功能。File > Print、File > Print Setup 和 File > Print Preview 菜单项都可以使用。选择 File > Print Preview 菜单项会显示一个窗口，显示当前 Sketcher 文档在页面上的样子，如图 17-4 所示。

![](img/2359b0c604600c58fba3539c738a356e_925_0.png)

图 17-4

无论当前文档中有什么内容，都会以当前视图比例放置在一张纸上。如果文档的范围超出纸张边界，则超出纸张部分的文档将不会被打印。如果你选择 Print 按钮，此页面将被发送到你的打印机。

作为一种免费获得的基础功能，它相当令人印象深刻，但对于大多数用途来说是不够的。我们程序中的典型文档可能根本放不下一页，因此你可能希望将文档缩放以适应，或者更方便地，将整个文档打印到所需的多个页面上。你可以添加自己的打印处理代码来扩展框架提供的功能，但要实现这一点，你首先需要了解 MFC 中是如何实现打印的。

### 打印过程

打印文档由当前视图控制。由于打印本质上是一件混乱的事情，因此该过程不可避免地有点混乱，并且可能需要你在视图类中实现相当数量的继承函数的自己的版本。

图 17-5 显示了该过程的逻辑和所涉及的函数。

![](img/2359b0c604600c58fba3539c738a356e_926_0.png)

图 17-5 显示了事件序列如何由框架控制，以及打印文档如何涉及调用当前视图类的五个继承成员，你可能需要重写它们。图中左侧显示的 CDC 成员函数与打印机设备驱动程序通信，并由框架自动调用。

在打印操作期间，当前视图中每个函数的典型作用在旁边的注释中指定。它们被调用的顺序由箭头上的数字指示。实际上，你不必实现所有这些函数，只需实现那些满足你特定打印需求的函数即可。通常，你至少需要实现自己的 OnPreparePrinting()、OnPrepareDC() 和 OnPrint() 版本。你将在本章后面 Sketcher 程序的上下文中看到这些函数如何实现的示例。

向打印机输出数据的方式与向显示器输出数据的方式相同——通过设备上下文。你用来输出文本或图形的 GDI 调用是设备无关的，因此它们对打印机同样有效，就像对显示器一样。唯一的区别是 CDC 对象所应用的设备。

图 17-5 中的 CDC 函数与打印机的设备驱动程序通信。如果要打印的文档需要多于一页打印，则该过程会循环返回以对每个后续新页面调用 OnPrepareDC() 函数，如 EndPage() 函数所确定。

在打印过程中涉及的视图类中的所有函数都作为参数传递一个指向 CPrintInfo 类型对象的指针。此对象在管理打印过程的所有函数之间提供了一个链接，因此请更详细地查看 CPrintInfo 类。

### CPrintInfo 类

CPrintInfo 对象在打印过程中具有基本作用，因为它存储正在执行的打印作业的信息以及其在任何时间的状态的详细信息。它还提供访问和操作此数据的函数。此对象是在打印期间在视图函数之间以及框架与视图函数之间传递信息的手段。

每当你选择 File > Print 或 File > Print Preview 菜单选项时，都会创建一个 CPrintInfo 类的对象。在被当前视图中涉及打印过程的每个函数使用后，它会在打印操作结束时自动删除。

CPrintInfo 的所有数据成员都是公开的。它们是：

| 成员 | 用途 |
|---|---|
| m_pPD | 指向显示打印对话框的 CPrintDialog 对象的指针。 |
| m_bDirect | 如果框架设置打印操作为绕过打印对话框，则此值由框架设置为 TRUE；否则为 FALSE。 |
| m_bPreview | 一个类型为 BOOL 的成员，如果选择了 File > Print Preview，则其值为 TRUE；否则为 FALSE。 |
| m_bContinuePrinting | 一个类型为 BOOL 的成员。如果将其设置为 TRUE，框架将继续图中所示的打印循环。如果将其设置为 FALSE，打印循环将结束。你仅在不向 CPrintInfo 对象传递打印操作的页数（使用 SetMaxPage() 成员函数）的情况下才需要设置此变量。在这种情况下，你将负责通过将此变量设置为 FALSE 来发出已完成的信号。 |
| m_nCurPage | 一个类型为 UINT 的值，存储当前页面的页码。页面通常从 1 开始编号。 |
| m_nNumPreviewPages | 一个类型为 UINT 的值，指定打印预览窗口中显示的页数。这可以是 1 或 2。 |
| m_lpUserData | 这是类型为 LPVOID 的，存储指向你创建的对象的指针。这允许你创建一个对象来存储有关打印操作的附加信息并将其与 CPrintInfo 对象关联。 |
| m_rectDraw | 一个 CRect 对象，以逻辑坐标定义页面的可用区域。 |
| m_strPageDesc | 一个 CString 对象，包含框架在打印预览期间用于显示页码的格式字符串。 |

CPrintInfo 对象具有以下公共成员函数：

| 函数 | 描述 |
|---|---|
| SetMinPage(UINT nMinPage) | 参数指定文档的第一页的页码。没有返回值。 |
| SetMaxPage(UINT nMaxPage) | 参数指定文档的最后一页的页码。没有返回值。 |
| GetMinPage() const | 以类型 UINT 返回文档的第一页的页码。 |
| GetMaxPage() const | 以类型 UINT 返回文档的最后一页的页码。 |
| GetFromPage() const | 以类型 UINT 返回要打印的文档的第一页的页码。此值通过打印对话框设置。 |
| GetToPage() const | 以类型 UINT 返回要打印的文档的最后一页的页码。此值通过打印对话框设置。 |

当你打印由多个页面组成的文档时，你需要计算出文档占用多少打印页，并将此信息存储在 CPrintInfo 对象中以使其可供框架使用。你可以在当前视图的 OnPreparePrinting() 成员的版本中执行此操作。

