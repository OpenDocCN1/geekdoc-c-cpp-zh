
## 边缘手势

正如我们在第 9 章“命令 UI”中所见，你不需要为应用栏或导航栏上的命令做任何特殊处理就能让它们显示出来：Windows 会自动处理从应用顶部和底部进行的边缘滑动，以及右键单击、Win+Z 和键盘上的上下文菜单键。话虽如此，你可以通过侦听 Windows.UI.Input.EdgeGesture 对象上的 starting、completed 和 canceled 事件，直接检测这些事件何时发生。

```
var edgeGesture = Windows.UI.Input.EdgeGesture.getForCurrentView();
edgeGesture.addEventListener("starting", onStarting);
edgeGesture.addEventListener("completed", onCompleted);
edgeGesture.addEventListener("canceled", onCanceled);
```

completed 事件会针对所有输入类型触发；starting 和 canceled 仅针对触摸发生。在这些事件中，eventArgs.kind 属性包含来自 EdgeGestureKind 枚举的值，用于指示调用该事件的输入类型。显然，starting 和 canceled 事件的 kind 始终是触摸，而 completed 可以是任何触摸、键盘或鼠标：

```
function onCompleted(e) {
    // Determine whether it was touch, mouse, or keyboard invocation
    if (e.kind === Windows.UI.Input.EdgeGestureKind.touch) {
        id("ScenarioOutput").innerText = "Invoked with touch.";
    }
    else if (e.kind === Windows.UI.Input.EdgeGestureKind.mouse) {
        id("ScenarioOutput").innerText = "Invoked with right-click.";
    }
    else if (e.kind === Windows.UI.Input.EdgeGestureKind.keyboard) {
        id("ScenarioOutput").innerText = "Invoked with keyboard.";
    }
}
```

上面的代码取自边缘手势调用示例的场景 1（js/edgeGestureEvents.js）。在场景 2 中，该示例还展示了你可以通过处理特定元素的 contextmenu 事件并在处理程序中调用 eventArgs.preventDefault，来阻止该元素发生边缘手势事件。它针对屏幕上的一个元素执行此操作，这样一来，当用鼠标右键单击该元素，或在该元素具有焦点时按下上下文菜单键，就会阻止边缘手势事件：

```
document.getElementById("handleContextMenuDiv").addEventListener("contextmenu", onContextMenu);

function onContextMenu(e) {
    e.preventDefault();
    id("ScenarioOutput").innerText = "The ContextMenu event was handled. The EdgeGesture event will not fire.";
}
```

请注意，此方法对通过触摸进行的边缘手势没有影响，也不会影响通常调用应用栏的 Win+Z 组合键。它主要是为了说明：如果你需要专门处理 contextmenu 事件，通常就会想要阻止边缘手势。

### 影响输入的 CSS 样式

既然我们在讨论输入，现在正好适合提一下若干会影响应用可能接收到的输入的 CSS 样式。

其中一种样式是 `-ms-user-select`，我们在第 3 章“应用剖析与性能基础”和第 5 章“控件与控件样式”中已经遇到过几次。此样式可以设置为以下值之一：

- `none` 禁用直接选择，不过如果元素的父级可选择，则整个元素仍可被选择。
- `inherit` 将元素的选择行为设置为与其父级匹配。
- `text` 即使父级设置为 `none`，也会启用文本选择。
- `element` 启用任意元素的选择。
- `auto`（默认值）可能会也可能不会启用选择，具体取决于控件类型和父级样式。对于不是文本控件且没有 `contenteditable="true"` 的元素，除非它包含在可选择的父级内，否则不可选择。

如果你想尝试这些变体，请参考使用 -ms-user-select CSS 属性的不可选内容区域示例，它拥有整个 Windows SDK 中第二长的 JavaScript 示例名称！

一种相关样式（但示例中未展示）是 `-ms-touch-select`，它可以是 `none` 或 `grippers`，后者是启用用于触摸的选择控件圆圈的样式：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_622_0.png)

可选择的文本元素会自动获得此样式，带有 `contenteditable = "true"` 的其他文本元素也是如此——`-ms-touch-select` 会将其关闭。要查看效果，请用上述名称很长的示例的场景 1 中的一些元素试一试！

在第 8 章“布局与视图”中，我们介绍了用于平移的吸附点（使用 `-ms-scroll-snap` 样式），以及用于缩放的吸附点，即 `-ms-content-zooming` 和 `-ms-content-zoom*`（参见触摸缩放和平移样式参考）。重要的是，`-ms-content-zooming: zoom`（与默认值 `none` 相对）会在相关元素允许 x 和 y 两个维度溢出的前提下，启用通过触摸和鼠标滚轮进行的自动缩放。这里在平移和缩放方面有许多变体，以及这些手势如何与 WinJS 控件交互。HTML 滚动、平移和缩放示例说明了详细信息。

