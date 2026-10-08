

| CONTROL | DESCRIPTION |
| :--- | :--- |
| DropShadowExtender | 此扩展器为 ASP.NET Panel 控件应用阴影。该扩展器允许你指定阴影的宽度、透明度以及阴影是否应具有圆角。对于允许用户移动或调整面板大小的页面，DropShadowExtender 具有一种模式，可以在运行时调整阴影的大小并重新定位，以匹配目标面板。 |
| DynamicPopulateExtender | 此扩展器用 Web 服务或页面方法调用的结果替换控件的内容。方法调用返回一个 HTML 字符串，该字符串将作为目标元素的子元素被插入。 |
| FilteredExtender | 这是一种扩展器，允许用户仅在文本框中输入你定义的字符，或者防止用户输入你指定的字符。 |
| HoverMenuExtender | 这是一个可以附加到任何 .NET WebControl 的扩展器，它会将该控件与一个弹出面板关联，以显示额外内容。当用户将光标移动到主控件上时，会发生两件事：弹出面板将在页面开发者指定的位置（主控件的左侧、右侧、顶部或底部）显示。可选情况下，会对控件应用 CSS 样式将其指定为“热点（hot）”。 |
| Editor | 此控件允许你轻松创建和编辑 HTML 内容。工具栏中的各种按钮用于内容编辑。你可以查看生成的 HTML 标记和预览文档。 |
| ListSearchExtender | 此扩展器通过输入字符来选择 ListBox 或 DropDownList 中的项。该扩展器根据已输入的内容在 ListBox 内进行增量搜索。点击列表时显示的提示消息可以自定义，同时同时其 CSS 类和位置也可以自定义。 |

## 表 20-1（续）

| CONTROL | DESCRIPTION |
| :--- | :--- |
| MaskedEditExtender | 此扩展器附加到 TextBox 控件上以限制可以输入的文本类型。MaskedEditExtender 对输入应用一个“掩码”，仅允许输入特定类型的字符。支持的数据格式有数字（Number）、日期（Date）、时间（Time）和日期/时间（DateTime）。MaskedEditExtender 使用 CultureName 中指定的区域设置。如果未指定，则区域设置将与页面相同。 |
| ModalPopupExtender | 此扩展器允许你在模拟对话框的元素中显示内容，从而防止用户与页面的其余部分进行交互。模态内容可以包含任何层次结构的控件。它显示在背景（z 轴顺序）之上，背景可以应用自定义样式。 |
| MultiHandleSliderExtender | 此扩展器为普通的 TextBox 控件提供了功能丰富的扩展。它允许你通过图形化滑块界面选择单个值或范围内的多个值。它支持一个句柄，或任何绑定到 TextBox 或 Label 控件值的任意数量句柄。它还提供了只读访问、自定义样式和拖动句柄的选项，以及用于辅助功能的鼠标和键盘支持。 |
| MutuallyExclusiveExtender | 此扩展器可以附加到任何 CheckBox 控件。通过向同一个“键（Key）”添加多个复选框，每次只能有一个指定键的复选框被选中。此扩展器在有多个选择但只能选择一个时（类似于单选按钮）非常有用。然而，使用复选框允许你取消选中某个值，这在单选按钮中通常是不行的。与使用 JavaScript 允许取消 RadioButton 项目相比，这还提供了一个更一致且符合预期的界面。 |

| CONTROL | DESCRIPTION |
| :--- | :--- |
| NoBot | 此控件尝试在不需要任何用户交互的情况下提供类似于 CAPTCHA 的机器人/垃圾邮件防护。这种方法比需要实际人工干预的实现更容易绕过，但 NoBot 的优点是完全不可见。NoBot 可能适用于博客垃圾邮件是问题且不需要 100% 有效的低流量站点。 |
| NumericUpDownExtender | 这是一种可以附加到 TextBox 控件的扩展器，用于添加“向上”和“向下”按钮，以增加或减少 TextBox 中的值。增加和减少的操作可以是简单的 +/-1 算术运算。它们可以在提供的值列表（如年份月份）之间循环，也可以调用 Web 服务来确定下一个值。页面作者还可以提供自定义图像来代替默认的向上/向下按钮。 |
| PagingBulletedListExtender | 此扩展器可以附加到 BulletedList。该扩展器为项目符号列表提供分页功能。你可以自定义每页页显示的项目数量以及页面导航控件的外观。 |
| PasswordStrength | 这是一种可以附加到 TextBox 的扩展器，在用户输入密码时显示密码强度。它提供了一个显示密码强弱的视觉指示器。 |
| PopupControlExtender | 此扩展器允许你在控件上方显示弹出窗口。弹出窗口可以包含任何层次结构的控件，并相对于目标控件进行定位。它通过各种事件或程序化触发。 |

## 表 20-1（续）

| CONTROL | DESCRIPTION |
| :--- | :--- |
| Rating | 此控件允许用户使用一组星形对项目进行评分。你可以自定义星的数量、范围以及星形的外观。 |
| ReorderList | 此控件允许用户通过拖放重新排列列表中的项。它提供了一种管理列表顺序的直观方式。 |
| ResizableControlExtender | 这是一种可以附加到任何控件的扩展器，使其可以调整大小。它提供了一个句柄，用户可以通过拖动句柄来更改目标控件的宽度高度。 |
| RoundedCornersExtender | 此扩展器为控件应用圆角。你可以指定角的半径和边框颜色。 |
| SeaDragon | 此控件允许用户对图像进行平和平缩放。它提供了导航高分辨率图像的控件。 |
| SliderExtender | 这是一种可以附加到 TextBox 的扩展器，允许用户从范围内选择值。滑块可以是水平的或垂直的，也可以作为离散滑块使用。 |

| CONTROL | DESCRIPTION |
| :--- | :--- |
| SlideShowExtender | 这是一个针对图像控件的扩展器。你可以为它提供“上一个”、“下一个”和“播放”按钮。你可以配置幻灯片在渲染时自动播放，允许它循环播放，并设置幻切换的间隔。你可以使用页面方法为幻灯片提供图像。 |
| TabContainer | 这是一个创建一组标签页的控件，可用于组织页面内容。TabContainer 是多个 TabPanel 控件的容器。 |
| TextBoxWatermarkExtender | 此扩展器可以附加到 TextBox 以获得水印行为。当带有水印的 TextBox为空时，它会使用自定义 CSS 样式向用户显示消息。一旦用户在 TextBox 中输入文本，该显示就会消失。水印的典型目的是向用户提供更多关于 TextBox 本身的信息，而不会弄乱页面其他部分。 | ToggleButtonExtender | 此扩展器可以附加到 CheckBox 控件。ToggleButtonExtender 允许使用自定义图像显示 CheckBox 的状态。CheckBox 的行为不受影响。 |
| UpdatePanelAnimationExtender | 这是一个简单的扩展器，允许你以简单、装饰性的在现有页面利用强大的动画框架。它用于在 UpdatePanel 更新期间以及更新完成后播放动画。 |
| ValidationCalloutExtender | 此扩展器增强了现有 ASP.NET 验证器的功能。要使用此项，请像往一样添加输入字段和验证器控件，并向其附加 ValidationCalloutExtender。 |

# 新服务器控件

AjaxControlToolkit.dll 向工具箱添加了多个 ASP.NET 控件。它们中的大多数使用起来非常简单且直观。但是，它们有许多你可以使用的属性和方法。

