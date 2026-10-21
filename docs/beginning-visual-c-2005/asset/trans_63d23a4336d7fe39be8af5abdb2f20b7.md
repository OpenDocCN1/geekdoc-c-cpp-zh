

## 完成鼠标消息处理程序

现在你可以回到 WM_MOUSEMOVE 消息处理程序，并补充细节。你可以在类视图中选择 CSketcherView，然后双击处理程序名称 OnMouseMove() 来进入该处理程序。

该处理程序只关心在移动光标时绘制一系列临时版本的元素，因为最终元素是在你释放鼠标左键时创建的。因此，你可以将提供橡皮筋效果的临时元素绘制完全视为该函数内部的局部操作，而将创建的最终版本元素留给视图的 OnDraw() 函数成员来绘制。这种方法使橡皮筋元素的绘制相当高效，因为它不会涉及最终负责绘制整个文档的 OnDraw() 函数。

要做到这一点，最好借助 CDC 类的一个在橡皮筋操作中特别有效的成员：SetROP2()。

## 设置绘图模式

SetROP2() 函数为与 **CDC** 对象关联的设备上下文中所有后续输出操作设置**绘图模式**。函数名中的“ROP”表示 Raster Operation（光栅操作），因为绘图模式的设置适用于光栅显示。如果你想知道“那 SetROP1() 呢？”——并没有这个函数。函数名的含义是“Set Raster Operation to”，而不是 2！

绘图模式决定你用于绘图的笔颜色如何与背景色组合，以生成所显示实体的颜色。你只需向该函数传递一个参数即可指定绘图模式，该参数可以是以下任意值：

| 绘图模式 | 效果 |
|---|---|
| `R2_BLACK` | 所有绘制均为黑色。 |
| `R2_WHITE` | 所有绘制均为白色。 |
| `R2_NOP` | 绘制操作不产生任何效果。 |
| `R2_NOT` | 以屏幕颜色的反色进行绘制。这确保输出始终可见，因为它避免以与背景相同的颜色进行绘制。 |
| `R2_COPYPEN` | 以笔的颜色进行绘制。这是默认绘图模式（如果你不设置的话）。 |
| `R2_NOTCOPYPEN` | 以笔颜色的反色进行绘制。 |
| `R2_MERGEPENNOT` | 以笔颜色与背景颜色的反色进行 OR（按位或）运算后产生的颜色进行绘制。 |
| `R2_MASKPENNOT` | 以笔颜色与背景颜色的反色进行 AND（按位与）运算后产生的颜色进行绘制。 |
| `R2_MERGENOTPEN` | 以背景颜色与笔颜色的反色进行 OR（按位或）运算后产生的颜色进行绘制。 |

## 在窗口中绘制

|  | R | G | B |
|---|---:|---:|---:|
| 背景——红色 | 1 | 0 | 0 |
| 笔——红色 | 1 | 0 | 0 |
| XOR（异或）后 | 0 | 0 | 0 |
| NOT XOR（异或非）——产生白色 | 1 | 1 | 1 |

如最后一行所示，线条以白色出现，又因为背景其余部分为白色，线条便消失了。

这里你需要注意使用正确的背景色。你应该能够看出，在红色背景上用白色笔画图并不会很理想，因为第一次绘制时图形是红色的，因此不可见；第二次才显示为白色。如果在黑色背景上绘制，图形会像在白色背景上一样出现和消失，但不会以你选择的笔颜色绘制。

## 编写 OnMouseMove() 处理程序

首先添加在鼠标移动消息后创建元素的代码。由于你要在处理程序函数中绘制元素，因此需要为设备上下文创建一个对象。最方便的类是 CClientDC，它派生自 CDC。如前所述，使用这个类而不是 CDC 的优点是，它会自动为你创建设备上下文，并在使用完毕后销毁它。它创建的设备上下文对应于窗口的客户区，这正是你所需要的。将以下代码添加到之前定义的框架处理程序中：