最后，`touch-action` 样式为元素提供了若干选项。<sup>90</sup>

- `none` 禁用元素上的平移和缩放等默认触摸行为。当你想要直接控制触摸行为时，通常会在元素上设置此项。
- `auto` 启用常规触摸行为。
- `pan-x`/`pan-y` 元素允许水平/垂直触摸平移，该平移在最近的可水平/垂直滚动的祖先元素上执行，例如父级 `div`。
- `pinch-zoom` 在元素上启用双指缩放，该缩放在最近具有 `-ms-content-zooming: zoom` 和溢出能力的祖先元素上执行。例如，单独的 `img` 元素不会响应使用此样式的手势，但如果你将其放在设置了 `overflow` 的父级 `div` 中，它就会响应。
- `manipulation` 是 `pan-x` `pan-y` `pinch-zoom` 的简写等效项。

有关平移和缩放的示例，请尝试创建一个使用如下标记的简单应用（可使用任意图片）：

```html
<div id="imageContainer">
  <img id="image1" src="/images/flowers.jpg" />
</div>
```

并按如下方式设置容器样式：

```css
#imageContainer {
  overflow: auto;
  -ms-content-zooming: zoom;
  touch-action: manipulation;
}
```

<sup>90</sup> Windows 应用商店应用不支持双击缩放。另请注意，此样式较早的供应商前缀变体 `-ms-touch-action` 已被弃用，建议改用 `touch-action`。

### 存在哪些输入能力？

`Windows.Devices.Input` 命名空间中的 WinRT API 通过以下三个对象提供了有关当前设备可用能力的所有所需信息：

- `MouseCapabilities` 属性包括 `mousePresent`（0 或 1）、`horizontalWheelPresent`（0 或 1）、`verticalWheelPresent`（0 或 1）、`numberOfButtons`（一个数字）和 `swapButtons`（0 或 1）。
- `KeyboardCapabilities` 仅包含一个属性：`keyboardPresent`（0 或 1），它不表示屏幕键盘是否存在，屏幕键盘始终可用；`keyboardPresent` 具体表示物理键盘设备。
- `TouchCapabilities` 属性包括 `touchPresent`（0 或 1）和 `contacts`（一个数字）。就触摸而言，你可能还会对 `Windows.UI.ViewManagement.UISettings.handPreference` 属性感兴趣，它表示用户是惯用右手还是惯用左手。

要检查触摸是否可用，可以使用如下代码：

```
var tc = new Windows.Devices.Input.TouchCapabilities();
var touchPoints = 0;

if (tc.touchPresent) {
    touchPoints = tc.contacts;
}
```

**注意** 在 WinRT 不可用的 Web 上下文中，可以通过 DOM 元素上挂接的 msPointerEnabled、msManipulationViewsEnabled 和 msMaxTouchPoints 属性获取一些关于能力的信息。这些属性在本地上下文中也可用。尤其是 msPointerEnabled 标志，它会告诉你系统内可用硬件是否支持指针*事件。如果这些事件不受支持，你可以改用标准鼠标事件作为替代。

你会注意到，上面的能力信息没有涉及触笔或笔。对于这些设备，以及包括触摸和鼠标在内的所有指针设备的更详细信息，我们可以使用 Windows.Devices.Input.PointerDevice.getPointerDevices 方法。它返回一个 PointerDevice 对象数组，其中每个对象都有以下属性：

- **pointerDeviceType** 一个来自 PointerDeviceType 的值，可以是 touch、pen 或 mouse。
- **maxContacts** 设备可支持的最大接触点数——鼠标和触笔通常为 1，触摸则为任意其他数字。
- **isIntegrated** true 表示设备内置于机器中，因此可以依赖其存在；false 表示用户可能断开连接的外围设备。
- **physicalDeviceRect** 这个 Windows.Foundation.Rect 对象提供设备自身视角下的边界矩形。通常，触摸屏的输入分辨率实际上不会与屏幕像素匹配，这意味着输入设备无法精确命中一个像素。例如，在我的一台支持触摸的笔记本电脑上，对于 1366x768 像素的屏幕（如下面的 screenRect 所报告），此分辨率报告为 968x548。另一方面，鼠标通常与屏幕像素一一对应。这对于使用触笔的绘图应用可能很重要：输入分辨率小于屏幕意味着将输入坐标转换为屏幕像素时会存在一些不准确。
- **screenRect** 这个 Windows.Foundation.Rect 对象提供设备在屏幕上的边界矩形，也就是说，你应该会从设备事件中遇到的最小和最大坐标。此矩形会考虑多显示器系统，并会针对分辨率缩放进行调整。

