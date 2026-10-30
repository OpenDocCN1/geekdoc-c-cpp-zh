

虽然没有真正设备的上手体验可以替代，但以下 bada 设计要点值得牢记：

- Touch – 基于手指的直接操作，包括多点触控、捏合和滑动，当然还有触觉反馈。
- Simplicity – 简单的屏幕布局、相对较大且粗体的字体、用于交互的大型 GUI 元素、简单的大图标、有限的自定义、简单的菜单。
- Bright and bold – 充分利用 superAMOLED 显示技术，高对比度、鲜艳的色彩、饱和的黑色（顺便说一下，由于 AMOLED 技术中暗像素比亮像素消耗更少电量，因此更偏好深色配色方案而非浅色）。
- Extended user input – 除了触控和硬键之外，触控 UI 还支持手势（包括敲击机身、旋转手机、快拍和摇晃等物理动作），甚至面部检测。
- Multiple display sizes and resolutions – WVGA（宽 VGA）480 × 800，WQVGA（宽四分之一 VGA）240 × 400。

您可以在 SDK Help 中找到详细的 UI 指南。在 IDE 中选择 Help | Help Contents | bada Application UI Guide。

### 2.2.1 Frames, Forms, and Controls

GUI 不仅仅是你屏幕上看到的内容。bada 的触控 UI 风格的简洁性延伸到了其下方的架构，以及驱动架构的概念。虽然 bada 不会为你设计 GUI，但它确实为你的应用提供了一个简单且标准化的 GUI 架构供使用。

你可以将应用中显示的一切视为组织在一个分层树中。树的根是应用 Frame。在每个应用中，Frame 都是所有 GUI 元素添加到的顶级容器。更正式地说，Frame 类封装了设备显示，并扮演应用顶级窗口的角色，每个应用恰好只有一个。所有应用都有一个 Frame，你无需做任何事情来创建或设置它。框架已全部处理好。

标准控件由框架预先制作，或你自己的派生自定义控件。Control 类抽象了一个屏幕区域，既用于显示也用于捕获输入。

自然地，bada 提供了全面的图形原语、位图、动画和字体，因此这里的真正限制只是你的想象力——以及你的设计技巧！⁴ Frames、Forms 和 Controls 之间的关系如图 2.8 所示。

> ⁴在底层，bada 图形功能所需的原始算力基于 OpenGL ES，支持 2.0（硬件加速和硬件着色器）和 1.1 标准（仅硬件加速）。可用的 OpenGL ES 版本取决于设备。也有可能在低端，一些 bada 手机根本不支持 OpenGL ES。需要 OpenGL ES 的应用将无法安装在缺乏相应支持的手机上。

![](img/a257d5fd53a79a244a20e587cd2f08f6_54_0.png)

Figure 2.8 All applications have a Frame, the top level container within which Forms are added; Forms are populated with Controls.

### 2.2.2 Standard Elements of a Form – Indicator Bar, Title Bar, Soft Keys, Option Menu

Form 占据手机的整个物理显示区域——屏幕上所有可见内容。因此 Form 还可选择性地包含一些标准系统元素（见图 2.9）。这些是

- 显示在显示区域顶部的 Indicator bar，用于显示系统图标（如信号和电池强度）和通知（如你是否有未读消息）。
- Title bar，可显示字符串。
- 显示在主显示底部命令区域的 Soft keys。
- Option menu key，显示在显示区域底部软键之间，用于启动 Option menu。

系统元素被定义为 Form 的属性。是否显示全部或部分元素由每个 Form 决定，因此受定义该 Form 的应用控制。然而，它们的样式和外观（对于 Indicator bar 来说，其内容也是如此）并非由应用直接控制。尽管 Form 显示系统元素，但框架保留对其的控制权。

![](img/a257d5fd53a79a244a20e587cd2f08f6_55_0.png)

**Figure 2.9** The application name and standard system elements.

### 2.2.3 Handling Events

