
## 第15章

![](img/2359b0c604600c58fba3539c738a356e_829_0.png)

图15-10

要添加调用 `SetScrollSizes()` 的代码，你需要在视图中重写 `OnInitialUpdate()` 函数的默认版本。访问它的方式与重写 `OnUpdate()` 函数相同（通过 `CSketcherView` 类的属性窗口）。添加重写后，只需在函数中注释指示的位置添加代码：

```cpp
void CSketcherView::OnInitialUpdate()
{
    CScrollView::OnInitialUpdate();

    // Define document size
    CSize DocSize(20000,20000);

    // Set mapping mode and document size.
    SetScrollSizes(MM_TEXT,DocSize);
}
```

这会保持映射模式为 `MM_TEXT`，并定义你在每个方向上可以绘制的总范围为20000像素。

这足以让滚动机制在一定程度上工作。用这些添加内容构建程序并运行，你将能够绘制一些元素，然后滚动视图。然而，虽然窗口滚动正常，但如果在视图滚动后尝试绘制更多元素，事情就不会按预期工作。元素出现在与绘制位置不同的位置，并且没有正确显示。这是怎么回事？

### 逻辑坐标与客户坐标

问题在于你正在使用的坐标系——这里用复数是有意的。到目前为止的所有示例中，你实际上一直在使用两个坐标系，虽然你可能没有注意到。正如你在前一章所见，当你调用类似 `LineTo()` 的函数时，它假定传入的参数是逻辑坐标。该函数是定义设备上下文的 `CDC` 类的成员，设备上下文有它自己的逻辑坐标系。映射模式是设备上下文的一个属性，它决定你在绘制内容时坐标的度量单位。

另一方面，你随鼠标消息接收到的坐标数据与设备上下文或 `CDC` 对象无关——并且在设备上下文之外，逻辑坐标并不适用。传递给 `OnLButtonDown()` 和 `OnMouseMove()` 处理程序的点，其坐标始终是设备单位，即像素，并且相对于客户区的左上角测量。这些被称为客户坐标。类似地，当你调用 `InvalidateRect()` 时，矩形被假定是以客户坐标定义的。

在 `MM_TEXT` 模式下，客户坐标和设备上下文中的逻辑坐标都以像素为单位，所以它们是相同的（只要你不滚动窗口）。在之前所有示例中都没有滚动，所以一切都没问题。对于最新版本的 Sketcher，在滚动视图之前一切正常，滚动之后，逻辑坐标原点（0,0点）会被滚动机制移动，因此它不再与客户坐标原点在同一位置。这里的逻辑坐标和客户坐标单位相同，但两个坐标系的原点不同。这种情况如图15-11所示。

左侧显示你在客户区中绘制的位置，以及定义线条的鼠标位置点。这些是以客户坐标记录的。右侧显示线条实际绘制的位置。绘制是在逻辑坐标中进行的，但你一直使用的是客户坐标值。在滚动窗口的情况下，由于逻辑原点被重新定位，线条会出现位移。

这意味着你实际上在Sketcher程序中使用错误的值来定义元素，并且当你使客户区的某些区域失效以重新绘制时，传递给函数的矩形也是错误的——因此程序行为怪异。对于其他映射模式，情况会更糟，因为不仅两个坐标系中的度量单位不同，而且y轴的方向也可能相反！

### 处理客户坐标

考虑需要做些什么来修复问题。你可能需要处理两件事：

- 你需要在将鼠标消息获得的客户坐标用于创建元素之前，将它们转换为逻辑坐标。
- 如果要在 `InvalidateRect()` 调用中使用边界矩形，你需要将在逻辑坐标中创建的边界矩形转换回客户坐标。

这相当于确保你在使用设备上下文函数时始终使用逻辑坐标，并在与窗口有关的其他通信中始终使用客户坐标。进行转换需要使用的函数与设备上下文关联，因此每当你想要在逻辑坐标和客户坐标之间进行转换时，都需要获取一个设备上下文。你可以使用 `CClientDC` 从 `CDC` 类继承的坐标转换函数来完成这项工作。

图15-11

### 创建文档并改进视图

包含这一处理的新版 `OnLButtonDown()` 处理程序是：

