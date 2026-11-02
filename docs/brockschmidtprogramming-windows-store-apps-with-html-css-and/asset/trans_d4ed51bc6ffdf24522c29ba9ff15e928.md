
当屏幕空间更多时，你会希望采用自适应布局。

要实现固定布局，一开始就要围绕一个最小尺寸和固定的宽高比进行设计，例如 1024×768（4:3 宽高比）或 1366×768（16:9 宽高比）。<sup>72</sup> 然后，无论实际视图大小如何，都按照这些固定坐标系来编写代码。也就是说，把内容包进一个按固定尺寸设置样式的 `div` 中。为了能看清黑边效果，我还为 `body` 添加了背景色：

```
<!-- In markup -->
<div id="viewbox" class="fixedlayout">
<p>Content goes here</p>
</div>
```

```
/* In CSS */
body {
  background-color: #8e643c;
}
.fixedlayout {
  height: 768px;
  width: 1024px;
}
```

然后，为 `window.onresize` 事件添加监听器，并根据参考尺寸与实际尺寸之间的差值，对根元素应用 CSS 2D 缩放变换：

```
window.onresize = resizeLayout;

function resizeLayout(e) {
  var viewbox = document.getElementById("viewbox");

  var w = window.innerWidth;
  var h = window.innerHeight;
  var bw = viewbox.clientWidth;
  var bh = viewbox.clientHeight;
  var wRatio = w / bw;
  var hRatio = h / bh;
  var mRatio = Math.min(wRatio, hRatio);
  var transX = Math.abs(w - (bw * mRatio)) / 2;
  var transY = Math.abs(h - (bh * mRatio)) / 2;
  viewbox.style["transform"] = "translate(" + transX + "px," + transY + "px) scale(" + mRatio + ")";
  viewbox.style["transform-origin"] = "top left";
}
```

这样既能保持宽高比，也能把内容放大或缩小。变换中附带的平移会确保在固定内容未占用的四周区域中，`body` 的背景色仍然可见。

72 有些应用也许能调整自己的宽高比并填满整个窗口，但更常见的情况是宽高比保持不变，多余空间用黑边填充。另外请注意，WinJS 1.0 提供了一个 ViewBox 控件来实现这里展示的效果，但它在 WinJS 2.0 中被移除了，原因是它很少被使用，而且复制实现非常简单。

你可以在随书配套内容（companion content）的 FixedLayout 项目中找到相关示例。该应用会在画布上绘制一个 4×3 的圆形网格，如图 8-4 所示，以匹配 1024×768 的布局尺寸。在 1366×768 或更大、采用 16:9 宽高比的屏幕上，两侧会出现黑边；在 320px 的窄视图中（如清单中所设置），顶部会出现黑边。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_414_0.png)

**图 8-4** 使用简单的 CSS 变换进行固定布局缩放，在全屏 16:9 显示器（左）和 320px 窄视图（右）中显示黑边。

### 侧栏：位图图形与固定布局

如果在固定布局中使用位图图形，请按最大 2560×1440 分辨率准备它们，以便在最大的屏幕上看起来也很好，同时仍然能缩放到较小的屏幕（而不是被拉伸放大）。或者，你也可以通过不同的 `img.src` URL 加载更适合最常见屏幕尺寸的不同图形。

请注意，本章稍后讨论的分辨率缩放仍然适用。如果你运行在 10.6 英寸 2560×1440 的高密度显示器（180% 缩放）上，应用以及固定内容看到的屏幕尺寸仍然会更小。但如果你按设备原生分辨率提供图形，它在屏幕上渲染时会很清晰。

与固定布局（你始终看到相同的内容）相比，自适应布局是指视图在可用屏幕空间更多时显示更多内容。这类布局最容易用 CSS 网格实现：按比例设置的行和列会自动伸缩，网格单元内的元素也会随之调整大小。Visual Studio/Blend 项目模板演示了这一点，尤其是 Grid App 项目。在典型的 1366×768 显示器上，你只会看到少数几个项目，如图 8-5 顶部所示。切换到 27 英寸 2560×1440 显示器后，你会看到多得多的内容，正如图底部所示。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_415_0.png)

**图 8-5** Grid App 项目模板中的自适应布局，分别显示在 1366×768 显示器（上）和 2560×1440 显示器（下）上。

说实话，Grid App 项目模板并没有针对不同的视图大小做什么特别的事。因为它使用了 CSS 网格和按比例设置的单元格，包含 ListView 控件的单元格会自动变大。ListView 控件会自行监听 `window.onresize`，在拥有更多空间时自动重排以显示更多项目；我们无需直接告诉它。无论如何，Grid App 模板确实演示了基本策略：

