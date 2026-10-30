

TOUCH_PRESSED 事件在用户触摸屏幕时发生。此事件在 MainForm 中由 OnTouchPressed() 方法处理。

在本教程中，OnTouchPressed() 方法用于将触摸起始位置 Point 对象设置为用户当前触摸的位置：

```
void
MainForm::OnTouchPressed(const Osp::Ui::Controls & source,
    const Osp::Graphics::Point& currentPosition,
    const Osp::Ui::TouchEventInfo & touchInfo)
{
    // Set the touch start position to the current position
    pStartPoint->SetPosition(currentPosition);
}
```

此触摸起始位置在 OnTouchMoved() 方法中用于绘制线条。

TOUCH_MOVED 事件在用户触摸屏幕并将手指在屏幕上移动时发生。第一次事件不会在用户移动若干像素后立即发送，以补偿不准确的触摸。在此余量之后，将为每个方向上两个像素或以上的移动发送事件。此事件在 MainForm 中由 OnTouchMoved() 方法处理。

在本教程中，OnTouchMoved() 方法用于从存储的触摸起始位置绘制一条线到当前位置：

```
void
MainForm::OnTouchMoved(const Osp::Ui::Controls & source,
    const Osp::Graphics::Point& currentPosition,
    const Osp::Ui::TouchEventInfo & touchInfo)
{
    // Draw a line from stored touch start point to current position
    pDrawingCanvas->DrawLine(*pStartPoint, currentPosition);

    // Draw the Form
    RequestRedraw();

    // Set the current position to the touch start point
    pStartPoint->SetPosition(currentPosition);
}
```

绘制线条后，触摸起始位置被设置为当前位置。这对于绘制正确表示用户在屏幕上移动的线条是必要的。传递给此函数的起始位置不能使用，因为它是用户触摸屏幕时的起始位置，而不是最后一次移动的起始位置。

TOUCH_DOUBLE_PRESSED 事件在用户在屏幕上双击时发生。此事件在 MainForm 中由 OnTouchDoublePressed() 方法处理。

在本教程中，OnTouchDoublePressed() 方法用于清除图形画布：

```
void
MainForm::OnTouchDoublePressed(const Osp::Ui::Controls source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo & touchInfo)
{
    // Clear the canvas
    pDrawingCanvas->Clear();

    // Draw the Form
    RequestRedraw();
}
```

## Hints, Pitfalls, and Related Topics

正如预期的那样，当用户触摸屏幕时，TOUCH_PRESSED 和 TOUCH_RELEASED 事件成对出现。这些事件也与 TOUCH_MOVED、TOUCH_LONG_PRESSED 和 TOUCH_DOUBLE_PRESSED 事件一起发生。在设计应用程序的事件处理时需要考虑这些事件序列。

移动触摸事件的事件序列为：
- 1. TOUCH_PRESSED
- 2. TOUCH_MOVED（多次）
- 3. TOUCH_RELEASED

长按触摸事件的事件序列为：
- 1. TOUCH_PRESSED
- 2. TOUCH_LONG_PRESSED
- 3. TOUCH_RELEASED

双击触摸事件的事件序列为：
- 1. TOUCH_PRESSED
- 2. TOUCH_RELEASED
- 3. TOUCH_DOUBLE_PRESSED
- 4. TOUCH_RELEASED

对于应用程序来说，仅在收到对应的 TOUCH_RELEASED 事件时才处理 TOUCH_PRESSED 事件可能是合适的。或者，应用程序也可以设计为如果在之后序列中收到 TOUCH_MOVED、TOUCH_LONG_PRESSED 或 TOUCH_DOUBLE_PRESSED 事件，则在 OnTouchPressed() 方法中完成的任何处理都会被撤销。在这两种情况下，都需要存储之前事件的状态。

建议不要在 OnTouchMoved() 方法中做太多处理，因为移动的灵敏度（两个像素）可能导致此方法被多次调用。

在本教程中，`GetCanvasN()` 方法在 `OnDraw()` 方法中使用来检索 `MainForm` 的画布。为了防止内存泄漏，如果方法名称以 'N' 为后缀，调用者必须在完成对返回实例的使用后删除该实例。