```
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
    // Define a Device Context object for the view
    CClientDC aDC(this);                 // DC is for this view
    aDC.SetROP2(R2_NOTXORPEN);           // Set the drawing mode
    if(nFlags & MK_LBUTTON)
    {
        m_SecondPoint = point;           // Save the current cursor position
        // Test for a previous temporary element
        {
            // We get to here if there was a previous mouse move
            // so add code to delete the old element
        }

        // Create a temporary element of the type and color that
        // is recorded in the document object, and draw it
        m_pTempElement = CreateElement(); // Create a new element
        m_pTempElement->Draw(&aDC);       // Draw the element
    }
}
```

## 第 14 章

新增的第一行代码创建了一个局部 `CClientDC` 对象。你传递给构造函数的 `this` 指针标识当前视图对象，因此 `CClientDC` 对象具有与当前视图客户区对应的设备上下文。除了我提到的特性外，这个对象还拥有你需要的所有绘图函数，因为它们继承自 `CDC` 类。你使用的第一个成员函数是 `SetROP2()`，它将绘图模式设置为 `R2_NOTXORPEN`。

要创建新元素，你要将当前光标位置保存在数据成员 `m_SecondPoint` 中，然后调用视图成员函数 `CreateElement()`。（你将在完成此处理程序后立即定义 `CreateElement()` 函数。）该函数应使用当前视图对象中存储的两个点，配合文档对象中存储的颜色和类型说明来创建一个元素，并返回该元素的地址。将其保存在 `m_pTempElement` 中。

使用指向新元素的指针，你调用其 `Draw()` 成员，让对象绘制自身。将 `CClientDC` 对象的地址作为参数传递。由于你在基类 `CElement` 中将 `Draw()` 函数定义为虚函数，因此会自动选择 `m_pTempElement` 所指向的任何元素类型对应的函数。新元素使用 `R2_NOTXORPEN` 正常绘制，因为这是你第一次在白色背景上绘制它。

你可以使用指针 `m_pTempElement` 作为是否存在先前临时元素的指示器。该处理程序此部分的代码如下：

```
void CSketcherView::OnMouseMove(UINT nFlags, CPoint point)
{
    // Define a Device Context object for the view
    CClientDC aDC(this);                  // DC is for this view
    aDC.SetROP2(R2_NOTXORPEN);            // Set the drawing mode
    if(nFlags&MK_LBUTTON)
    {
        m_SecondPoint = point;            // Save the current cursor position

        if(m_pTempElement)
        {
            // Redraw the old element so it disappears from the view
            m_pTempElement->Draw(&aDC);
            delete m_pTempElement;        // Delete the old element
            m_pTempElement = 0;           // Reset the pointer to 0
        }

        // Create a temporary element of the type and color that
        // is recorded in the document object, and draw it
        m_pTempElement = CreateElement();// Create a new element
        m_pTempElement->Draw(&aDC);      // Draw the element
    }
}
```

如果指针 `m_pTempElement` 不为零，则存在之前的临时元素。你需要重绘它指向的元素，以将其从视图客户区中移除。然后删除该元素并将指针重置为零。随后，之前添加的代码会创建并绘制新元素。这种组合会自动对正在创建的图形进行橡皮筋式绘制，使其看起来随着光标移动而附着在光标位置上。在创建最终版本的元素后，你一定不要忘记在 WM_LBUTTONUP 消息处理程序中将指针 m_pTempElement 重置为 0。

## 创建元素

你应该将 `CreateElement()` 函数作为受保护成员添加到 `CSketcherView` 类的“操作”部分：

```
class CSketcherView: public CView
{
    // Rest of the class definition as before...
    // Operations
    public:
    protected:
        CElement* CreateElement(void);    // Create a new element on the heap
    // Rest of the class definition as before...
};
```

为此，你可以直接修改类定义，添加阴影行；也可以在类视图中右键单击类名 `CSketcherView`，然后从上下文菜单中选择“添加 > 添加函数”。这将打开如图 14-19 所示的对话框。

![](img/2359b0c604600c58fba3539c738a356e_792_0.png)

图 14-19

