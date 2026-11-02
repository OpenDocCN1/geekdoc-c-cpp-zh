
（即该浮出控件）。例如，App settings 示例中的场景 2 为其“帮助”命令定义了以下浮出控件（见 `html/2-SettingsFlyout-Help.html`，省略了文本内容并稍作格式化）；结果如图 10-6 所示：

```html
<div data-win-control="WinJS.UI.SettingsFlyout" id="helpSettingsFlyout"
    aria-label="Help settings flyout" data-win-options="{settingsCommandId:'help'}">
    <!-- Use either 'win-ui-light' or 'win-ui-dark' depending on the contrast between the
        header title and background color; background color reflects app's personality -->
    <div class="win-ui-dark win-header" style="background-color:#00b2f0">
        <button type="button" id="backButton" class="win-backbutton"></button>
        <div class="win-label">Help</div>
        <img src=".../images/smallTile-sdk.png" style="position: absolute; right: 40px;"/>
    </div>
    <div class="win-content ">
        <div class="win-settings-section">
            <h3>Settings charm usage guidelines summary</h3>
            <!-- Other content omitted -->
            <li>For more in-depth usage guidance, refer to the
                <a href="http://msdn.microsoft.com/en-us/library/windows/apps/hh770544">
                App settings UX guide</a>.</li>
        </div>
    </div>
</div>
```

与往常一样，`SettingsFlyout` 控件也有一些选项（这里只有一个 `settingsCommandId`，用途显而易见），以及几个适用的 `win-*` 样式类。适用的样式包括 `win-settingsFlyout`，它负责整个控件的样式，尤其是宽度和边框颜色；还有 `win-ui-light` 和 `win-ui-dark`，它们为浮出控件的内容应用浅色或深色主题。在本例中，我们为标题栏使用深色主题，而浮出控件的其余部分使用默认浅色主题，该主题继承自应用的全局样式表（即 `default.html` 引入 `ui-light.css`）。

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_549_0.png)

**图 10-6** App settings 示例场景 2 中的“帮助”设置浮出控件（垂直方向截断）。请注意底部的超链接。

如果上一节中的标记（连同图 10-6）已包含在当前加载到应用中的同一个 HTML 页面里，那么下面这行代码将显示该浮出控件：

```javascript
WinJS.UI.SettingsFlyout.showSettings("help");
```

在这种情况下，你还可以省略传给 `populateCommands` 的 JSON 对象中的 `href` 部分，但前提依然是：该浮出控件已经包含在当前 HTML 文档中。

通常更有意义的做法是，将设置浮出控件与其余标记分开，然后使用传给 `showSettings` 的 `page` 参数，传入应用包中某个页面的 URI。App settings 示例使用这种方式，为每个场景的浮出控件分别创建一个独立的 HTML 文件。你也可以把所有浮出控件放在同一个 HTML 文件中，只要它们的 id 唯一即可。无论采用哪种方式，`showSettings` 都会通过 `WinJS.UI.Pages.load`（它会调用 `WinJS.UI.processAll`）将该浮出控件的 HTML 加载到当前页面，扫描该 DOM 树以查找具有指定 `<id>` 的匹配浮出控件，然后将其显示出来。如果找不到该浮出控件，则会抛出异常。

App settings 示例中的场景 4 展示了这种编程式调用形式。这也是展示浮出控件如何垂直滚动的一个很好的例子（见图 10-7），相关代码见 `js/4-ProgrammaticInvocation.js`：

```javascript
WinJS.UI.SettingsFlyout.showSettings("defaults", "/html/4-SettingsFlyout-Settings.html");
```

![](img/0e8e4a2b6f953d3397e14e88cd5d8b4d_551_0.png)

**图 10-7** App settings 示例场景 4 中的设置浮出控件，展示了浮出控件如何支持垂直滚动；请注意顶部区域（左）和底部区域（右）的滚动条位置。

因此，`showSettings` 调用正是你在任何特定命令的 `invoked` 处理程序中所要使用的调用，也是 WinJS 在 `populateCommands` 中建立起来的机制。但这也意味着，当你想在代码中的任何其他位置显示特定设置窗格时，都可以调用 `showSettings`。

例如，如果在应用中遇到一个可以通过更改应用设置来解决的错误条件，你可以在消息对话框或通知浮出控件中提供一个按钮，调用 `showSettings` 来打开相应窗格。另外，该浮出控件的 `hide` 方法会将其关闭；它不会影响顶层的设置窗格，要关闭顶层窗格，必须使用 `Windows.UI.ApplicationSettings.SettingsPane.getForCurrentView().hide`。

