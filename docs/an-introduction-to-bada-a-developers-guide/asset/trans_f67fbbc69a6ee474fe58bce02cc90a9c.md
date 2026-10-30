

## 扩展UI和传感器

### 方案3.1：使用手势输入和运动UI

### 问题描述

您希望使用手势和运动事件来控制UI。

### 方案

本方案需要以下配置：

使用的命名空间：
Osp::UI, Osp::UI::Controls, Osp::UIx

需包含的头文件：
FUI.h, FUIControls.h, FUIx.h

所需库：
FUI, FUIControls, FUIx

所需特权级别：
普通（Normal）

所需特权组：
无

用户可以通过各种不同的手势（运动UI）与bada设备交互，还可以旋转屏幕，从而改变应用程序的方向。本方案详细说明了如何在应用程序中启用运动和方向控制，并描述了Form需要实现的代码，以便接收和处理运动及方向改变事件。

支持的运动事件类型有三种：

- 双击（Double-tap）：当设备的任何部分被敲击两次时发生。敲击使用加速度传感器，因此可以敲击设备的任何部分，包括屏幕。
- 摇动（Shake）：当设备快速来回移动多次时发生。摇动可能持续较长时间。为了准确捕获此行为，摇动的开始和结束会作为两个独立事件报告。
- 甩动（Snap）：当设备沿某一轴移动并返回时发生。

本方案假设已按照“向基于框架的应用添加Form”方案（可在第二组方案“UI基础”中找到）中的步骤，向应用程序的Frame中添加了一个Form。

在本方案中，将创建一个Flash动画并在屏幕上播放。用户可以通过运动事件控制动画的状态、可见性以及动画的大小和位置。

如“向基于框架的应用添加Form”方案所示，MainForm类继承自Form基类。为了让该Form处理运动和方向事件，必须实现运动和方向事件监听器接口。因此，在本方案中，MainForm类必须实现Osp::Ui::IMotionEventListener和Osp::Ui::IOrientationEventListener接口类。

以下代码片段展示了MainForm类定义的示例：

```
class MainForm :
    public Osp::Ui::Controls::Form,
    public Osp::Ui::IMotionEventListener,
    public Osp::Ui::IOrientationEventListener
{
public:
    MainForm(void);
    ~MainForm(void);
    bool Initialize(void);

protected:
    Osp::Ui::Motion* pMotion;

public:
    Osp::Ui::Controls::Flash* pFlash;

    result OnInitializing(void);
```

```
result OnTerminating(void);

void OnShakeDetected(Osp::Uix::MotionState motionState);
void OnDoubleTapDetected(void);
void OnSnapDetected(Osp::Uix::MotionSnapType snapType);

void OnOrientationChanged(const Osp::Ui::Control &source,
    OrientationStatus orientationStatus);
);
```

Flash动画的创建、运动和方向支持的启用，以及运动和方向事件监听器的注册，应在OnInitializing()方法中执行：

- 1. 创建一个运动对象。
- 2. 使用关联的监听器初始化运动对象。
- 3. 设置要启用的运动类型（例如双击、摇动和甩动）。
- 4. 创建一个Flash对象。
- 5. 构造Flash对象：设置控件的大小和位置、Flash播放样式以及SWF文件的文件名和路径。
- 6. 将Flash控件添加到MainForm。
- 7. 设置MainForm的方向（例如四方向方向样式）。
- 8. 绘制MainForm。

以下代码片段是添加到MainForm的OnInitializing()方法中的示例代码：

```
// Create Motion instance and set to detect all types of events
pMotion = new Motion();
pMotion->Construct(*this);
pMotion->SetEnabled(MOTION_TYPE_DOUBLE_TAP|MOTION_TYPE_SHAKE|
    MOTION_TYPE_SNAP);

// Create new Flash object
pFlash = new Flash();
pFlash->Construct(Rectangle(40, 40, 400, 400),
    FLASH_STYLE_PLAY_WITHOUT_FOCUS,
    String(L"/Res/Bada.swf"));

// Add flash object to form
AddControl(*pFlash);

// Set Orientation of the form
SetOrientation(ORIENTATION_AUTOMATIC_FOUR_DIRECTION);

// Register Orientation listener
AddOrientationEventListener(*this);

// Draw the controls
Draw();
Show();
```

