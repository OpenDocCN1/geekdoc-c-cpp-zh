
**响应式：** 一个花哨的词，用来表示你的网站除了在台式电脑上运行外，还能在手机和平板电脑上运行。通常，你需要编写额外的代码，使网站在这些不同屏幕尺寸上正确显示，但 Bootstrap 代码已经为你优化了这一点，如图 8-2 所示。

**跨浏览器兼容性：** Chrome、Firefox、Safari、Internet Explorer 和其他浏览器在渲染某些 HTML 元素和 CSS 属性时各不相同。Bootstrap 代码经过优化，因此无论使用哪种浏览器，你的网页都会显示一致。

![](img/5a907eb39993e80f28c82efc2e4632b3_134_0.png)

*图 8-2：* 使用 Bootstrap 针对桌面、平板和手机优化的《愤怒的小鸟：星球大战》页面。

## 安装 Bootstrap

按照以下两个步骤安装 Bootstrap 并将其添加到 HTML 文件中：

- 1. **在开始和结束的 `<head>` 标签之间加入以下代码行：**

    ```html
    <link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
    ```

`<link>` 标签引用托管在互联网上的 Bootstrap CSS 文件 3.2.0 版，因此此方法需要联网才能生效。

- 2. **在结束的 HTML `</body>` 标签之前立即加入以下两行代码。**

    ```html
    <!-- jQuery (needed for Bootstrap's JavaScript plugins) -->
    <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
    <!-- Bootstrap JavaScript plugin file -->
    <script src="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
    ```

![](img/5a907eb39993e80f28c82efc2e4632b3_134_1.png)

第一个 `<script>` 标签引用一个名为 jQuery 的 JavaScript 库。JavaScript 将在第 9 章介绍。虽然本书不介绍 jQuery，但从高层次来说，jQuery 简化了使用 JavaScript 执行的任务。第二个 `<script>` 标签引用 Bootstrap JavaScript 插件，包括下拉菜单等动画效果。如果你的网站不使用任何动画效果或 Bootstrap JavaScript 插件，则不需要包含此文件。

Bootstrap 可免费用于个人和商业用途，但需要包含 Bootstrap 许可证和版权声明。

如果你无法可靠地访问互联网，也可以下载并在本地托管 Bootstrap CSS 和 JavaScript 文件。为此，在解压 Bootstrap 文件后，使用 `<link>` 和 `<script>` 标签链接到本地版本的文件。访问 www.getbootstrap.com/getting-started/ 下载文件，并获取其他说明和示例。

## 了解布局选项

Bootstrap 允许你使用网格系统快速轻松地在页面上布局内容。使用此网格系统时有三个选项：

- **自己编写代码：** 学习网格组织方式后，可以编写代码创建任何想要的布局。
- **使用 Bootstrap 编辑器编写代码：** 无需在文本编辑器中编写代码，而是拖放组件和元素来生成 Bootstrap 代码。然后可以下载并使用此代码。
- **使用预构建主题编写代码：** 下载免费的 Bootstrap 主题，或购买已创建好网站的主题，然后填入自己的内容。

### 在网格系统中排列

Bootstrap 将屏幕划分为由 12 个等宽列组成的网格系统。这些列遵循几条规则：

- **各列宽度之和必须为 12 列。** 可以使用一个宽 12 列的列、12 个各宽 1 列的列，或介于两者之间的任何组合。
- **列可以包含内容或空白。** 例如，可以有一个宽 4 列的列、一个 4 列的空白，以及另一个宽 4 列的列。
- **除非另有指定，否则在较小的浏览器尺寸或手机等屏幕上，这些列会自动堆叠成单列；在较大的浏览器尺寸或笔记本电脑和台式机屏幕等屏幕上，则会水平展开。** 见图 8-3。

![](img/5a907eb39993e80f28c82efc2e4632b3_136_0.png)

**图 8-3：** 示例 Bootstrap 布局。

现在你已经了解这些布局在屏幕上的显示方式，让我们看看用于生成这些布局的示例代码。要创建任何布局，请遵循以下步骤：

