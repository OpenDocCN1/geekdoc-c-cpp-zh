

## 第一部分：入门 3ds Max

## 第 4 章：自定义 Max 界面和设置首选项

要指定单位系统，请选择 Customize ▸ Units Setup 以显示 Units Setup 对话框，如图 4.19 所示。对于 Metric 系统，选项包括 Millimeters、Centimeters、Meters 和 Kilometers。U.S. Standard 单位系统可以设置为默认单位 Feet and Inches，以小数或分数单位显示。您还可以选择以分数英寸显示英尺，或以小数英寸显示英尺。分数值可以从 1/16 到 1/256 的增量进行划分。

**FIGURE 4.19** The Units Setup dialog box lets you choose which units system to use. Options include Metric, U.S. Standard, Custom, and Generic.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_170_0.png)

### 使用 Custom 和 Generic 单位

要定义 Custom 单位系统，请修改 Custom 选项下的字段，包括单位标签及其与已知单位的等价关系。最后的选项是使用默认的 Generic 单位。Generic 单位将距离相互关联，但数字本身无关紧要。您还可以将照明单位设置为使用 American 或 International 标准。照明单位用于定义 Photometric 灯光。

在 Units Setup 对话框顶部是 System Unit Setup 按钮。此按钮打开 System Unit Scale 对话框，也显示在图 4.19 中。此对话框使您能够定义 Max 使用的测量系统。选项包括 Inches、Feet、Miles、Millimeters、Centimeters、Meters 和 Kilometers。

例如，当使用 Max 创建要在 Unreal 游戏编辑器中使用的模型时，您可以使用 Custom 选项定义一个名为 Unreal Foot 单位的单位，将 1 Uft 设置为等于 16 个单位，这与 Unreal 编辑器中的单位完全匹配。

Multiplier 字段允许您更改每个单位的值。Respect System Units in Files 切换按钮会在遇到系统单位设置不同的文件时弹出对话框。如果禁用此选项，所有新对象都会自动转换为当前单位系统。

Origin 控制有助于您确定对象远离场景原点移动时的准确性。如果您知道对象将位于原点多远的位置，则输入该值即可告诉您 Resulting Accuracy。您可以使用此功能来确定参数的准确性。距离原点越远的对象准确性越低。

**Caution**

在处理位于场景原点很远处的对象时要谨慎。对象距离原点越远，其准确性越低，您移动它的精确度也越低。如果您在精确放置对象时遇到困难（尤其是从外部文件导入的对象），请检查对象与原点的距离。将其移近原点应该有助于解决问题。

### 处理单位不匹配

想象一下设计一个新的滑雪度假村布局。对于此类项目，您可能希望使用公里作为文件单位。如果您的下一个项目是为赛车设计定制的车身设计，那么您将希望使用米作为新的单位。如果您需要在单位设置为米时重新打开滑雪度假村项目，则会收到 File Load: Units Mismatch 对话框，如图 4.20 所示。

**FIGURE 4.20** The Units Mismatch dialog box lets you synch up units between the current file and the system settings.

![](img/ebbb4844f027f7d1c580e48108d2b6cb_171_0.png)

此对话框提醒您，正在打开的文件中指定的单位与当前单位设置不匹配。在尝试合并具有不同单位设置的对象时也会发生这种情况。对话框列出了文件和系统中使用的单位，并提供两个选项。Rescale the File Objects to the System Unit Scale 选项会将文件中的单位更改为与当前系统单位设置匹配。第二个选项会将系统单位更改为与文件单位设置匹配。

**Tip**

如果您将文件对象重新缩放以匹配系统文件单位设置，则对象在当前场景中可能会显得非常小或非常大。使用 Zoom Extents All 按钮可在视口中查看重新缩放的对象。

### 重新缩放世界单位

如果您在场景进行到一半时发现自己使用的是错误的单位，可以使用 Rescale World Units 实用工具来缩放整个场景或仅选定的对象。要访问此实用工具，请单击 Utilities 面板，然后单击 More 按钮。在实用工具列表中，选择 Rescale World Units 实用工具并单击 OK。

Rescale World Units 对话框具有 Scale Factor 值，即场景或对象增加或减少的数值。如果您的世界使用毫米单位创建，而您需要在米中工作，则增加 Scale Factor 1000 将使世界恢复正常。