为了开始Flash动画播放，必须调用Flash控件的Play()方法。如果应用程序需要立即播放，应在应用程序进入前台状态后调用Flash控件的Play()方法。在简单的应用程序中，可以通过在应用程序的OnForeground()方法中调用Flash控件的Play()方法来实现。如果不需要立即播放，可以在处理用户或系统事件时，由MainForm调用Flash控件的Play()方法。

以下代码片段是添加到应用程序的OnForeground()方法中以开始播放Flash控件的示例代码：

```
Frame *pFrame = GetAppFrame()->GetFrame();
MainForm *pForm = static_cast<MainForm*>(pFrame->GetCurrentForm());

pForm->pFlash->Play();
```

摇动运动通过IMotionEventListener::OnShakeDetected()方法报告给应用程序。在本方案中，摇动运动用于暂停或恢复Flash动画。当收到MOTION_ENDED通知时，根据当前动画状态暂停或恢复动画：

```
void
MainForm::OnShakeDetected(Osp::UiX::MotionState motionState)
{
    switch (motionState)
    {
    case MOTION_STARTED:
        AppLog("OnShakeDetected: Motion started\n");
        break;
    case MOTION_INPROGRESS:
        AppLog("OnShakeDetected: Motion in progress\n");
        break;
    case MOTION_ENDED:
    {
        AppLog("OnShakeDetected: Motion ended\n");
        if(pFlash->GetStatus() == FLASH_PLAYING)
            pFlash->Pause();
        else if(pFlash->GetStatus() == FLASH_PAUSED)
            pFlash->Resume();
    }
        break;
    default:
        break;
    }
    RequestRedraw();
}
```

双击运动通过IMotionEventListener::OnDoubleTapDetected()方法报告给应用程序。在本方案中，双击运动用于显示或隐藏Flash动画。当收到此事件时，根据当前状态显示或隐藏Flash控件：

```
void
MainForm::OnDoubleTapDetected(void)
{
    if(pFlash->GetShowState() == true)
        pFlash->SetShowState(false);
    else
        pFlash->SetShowState(true);

    RequestRedraw();
}
```

甩动运动通过IMotionEventListener::OnSnapDetected()方法报告给应用程序。在本方案中，甩动运动用于在屏幕上移动Flash动画或更改其大小。

当收到甩动事件时，会检查snapType参数以确定甩动运动发生的平面：

- 如果设备在x平面移动，则Flash动画的x坐标根据甩动方向（正或负）增加或减少20像素。
- 如果设备在y平面移动，则Flash动画的y坐标根据甩动方向（正或负）增加或减少20像素。
- 如果设备在z平面移动，则Flash动画的大小根据甩动方向（正或负）增加或减少20像素。

```
void
MainForm::OnSnapDetected(Osp::Uix::MotionSnapType snapType)
{
    Point currentPosition = pFlash->GetPosition();
    Dimension currentSize = pFlash->GetSize();
    switch(snapType)
    {
    case MOTION_SNAP_X_POSITIVE:
        pFlash->SetPosition(Point(currentPosition.x+20,
            currentPosition.y));
        break;
    case MOTION_SNAP_X_NEGATIVE:
        pFlash->SetPosition(Point(currentPosition.x-20,
            currentPosition.y));
        break;
    case MOTION_SNAP_Y_POSITIVE:
        pFlash->SetPosition(Point(currentPosition.x,
            currentPosition.y+20));
        break;
    case MOTION_SNAP_Y_NEGATIVE:
        pFlash->SetPosition(Point(currentPosition.x,
            currentPosition.y-20));
        break;
    case MOTION_SNAP_Z_POSITIVE:
        pFlash->SetSize(Dimension(currentSize.width+20,
            currentSize.height+20));
        break;
```