我们说过每个 Control 派生类都抽象了一个屏幕区域，既用于显示也用于输入，但我们没有说如何实现。输入事件包括来自触摸屏的输入，包括菜单和软键，来自物理手机按键包括侧键如锁定和相机，来自手势和原始传感器事件，来自 bada 系统事件——可能来自*任何*类型的事件。

Listeners 是将行为与 bada 应用中的呈现绑定在一起的粘合剂。在 bada 中，监听器提供了所有事件处理的机制。任何时候，GUI 中恰好有一个控件具有*焦点*。*焦点*只是指哪个对象正在主动更新显示并接收用户和系统事件。从概念上讲，焦点属于当前正在运行的前台应用的当前活动控件。该控件接收发生的任何输入事件（顺便说一下，也会启动重绘显示）。

每个控件都有内置的监听器，用于其识别的基本事件类型。根据控件的不同，这些可能包括以下任何一种：

- Focus events
- Key events
- Touch events
- Drag and drop events

## The BuddyFix UI

BuddyFix 是一个简单的应用，实现了简单的用例。它使用户能够与好友列表定期共享更新的位置信息，以便实时汇聚到一个会面地点。为此，BuddyFix 使用 bada 提供的 Buddy 服务作为服务 API。

BuddyFix 显示好友列表，对每个好友显示以下信息：

- picture;
- name;
- location fix, i.e. last known location;
- time fix, i.e. time of last location fix;
- location status, on or off the grid, i.e. currently reachable or not;
- whether location sharing is enabled for this buddy.

此外 UI 还必须提供以下信息：

- whether sharing is paused or active at application level;
- interval at which location fixes are updated.

Points to note:

- Location sharing is always in both directions.
- Location fixes are therefore always updated in both directions.
- Application-level pausing of location sharing allows power to be saved.
- Location display format should be user selectable.
- Location sharing is periodic not continuous, and is scheduled according to the update interval.
- The update interval should be user selectable.
- The update interval applies to all buddies.
- Individual buddies are added from the phone Contacts app.
- Friends must already be buddies on the Buddy service to be allowed by BuddyFix.

显然，以上一些限制使应用无法完全功能化，但就当前目的而言，它们使复杂性保持在可控范围内。

UI 必须启用以下操作：

- Add/Remove a buddy.
- Start/Stop sharing, for some buddy.
- Nudge now, share a location fix with some buddy now, without waiting for the next scheduled update.
- Set the update interval.
- Pause/Unpause all sharing.

那么让我们开始吧。我们将定义一个单一的 MainListForm 作为基本应用屏幕，所有功能都将从这里可用。通过 Eclipse 主菜单栏选择 Window | Show View | Other 启动 Resource Explorer，如图 2.10 所示。

![](img/a257d5fd53a79a244a20e587cd2f08f6_58_0.png)

Figure 2.10 Launching the Resource Explorer.

Resource Explorer 面板将在 IDE 中打开。（如果启动时为空，请确保在 Project Explorer 面板中已选择你的项目。）在 Resource Explorer 中任意位置右键单击并选择 Open Insert Wizard，如图 2.11 所示。我们要创建一个新的 Form，因此选择 Create Form File，然后 Finish。Resource Explorer 面板中会出现一个新的 Form。双击以启动 WYSIWYG UI Builder，你应该会看到如图 2.12 所示的屏幕。请注意，默认 Form——出于演示目的——已包含一个 Button 控件，你可以使用它或直接删除。当 UI Builder 面板启动时，双击主 Form 面板以打开如图 2.13 所示的 Form Properties 面板。

### 2.3.2 Form Properties

在做任何其他事情之前，让我们先将 Form 名称更改为有意义的名称。属性是简单的名称、值对。要编辑属性，请在属性列表中双击属性名称并更改关联的值。对于 BuddyFix，我们保留 'IDF' 前缀和全大写的资源命名约定以在代码中提供清晰度，并将 Form 命名为 IDF_MAIN_LIST_FORM。