### 设置首选项

Preference Settings 对话框让您可以配置 Max 以最舒适的方式工作。您可以通过选择 Customize ▸ Preferences 打开它。对话框包含多个面板：General、Files、Viewports、Gamma and LUT、Rendering、Animation、Inverse Kinematics、Gizmos、MAXScript、Radiosity、mental ray 和 Containers。

**Tip**

我发现打开 Preference Settings 对话框最快的方法是右键单击主工具栏上的 Spinner Snap Toggle 按钮。

### General 首选项

Preference Settings 对话框中的第一个面板是 General 设置，如图 4.21 所示。General 面板包含许多影响整个界面的全局设置。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_172_0.png)

General 面板让您可以更改许多 UI 设置。

**Undo Levels 和 Reference Coordinate System**

Scene Undo 旋转器设置可以保留在缓冲区中以供撤销的命令数量。较小的数字可以释放内存，但无法让您回溯到工作中的更远位置。默认 Undo Levels 为 20。

**Tip**

虽然会占用一些宝贵的内存，但我发现增加撤销次数非常有帮助。在建模时，执行 20 个命令几乎不需要时间。

Reference Coordinate System 设置使所有变换工具在启用 Constant 选项时使用相同的坐标系统和变换中心。如果禁用，每个变换（移动、缩放和旋转）都会使用最后选择的坐标系统。

**加载 Plug-Ins 和 Sub-Material 设置**

Load Plug-Ins When Used 选项会将插件保留在内存之外，直到访问它们为止。这可以节省宝贵的内存，同时仍可访问插件。

当选中 Automatic Sub-Material Assignment 选项时，可以将材质直接拖放到子对象选择上。这会将 Multi/Sub-Object 材质应用于对象，其中拖放的材质对应于子对象选择的 Material ID。如果您经常使用 Multi/Sub-Object 材质，启用此选项可以大大节省时间，但如果您不熟悉 Multi/Sub-Object 材质，此选项可能会导致混淆，使定位已应用的材质变得困难。

**Scene Selection 设置**

Auto Window/Crossing by Direction 选项允许您同时使用窗口方法（整个对象必须在选定的窗口区域内才会被选中）和交叉方法（当鼠标与对象边界交叉时选择对象）来选择场景对象，具体取决于鼠标拖动的方向。如果您选择第一个选项，则当鼠标从右向左拖动时使用 Crossing 方法，当鼠标从左向右拖动时使用 Window 方法。

**Tip**

我喜欢保持 Auto Window/Crossing by Direction 选项禁用。我使用 Crossing 选择方法，发现我并不总是从同一侧开始选择。

Paint Selection Brush Size 值设置 Paint Selection Brush 的默认大小。在默认界面中，此大小设置为 20。如果您每次使用此工具时都发现自己在更改画笔大小，则可以使用此设置更改其默认大小。

**Spinner、Rollout 和 Vertex Normal 设置**

Spinners 是界面控件，可让您输入值或通过单击右侧的箭头交互式地增加或减少值。Preference Settings 对话框包含用于更改 Spinner 中显示的小数位数以及单击箭头时的增量或减量值的设置。Use Spinner Snap 选项启用吸附模式。

您还可以使用主工具栏上的 Spinner Snap 按钮启用吸附模式。

**Tip**

右键单击 Spinner 可自动将其值设置为 0 或其最低阈值。

您还可以通过单击 Spinner 并向上拖动来增加值，向下拖动来减小值来更改 Spinner 中的值。Wrap Cursor Near Spinner 选项在您通过鼠标拖动更改值时使光标保持靠近 Spinner 附近，这样您就可以连续拖动鼠标，而不必担心碰到屏幕顶部或底部。

Rollout Threshold 值设置在滚动条移动到另一列之前可以滚动的像素数。这仅在您使 Command Panel 更宽或浮动时使用。

Use Legacy R4 Vertex Normals 选项基于 Max 版本 4 而不是更新的方法来计算顶点法线。更新的方法更准确，但可能会影响平滑组。仅在计划使用使用 Max R4 或更早版本创建的模型时才启用此设置。