### Related Recipe
- Add a Form to a Frame-based App

## Recipe 2.8: Get Multi-touch Events

### Problem Description

你想要从用户输入中检索多个触摸事件。

### The Recipe

本教程需要以下配置：

**Namespaces used:**
`Osp::UI, Osp::UI::Controls, Osp::Graphics`

**Header files to #include:**
`FUI.h, FUIControls.h, FGraphics.h`

**Required libraries:**
`FUI, FUIControls, FGraphics`

**Required privilege level:**
`Normal`

**Required privilege groups:**
`None.`

bada 平台同时支持单点和多点触摸用户输入。本教程详细介绍了在 Form 中启用多点触摸用户输入的步骤，并描述了 Form 接收和处理多个触摸事件所需实现的代码（参见图 R2.9）。bada 平台支持同时检测和处理多达六个点²。

本教程假设已按照教程‘Get Touch Events’中详细说明的步骤启用触摸输入并处理触摸事件。

¹用于教程中的图形画布绘制。
²这可能因设备的硬件规格而异，有些可能不支持六个点。

在本教程中，触摸屏用户输入由应用程序处理，并用于在图形画布上绘制线条。线条会跟随用户触摸输入的移动而在图形画布上绘制。双击触摸输入用于清除画布。

![](img/a257d5fd53a79a244a20e587cd2f08f6_310_0.png)

图 R2.9 使用多点触摸输入绘制线条。

本教程仅详细说明对‘Get Touch Events’教程所做的更改，以启用多个触摸事件的处理。

在‘Get Touch Events’教程中，添加了一个类型为 Point 的成员变量指针来存储用于 TOUCH_MOVED 事件计算的上一个触摸位置。因为本教程将处理多个触摸点，所以将使用类型为 IList 的成员变量指针来存储每个点的事件信息：

```
Osp::Base::Collection::IList* pStartInfoList;
```

除了绘制代码的初始化和触摸事件监听器的注册之外，还需要修改 OnInitializing() 方法以为主 Form 启用多点触摸事件。

通过创建 Touch 对象的实例并使用 SetMultipointEnabled() 方法启用它，可以为 MainForm 控件启用多点触摸。

以下代码片段是添加到 MainForm 的 OnInitializing() 方法中的示例代码，用于初始化事件位置信息指针并启用多点触摸：

```
// Initialise list pointer
pStartInfoList = null;

// Enable multi-point touch
Touch touch;
touch.SetMultipointEnabled(*this, true);
```

在本教程中，只有 OnTouchPressed() 和 OnTouchMoved() 事件处理方法与‘Get Touch Events’教程相比有所修改。

如‘Get Touch Events’教程所述，每个事件处理方法都会传递有关触摸事件的位置和状态的信息，并且可以使用这些参数来实现所需的功能。在本教程中，可以忽略这些参数，因为它们仅包含有关单个触摸点的信息，而不包含所需的多点触摸信息。

为了检索多个触摸点的信息，需要创建一个 Touch 对象的实例。Touch 对象提供了一个 GetTouchInfoList() 方法，该方法返回 MainForm 控件的多点触摸位置列表，每个位置由一个 TouchInfo 对象表示。

在‘Get Touch Events’教程中，OnTouchPressed() 方法被实现为将当前触摸位置存储到触摸起始位置 Point 对象中。在本教程中，多点触摸位置的列表存储在事件位置信息 IList 成员变量中。此列表中的每个项的类型为 TouchInfo：

```
void
MainForm::OnTouchPressed(const Osp::Ui::Controls& source,
    const Osp::Graphics::Point& currentPosition,
    const Osp::Ui::TouchEventInfo & touchInfo)
{
    Touch touch;

    // Set the start info list to the current touch info list
    pStartInfoList = touch.GetTouchInfoList(source);
}
```

在‘Get Touch Events’教程中，OnTouchMoved() 方法被实现为从存储的触摸起始位置绘制一条线到当前位置。在本教程中，OnTouchMoved() 方法实际上做的是同样的事情