实际上，如果需要导航到第三级设置窗格，你可能会将 `showSettings` 和 `hide` 结合使用。也就是说，你自己的某个设置浮出控件可以包含一个命令，该命令先对当前浮出控件调用 `hide`，再调用 `showSettings` 来调用另一个浮出控件。该次级浮出控件的返回按钮（它应该始终有返回按钮）也会以类似方式先对当前浮出控件调用 `hide`，再调用 `showSettings`，让第二级父窗格重新出现。不过，我们不建议把设置做得复杂到必须使用第三级浮出控件的程度；但如果你有特定场景确实需要这种能力，它也是可用的。

了解 `showSettings` 如何尝试查找浮出控件，也有助于以编程方式创建 `SettingsFlyout`。只要该控件在你使用其 id 调用 `showSettings` 时已存在于 DOM 中，WinJS 就能像处理其他浮出控件一样找到并显示它。使用一种混合方法也是可行的，不过我还没有尝试过，示例中也没有提供这种用法。由于 `showSettings` 会通过 `WinJS.UI.Pages.load` 把你指定的 HTML 页面作为页面控件加载，因此该页面也可以包含自己的脚本，并在其中定义一个带有 `processed`、`ready` 等方法的页面控件对象。在这些方法中，你可以对标记中定义的设置浮出控件进行特定的自定义。

### 侧栏：权限设置的更改

一个常见问题是，当用户在“权限”窗格中更改设置时，应用能否收到事件。答案是不能；也就是说，只有在你尝试使用某项功能并处理“拒绝访问”异常时，才会发现访问权限是否已被禁止。不过平心而论，你始终必须以妥善的方式处理功能被拒绝的情况，因为用户在你第一次使用 API 时就可以拒绝访问。发生这种情况时，你要再次显示一条关于已禁用权限的消息（如 Here My Am! 应用所示），并提供某种 UI 让用户重试该操作。但用户仍然需要手动调用“权限”设置。更多详情请参阅*访问个人数据的设备准则*，尤其是“如果对设备的访问被关闭怎么办？”一节。

## Here My Am! 更新

为了把本章涉及的一些主题串联起来，配套内容中包含了 Here My Am! 应用的又一次修订，改动和新增内容如下（除非另有说明，主要集中在 `pages/home/home.js`）：

- 现在它集成了 Bing Maps SDK，因此该控件是包的一部分，而不是从远程源加载。这消除了我们一直用来承载地图的 webview，因此 `html/map.html` 中的所有核心代码都可以移入 `js/default.js`，我们也不再需要应用与 webview 通信所需的代码。注意，要在 Visual Studio 中运行此示例，你需要自行下载并安装该 SDK（务必选择适用于 Windows 8.1 的版本）。
- 用相机拍摄的照片不再复制到应用数据，而是复制到“图片”库中的 HereMyAm 文件夹。已声明“图片库”功能。
- 不再保存最后一张捕获图像的路径名（该路径名用于应用终止并重新启动时），而是将 `StorageFile` 保存到 `Windows.Storage.AccessCache` 中，以保证将来的编程式访问。
- 新增了一个 appbar 命令，让你可以使用文件选择器选择要加载的图像，而不只依赖相机。如果需要，这也允许你使用相机应用。注意，在这种情况下，我们为选择器使用特定的 `settingsIdentifier`，以区别于最近图像所用的选择器。我们将在第 11 章再次了解文件选择器。
- 另一个 appbar 命令允许你从相机拍摄的最近照片中进行选择。它最初默认打开“图片”库，但使用不同的 `settingsIdentifier`，因此后续调用会默认打开上次查看的位置。
- 设置窗格中通过 `WinJS.Application.onsettings` 事件（见 `js/default.js`）增加了“关于”、“帮助”和“隐私声明”命令。前两个显示应用内部的内容，第三个则使用 webview 拉取 Web 内容；所有设置页面都位于项目的 html 文件夹中，样式位于 `css/default.css`。

## 本章学习要点

- 状态保持对 Windows 应用商店应用很重要，目的是即使在应用被挂起并终止后，也能在会话之间保持连续性。
- 应用数据是与应用本身绑定的会话、本地、临时和漫游状态；只有该应用本身可以访问。
- 用户数据存储在应用数据之外的其他位置（例如用户的音乐、图片和视频库，以及可移动存储），并且独立于任何特定应用而持久存在。多个应用可能可以打开和处理用户文件。
- WinRT 中的 `StorageFolder` 和 `StorageFile` 类是处理文件夹和文件的核心对象。事实上，对文件系统的所有编程式访问都从 `StorageFolder` 开始。`Windows.Storage.FileIO` 和 `PathIO` 类可以简化文件访问，`WinJS.Application` 中的辅助函数也是如此。