- 1. 创建一个带有 `class="container"` 属性的 `<div>` 标签。
- 2. 在第一个 `<div>` 标签内，创建另一个带有 `class="row"` 属性的嵌套 `<div>` 标签。
- 3. 对于要创建的每一行，创建另一个带有 `class="col-md-X"` 属性的 `<div>` 标签。将 X 设置为希望该行跨越的列数。

例如，要让一行跨越 4 列，请写 `<div class="col-md-4">`。md 针对桌面设备的列宽，本节后面会展示如何针对其他设备。

![](img/5a907eb39993e80f28c82efc2e4632b3_136_1.png)

必须在页面开头包含 `<div class="container">`，并有一个结束的 `</div>` 标签，否则页面将无法正确渲染。

以下代码（如图 8-4 所示）创建一个简单的三列居中布局：

```html
<div class="container">
  <!-- Example row of columns -->
  <div class="row">
    <div class="col-md-4">
      <h2>Heading</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
        tempor incididunt ut labore et dolore magna aliqua. Ut enim ad
        minim veniam, quis nostrud exercitation ullamco laboris nisi ut
        aliquip ex ea commodo consequat
      </p>
    </div>
    <div class="col-md-4">
      <h2>Heading</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
      </p>
    </div>
    <div class="col-md-4">
      <h2>Heading</h2>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
      </p>
    </div>
  </div>
</div>
```

![](img/5a907eb39993e80f28c82efc2e4632b3_137_0.png)

**图 8-4：** 包含桌面版（左）和移动版（右）的 Bootstrap 三列布局。

要查看另一个示例，请访问 Codecademy 网站，并调整浏览器窗口大小。你会注意到，随着浏览器窗口变小，各列会自动堆叠在一起以便阅读。此外，各列会自动居中。如果不使用 Bootstrap，则需要更多代码才能实现相同的效果。

![](img/5a907eb39993e80f28c82efc2e4632b3_137_1.png)

你在上面看到的 Lorem ipsum 文本通常用于创建占位文本。虽然这些词没有实际含义，但这段引文源自公元前一世纪西塞罗的拉丁文文本。创建自己的网站时，可以使用 www.lipsum.org 或 www.socialgoodipsum.com 生成占位文本。

### 拖放到网站

看完上面的代码后，你可能想要一种更简单的方法来生成代码，而不必自己输入。Bootstrap 编辑器允许你拖放组件来创建布局，然后编辑器会生成供你使用的 Bootstrap 代码。

可以使用的 Bootstrap 编辑器包括：

- **LayoutIt.com：** 免费的在线 Bootstrap 编辑器（如图 8-5 所示），允许你拖放组件，然后下载源代码。
- **Jetstrap.com：** 付费的在线拖放式 Bootstrap 编辑器。
- **Pingendo.com：** 可免费下载的拖放式 Bootstrap 编辑器。
- **Bootply.com：** 免费的在线 Bootstrap 编辑器，内置可修改的模板。

![](img/5a907eb39993e80f28c82efc2e4632b3_138_0.png)

这些网站是免费的，可能会在没有通知的情况下停止工作。你可以使用任何搜索引擎搜索 Bootstrap 编辑器来找到更多选项。

![](img/5a907eb39993e80f28c82efc2e4632b3_138_1.png)

**图 8-5：** 带有拖放 Bootstrap 组件的 Layoutit.com 界面。

### 使用预定义模板

有些网站提供可直接使用的 Bootstrap 主题；你只需添加自己的内容。当然，如果愿意，也可以修改主题。其中一些 Bootstrap 主题包括：

- **Blacktie.co：** 免费的 Bootstrap 主题（如图 8-6 所示），全部由一位设计师创建。
- **Bootstrapzero.com：** 免费开源 Bootstrap 模板合集。
- **Bootswatch.com 和 bootsnipp.com：** 包含预构建的 Bootstrap 组件，你可以将它们组合用于自己的网站。
- **Wrapbootstrap.com：** 可购买的 Bootstrap 模板。