-   尽可能使用 CSS 网格来自动处理自适应布局。
-   在必要时监听 `window.onresize`，手动重新定位并调整元素大小，例如 HTML `canvas` 元素。
-   让控件自行监听 `window.onresize`，从而直接进行自我调整。

作为另一个参考点，请参阅[使用 CSS 的自适应布局示例](#)。该示例确实采用了与 Grid App 项目模板相同的方法，依靠控件自行调整大小。在示例中，你会看到应用并没有基于视图大小做任何直接计算。

**提示** 如果你的自适应布局希望把 CSS 中指定的背景图片缩放到其容器（而不是平铺显示），请把 `background-size` 设置为 `contain` 或 `100% 100%`。

最后，我再次推荐文档中的[面向屏幕缩放的指南](#)主题，其中涉及更多设计问题，例如：

-   视图的哪些区域是固定的，哪些是自适应的？
-   自适应区域如何使用可用空间，包括该区域沿哪些方向进行自适应？
-   在线框图中，自适应区域和固定区域如何关联？
-   视图整体布局如何利用空间，也就是说，空白区域本身如何扩展，以免内容变得过于密集？这可能意味着在较窄的视图中收拢界面的某些区域，以在空间较少时降低密度。
-   视图如何使用多栏文本？

回答这类问题有助于你理解布局应该如何自适应。

## 处理屏幕方向

如果你用过任何带有加速度计的设备，就会知道最自然的操作之一是把设备向某个方向旋转 90 度，从而重新定向应用。在其他系统上，用户可以通过“电脑设置 > 电脑和设备 > 显示 > 方向”手动更改方向：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_416_0.png)

发生这种情况时，应用会收到一个 `window.onresize` 事件，并应据此更新其视图。这里的关键点是：横屏方向支持多个并排视图，但竖屏不支持。事实上，当多个应用并排显示时，Windows 会锁定屏幕方向。要切换到竖屏，请确保你要使用的应用单独以全屏方式运行。

如果为不同的视图状态恰当组织 CSS，并按需处理 resize 事件，你通常无需关心设备的实际物理方向，只需关心放置内容所需的视图大小。不过，你仍然可以通过多种方式确定物理方向。一种方式是通过前文“侧栏：ApplicationView 对象中的视图属性”中提到的 `ApplicationView.orientation` 属性。它的可能取值为 `portrait` 和 `landscape`。

更具体的值来自 `Windows.Graphics.Display.DisplayInformation` 类（通过 `DisplayInformation.getForCurrentView()` 获取）及其 `currentOrientation` 属性。该属性会标识设备相对于其原生方向可能处于的四个旋转象限之一：`landscape`、`portrait`、`landscapeFlipped` 和 `portraitFlipped`。如果需要，还有一个 `orientationChanged` 事件（其用法参见 `Display orientation sample` 中的场景 3）。

第三，`Windows.Devices.Sensors` 中的 API，具体来说是 `SimpleOrientationSensor` 和 `OrientationSensor` 类，可以提供来自硬件本身的更多信息，包括精确的旋转角度。这些内容将在第 12 章“输入与传感器”中介绍。

**注意** Internet Explorer 11 和 Windows 8.1 的应用宿主还通过 `msOrientation` 属性、`onmsorientationchange` 事件以及 `msLockOrientation` 和 `msUnlockOrientation` 方法，支持 `screen` 对象上的 W3C 方向标准。

当然，有些应用希望*不*让自己的视图因加速度计引起的旋转而调整大小。例如，全屏视频播放器希望无论设备方向如何都保持横屏，这样你就可以把平板支在椅子上，侧躺在沙发上观看视频。<sup>73</sup>

锁定方向可以在两个地方进行。首先，你可以在应用清单的“应用程序”标签页上的“受支持的旋转”（Supported Rotations）中指定应用支持的方向：

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_417_0.png)

默认情况下，这些选项全部未选中，这意味着当设备方向改变时，应用会调整大小（并因此重新绘制）；选中全部选项也表示相同含义。当你选中其中一部分选项时，会产生以下效果：

-   如果应用启动时设备不处于受支持的方向，应用会以最接近的受支持方向启动。例如，如果你同时选中“竖屏”和“横屏翻转”方向（我真不知道为什么你会选这个组合！），而设备处于横屏方向，应用将按竖屏启动。

73 类似电影播放器的应用除了锁定方向外，通常还需要在用户长时间未与系统交互时保持屏幕常亮。关于这一点，请参见 `Windows.System.Display.DisplayRequest` API。