```cpp
// Handler for left mouse button down message
void CSketcherView::OnLButtonDown(UINT nFlags, CPoint point)
{
	CClientDC aDC(this);
	// Create a device context
	OnPrepareDC(&aDC);
	// Get origin adjusted
	aDC.DPtoLP(&point);
	// convert point to Logical
	m_FirstPoint = point;
	// Record the cursor position
	SetCapture();
	// Capture subsequent mouse messages
}
```

你通过创建 `CClientDC` 对象并将指针 `this` 传递给构造函数，来获取当前视图的设备上下文。使用 `CClientDC` 对象的优点是，当对象超出作用域时，它会自动释放设备上下文。重要的是不要保留设备上下文，因为Windows提供的设备上下文数量有限，你可能会用完它们。如果使用 `CClientDC`，你总是安全的。

由于你使用 `CScrollView`，必须调用从该类继承的 `OnPrepareDC()` 成员函数，将设备上下文中的逻辑坐标系原点设置为与滚动位置对应。通过此调用设置原点后，你使用 `DPtoLP()` 函数，它将设备点转换为逻辑点，将传递给处理程序的点值转换为逻辑坐标。然后，你存储转换后的点，以便在 `OnMouseMove()` 处理程序中创建元素时使用。

新的 `OnMouseMove()` 处理程序代码如下：

```cpp
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
	CClientDC aDC(this);
	// Device context for the current view
	OnPrepareDC(&aDC);
	// Get origin adjusted
	if ((nFlags&MK_LBUTTON) && (this==GetCapture()))
	{
		aDC.DPtoLP(&point);
		// convert point to Logical
		m_SecondPoint = point;
		// Save the current cursor position
		// Rest of the function as before...
	}
}
```

传递给处理程序的点值转换代码与之前的处理程序基本相同，目前你只需要这些。最后一个必须更改的函数很容易忽略：视图类中的 `OnUpdate()` 函数。需要将其修改为：

```cpp
void CSketcherView::OnUpdate(CView* pSender, LPARAM lHint, CObject* pHint)
{
	// Invalidate the area corresponding to the element pointed to
	// if there is one, otherwise invalidate the whole client area
	if(pHint)
	{
		CClientDC aDC(this);
		// Create a device context
		OnPrepareDC(&aDC);            // Get origin adjusted

		// Get the enclosing rectangle and convert to client coordinates
		CRect aRect=((CElement*)pHint)->GetBoundRect();
		aDC.LPtoDP(aRect);
		InvalidateRect(aRect);        // Get the area redrawn
	}
	else
		InvalidateRect(0);          // Invalidate the client area
}
```

### 使用MM_LOENGLISH映射模式

现在来看看使用 `MM_LOENGLISH` 映射模式需要做什么。这种模式以0.01英寸的逻辑单位进行绘图，并且还能确保在不同分辨率的显示器上绘图大小一致。从用户的角度来看，这使应用程序更加令人满意。

你可以在视图类的 `OnInitialUpdate()` 函数中调用 `SetScrollSizes()` 时设置映射模式。你还需要指定总绘图区域，因此如果你将其定义为3000乘3000，就会提供30英寸乘30英寸的绘图区域，这应该是足够的。一行和一页的默认滚动距离已经令人满意，所以不需要指定它们。你可以使用类视图定位到 `OnInitialUpdate()` 函数，然后将其改为以下内容：

```cpp
void CSketcherView::OnInitialUpdate(void)
{
    CScrollView::OnInitialUpdate();

    // Define document size as 30x30ins in MM_LOENGLISH
    CSize DocSize(3000,3000);

    // Set mapping mode and document size.
    SetScrollSizes(MM_LOENGLISH, DocSize);
}
```

你只需更改 `SetScrollSizes()` 调用中针对映射模式和所需文档大小的参数。这就是让视图在 `MM_LOENGLISH` 下工作所需的全部操作，但你仍然需要修复处理矩形的方式。

请注意，你并不局限于一次性设置映射模式。你可以随时更改设备上下文中的映射模式，并使用不同的映射模式绘制要显示图像的不同部分。函数 `SetMapMode()` 用于执行此操作，但这里我不再进一步展开。你可以只使用 `MM_LOENGLISH` 就让应用程序正常工作。每当你为视图创建 `CClientDC` 对象并调用 `OnPrepareDC()` 时，它拥有的设备上下文都会使用你在 `OnInitialUpdate()` 函数中设置的映射模式。

