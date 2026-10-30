

void
MainForm::OnActionPerformed(const Osp::Ui::Control& source,
    int actionId)
{
    switch(actionId)
    {
    case ID_BUTTON_EDITFIELD_DONE:
        pScrollPanel->CloseOverlayWindow();
        pEditField->Draw();
        pEditField->Show();
        break;
    case ID_BUTTON_EDITFIELD_CANCEL:
        pEditField->SetText(*pEditFieldText);
        pScrollPanel->CloseOverlayWindow();
        pEditField->Draw();
        pEditField->Show();
        break;
    default:
        break;
    }
}

当按下“Done”按钮时，覆盖式键盘关闭并且编辑字段被重绘。当按下“Cancel”按钮时，存储在成员变量 pEditFieldText 中的原始文本字符串会被载入编辑字段，覆盖式键盘关闭并且编辑字段被重绘。

## Hints, Pitfalls, and Related Topics

ITextEventListener 接口接收文本事件，但它接收到的文本事件类型会根据其注册的 UI 控件类型而有所不同。例如，在方法 1 中，OnTextValueChanged() 方法在按下“Done”按钮时被调用，但在方法 2 中，它在光标在编辑字段内移动时每次都被调用。默认情况下，覆盖式键盘不会显示任何命令按钮。如果需要这些按钮，必须使用 SetOverlayKeypadCommandButton() 方法创建它们。

在为编辑字段初始化 ScrollPanel 对象时，ScrollPanel 的位置和大小参数应相对于 Form 可用客户端区域的左上角进行设置。因此，如果 Form 包含指示区域和/或标题区域，则在设置 ScrollPanel 的高度参数时应考虑这些区域的高度。如果这些值设置不正确，覆盖式键盘将不会显示在正确的位置。

要清除独立键盘中之前输入的任何文本，可以使用空字符串参数调用 SetText() 方法。

## Related Recipe

- Add a Form to a Frame-based App

# Recipe 2.7: Get Touch Events

## Problem Description

你想要从用户输入中获取触摸事件。

## The Recipe

本配方需要以下配置：

| Configuration | Value |
|---|---|
| **Namespaces used:** | `Osp::Ui`, `Osp::Ui::Controls`, additionally `Osp::Graphics` for graphics canvas drawing in the recipe |
| **Header files to #include:** | `FUi.h`, `FUiControls.h`, additionally `FGraphics.h` for graphics canvas drawing in the recipe |
| **Required libraries:** | `FUi`, `FUiControls`, additionally `FGraphics` for graphics canvas drawing in the recipe |
| **Required privilege level:** | `Normal` |
| **Required privilege groups:** | `None` |

bada 平台同时支持单点触摸和多点触摸用户输入。本配方详细说明了在 Form 中启用单点触摸用户输入的步骤，并描述了 Form 接收和处理触摸事件所需实现的代码。

本配方假设已按照“Add a Form to a Frame-based App”配方中的方法 2 的步骤将 Form 添加到应用程序的 Frame 中。

在本配方中，触摸屏用户输入由应用程序处理，并用于在图形画布上绘制线条（参见图 R2.8）。线条会跟随用户触摸输入的移动而在图形画布上绘制。双击触摸输入用于清除画布。

如“Add a Form to a Frame-based App”配方所示，MainForm 类继承自 Form 基类。为了使此 Form 能够处理来自触摸屏的事件，必须实现一个事件监听器接口。因此在本配方中，MainForm 类必须实现 `Osp::Ui::ITouchEventListener` 接口类。

![](img/a257d5fd53a79a244a20e587cd2f08f6_304_0.png)

Figure R2.8 Drawing lines with touch screen input.

以下代码片段显示了 MainForm 类定义的示例：

```
class MainForm :
    public Osp::Ui::Controls::Form,
    public Osp::Ui::ITouchEventListener
{
public:
    MainForm(void);
    ~MainForm(void);
    bool Initialize(void);

private:
    Osp::Graphics::Canvas* pDrawingCanvas;
    Osp::Graphics::Point* pStartPoint;

public:
    result OnDraw(void);
    result OnInitializing(void);
```

```
result OnTerminating(void);
void OnTouchPressed(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchLongPressed(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchReleased(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchMoved(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchDoublePressed(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchFocusIn(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
void OnTouchFocusOut(const Osp::Ui::Controls& source,
const Osp::Graphics::Point& currentPosition,
const Osp::Ui::TouchEventInfo& touchInfo);
);
```

为了接收触摸事件，MainForm 必须使用 AddTouchEventListener() 方法注册触摸事件监听器。

画布的创建和触摸事件监听器的注册应在 MainForm 初始化期间（OnInitializing()）执行：

- 1. 创建一个图形画布并根据可用的客户端区域设置其大小和位置。
- 2. 设置 MainForm 的背景颜色。
- 3. 设置绘图画布的背景颜色和前景颜色。
- 4. 设置绘图画布的线宽。
- 5. 清除绘图画布。
- 6. 创建一个 Point 对象以在绘制时存储触摸起始位置。
- 7. 注册由 MainForm 类实现的 ITouchEventListener。

以下代码片段是添加到 MainForm 的 OnInitializing() 方法中以创建图形画布并启用触摸事件处理的示例代码：

```
// Create a member canvas object, and set its size to the
// Form's client area
pDrawingCanvas = new Canvas;
pDrawingCanvas->Construct(GetClientAreaBounds());

// Set background colour of the Form
SetBackgroundColor(Color::COLOR_WHITE);

// Set the bg, fg colour and line width of canvas
```

```
pDrawingCanvas->SetBackgroundColor(Color::COLOR_WHITE);
pDrawingCanvas->SetForegroundColor(Color::COLOR_RED);
pDrawingCanvas->SetLineWidth(3);
pDrawingCanvas->Clear();

// Create an instance of a Point to store the touch start position
pStartPoint = new Point();
// Register touch event listener
AddTouchEventListener(*this);
```

由于本配方使用触摸事件在图形画布上创建自定义绘图，因此必须实现 OnDraw() 方法。GetCanvasN() 方法在 OnDraw() 实现中使用来检索 MainForm 使用的画布；否则 MainForm 的默认 Draw() 方法将覆盖自定义绘图。

在本配方中，OnDraw() 方法将绘图画布的内容复制到窗口画布；这是必要的，因为绘图操作实际上并未在 OnDraw() 方法中直接在 MainForm 的画布上执行：

```
result
MainForm::OnDraw(void)
{
    result r = E_SUCCESS;

    // Retrieve the window canvas
    Canvas* pWindowCanvas = GetCanvasN();

    if (pWindowCanvas)
    {
        // Copy the contents of the drawing canvas (where the
        // operations have been performed) to the window canvas
        pWindowCanvas->Copy(Point(GetClientAreaBounds().x,
            GetClientAreaBounds().y),
            *pDrawingCanvas, GetClientAreaBounds());
        delete pWindowCanvas;
    }

    return r;
}
```

显示将在调用 MainForm 的 Show() 方法时更新；这会在 OnDraw() 回调之后自动发生。

为了在触摸事件发生时处理它们，MainForm 必须实现以下方法：OnTouchDoublePressed()、OnTouchFocusIn()、OnTouchFocusOut()、OnTouchLongPressed()、OnTouchLongPressed()、OnTouchMoved()、OnTouchPressed() 或 OnTouchReleased()。每个方法都会传递有关事件源、当前位置、起始位置和事件状态的信息。

在本配方中，仅实现了 OnTouchPressed()、OnTouchMoved() 和 OnTouchDoublePressed() 方法。

