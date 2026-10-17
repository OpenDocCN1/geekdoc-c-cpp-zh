
| `ErrorStyle` | Retrieves the style attributes of an EditorZone control for displaying an error message if the control is not loaded or created |

| `ErrorText` | Retrieves or sets the text to display an error message in the editing UI |

| `FooterStyle` | Retrieves the style attributes for the footer area of a zone |

| `HeaderCloseVerb` | Retrieves a reference to a `WebPartVerb` object in the header of a `ToolZone` control to close the control |

| `HeaderStyle` | Retrieves the style attributes for the header area of a zone |

| `HeaderText` | Retrieves or sets the text for the header area of a zone |

| `HeaderVerbStyle` | Retrieves the style attributes of all the header verbs displayed in a `ToolZone` control |

| `InstructionText` | Retrieves or sets the text to instruct users how to use a `ToolZone` control |

| `InstructionTextStyle` | Retrieves the attributes for the text displayed at the top of a `ToolZone` control |

| `LabelStyle` | Retrieves the style attributes for the labels that appear in the editing controls of a `ToolZone` control |

| `OKVerb` | Retrieves a reference to a `WebPartVerb` object to apply editing changes to a control and hide the editing UI |

| `Padding` | Retrieves or sets the attributes related to cell padding in a table containing Web Parts controls |

| `PartChromeStyle` | Retrieves the style attributes for the borders of Web Parts controls contained in a zone |

| `PartChromeType` | Retrieves or sets the border type of Web Parts controls |

| `PartStyle` | Retrieves the style attributes for the border and content of Web Parts controls |

| `PartTitleStyle` | Retrieves the style attributes for the title bar of Web Parts controls |

| `VerbButtonType` | Retrieves or sets the button to represent the verbs in a zone |

| `VerbStyle` | Retrieves style characteristics for the UI of verbs of Web Parts controls |

| `ZoneTemplate` | Provides a template to add child controls to an `EditorZone` control |

# The LayoutEditorPart Control

你可以使用 `LayoutEditorPart` 控件为 Web Parts 控件创建一个功能完善的布局编辑器，这些控件可以与其各自的 `LayoutEditorPart` 控件关联。要更改 Web Parts 控件的布局，只需在与该 Web Parts 控件关联的 `LayoutEditorPart` 控件中进行必要的更改即可。

`LayoutEditorPart` 控件仅在 Web 页面处于编辑模式时可见。在此模式下，你可以选择并更改 Web Part 控件的属性。`LayoutEditorPart` 控件提供以下三个选项来修改 Web Parts 控件：

- `ChromeState` – 获取或设置 Web Parts 控件的当前状态，该状态可以是正常或最小化。
- `Zone` – 设置 `WebPartZoneBase` 区域，该区域由你想要修改的 Web Parts 控件组成。
- `ZoneIndex` – 设置驻留在 `WebPartZone` 控件中的 Web Parts 控件的索引位置。此选项允许你确定 Web Parts 控件在 `WebPartZone` 控件内的特定位置。

你必须以页面持久性格式使用 `LayoutEditorPart` 控件。此格式使 `LayoutEditorPart` 控件能够在浏览器会话之间保留其属性值。为此，你需要在 `<ZoneTemplate>` 元素内声明 `<asp:LayoutEditorPart>` 元素。

要将 `LayoutEditorPart` 控件添加到 Web 页面，请从工具箱拖放 `LayoutEditorPart` 控件到 `Default.aspx` 页面的设计视图中。图 16.17 显示了设计视图中 `EditorZone` 控件内的 `LayoutEditorPart` 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_823_0.png)

你也可以通过在 `Default.aspx` 页面的 `<form>` 元素中使用以下代码来添加 `LayoutEditorPart` 控件：

```
<asp:EditorZone ID="EditorZone1" runat="server">
<ZoneTemplate>
<asp:LayoutEditorPart ID="LayoutEditorPart1" runat="server" />
</ZoneTemplate>
</asp:EditorZone>
```

`LayoutEditorPart` 控件是 `LayoutEditorPart` 类的对象。

> NOTE
>
> 如果你将 `LayoutEditorPart` 控件放置在 `EditorZone` 控件以外的任何区域，设计器将生成错误。

`LayoutEditorPart` 控件是使用 .NET Framework 类库的 `LayoutEditorPart` 类创建的。`LayoutEditorPart` 类允许你修改关联的 Web Parts 控件的布局。此类可在 `System.Web.UI.WebControls.WebParts` 命名空间中使用。`LayoutEditorPart` 类的继承层次结构如下所示：

```
System.Object
    System.Web.UI.Control
        System.Web.UI.WebControls.WebControl
            System.Web.UI.WebControls.Panel
                System.Web.UI.WebControls.WebParts.Part
                    System.Web.UI.WebControls.WebParts.EditorPart
                        System.Web.UI.WebControls.WebParts.LayoutEditorPart
```

`LayoutEditorPart` 控件与 `LayoutEditorPart` 类关联。此类采用各种方法来执行任务，例如将更改和样式属性应用于 Web Parts 控件并确定两个对象实例是否相等。`LayoutEditorPart` 类的注目方法列于表 16.31：

| Table 16.31: Noteworthy Methods of the LayoutEditorPart Class |

| Method | Description |

| ApplyChanges | 使用在 `LayoutEditorPart` 控件中进行的更改更新关联的 `WebPart` 控件属性 |

| SyncChanges | 从 `WebPart` 控件获取属性值，然后将其分配给关联的 `LayoutEditorPart` 控件 |

现在，让我们来看看 `LayoutEditorPart` 类的属性，该类继承自 `EditorPart` 类。此类充当基类，为 `LayoutEditorPart` 类提供一组属性和方法，该类还从其他类（如 `Control`、`Part` 和 `WebControl`）继承了一些属性。`LayoutEditorPart` 类继承的各种属性为 `Font`、`Enabled`、`Page` 和 `Style`。`LayoutEditorPart` 类的注目属性列于表 16.32：

| Table 16.32: Noteworthy Properties of the LayoutEditorPart Class |

| Property | Description |

| DefaultButton | 检索或指定包含在 `Panel` 控件中的默认按钮的 ID |

| Display | 检索一个值，该值指定当与其关联的 Web Parts 控件处于编辑模式时是否应显示 `LayoutEditorPart` 控件 |

| Title | 检索或指定用作 `LayoutEditorPart` 控件标题的字符串 |

## The AppearanceEditorPart Control

`AppearanceEditorPart` 控件允许用户编辑与 Web 页面上 Web Parts 控件的外观相关联的属性。此控件驻留在 `EditorZone` 区域中，仅在选择 Web Parts 控件进行编辑时可见。`AppearanceEditorPart` 控件上显示以下选项：

- `Title` — 指定一个字符串值，该值作为 `AppearanceEditorPart` 控件的标题出现
- `Height` — 指定 `AppearanceEditorPart` 控件的高度
- `Width` — 指定 `AppearanceEditorPart` 控件的宽度
- `ChromeType` — 使用 `DropDownList` 控件选择 `AppearanceEditorPart` 控件的标题和边框类型（点线、单线或双线）
- `Direction` — 使用 `DropDownList` 控件选择 `AppearanceEditorPart` 控件内内容流的方向（水平或垂直）
- `Hidden` — 使用 `CheckBox` 控件隐藏或显示 `AppearanceEditorPart` 控件

要将 `AppearanceEditorPart` 控件添加到 `EditorZone` 控件，请从工具箱拖放该控件到 `Default.aspx` 页面的设计视图中的 `EditorZone` 控件。图 16.18 显示了设计视图中 `EditorZone` 控件内的 `AppearanceEditorPart` 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_825_0.png)

你也可以通过在 `Default.aspx` 页面的 `<form>` 元素中使用以下代码来添加 `AppearanceEditorPart` 控件：

```
```aspx

<asp:EditorZone ID="EditorZone1" runat="server">

    <ZoneTemplate>

        <asp:AppearanceEditorPart

            ID="AppearanceEditorPart1"

            runat="server" />

    </ZoneTemplate>

</asp:EditorZone>

```
```

`AppearanceEditorPart` 控件是使用 .NET Framework 类库的 `AppearanceEditorPart` 类创建的。`AppearanceEditorPart` 类提供了一个编辑器，用于修改关联的 Web Parts 控件的 UI 属性。此类可在 `System.Web.UI.WebControls.WebParts` 命名空间中使用。`AppearanceEditorPart` 类的继承层次结构如下所示：

```
```text

System.Object

    System.Web.UI.Control

        System.Web.UI.WebControls.WebControl

            System.Web.UI.WebControls.Panel

                System.Web.UI.WebControls.WebParts.Part

                    System.Web.UI.WebControls.WebParts.EditorPart

                        System.Web.UI.WebControls.WebParts.AppearanceEditorPart

```
```

`AppearanceEditorPart` 类包含在运行时用于处理 `AppearanceEditorPart` 控件的方法和属性。`AppearanceEditorPart` 类的注目方法列于表 16.33：

**Table 16.33: Noteworthy Methods of the AppearanceEditorPart Class**

| Method | Description |

|---|---|

| ApplyChanges | 使用在 `AppearanceEditorPart` 控件中进行的更改更新关联的 `WebPart` 控件属性 |

| SyncChanges | 从 `WebPart` 控件获取属性值，然后将其分配给关联的 `AppearanceEditorPart` 控件 |

`AppearanceEditorPart` 类的注目属性列于表 16.34：

| Table 16.34: Noteworthy Properties of the AppearanceEditorPart Class |

| Property | Description |

| DefaultButton | 检索或指定包含在 `Panel` 控件中的默认按钮的 ID |

| Title | 检索或指定用作 `AppearanceEditorPart` 控件标题的字符串 |

## The PropertyGridEditorPart Control

`PropertyGridEditorPart` 控件提供了一个 UI，允许用户在 Web 页面上编辑 Web Parts 控件的自定义属性。此控件驻留在 Web 页面的 `EditorZone` 控件中。`PropertyGridEditorPart` 控件仅在 Web 页面处于编辑模式时或用户选择 Web Parts 控件进行编辑时可见。

`PropertyGridEditorPart` 控件使用户能够编辑在源代码中标记有 `WebBrowsableAttribute` 属性的属性。此属性指定属性是否应在 `PropertyGridEditorPart` 控件中显示。在指定可编辑属性后，`PropertyGridEditorPart` 控件会根据要编辑的属性类型创建可编辑的 UI。

要将 `PropertyGridEditorPart` 控件添加到 Web 页面，首先从工具箱拖放 `EditorZone` 控件到 `Default.aspx` 页面的设计视图中，然后从工具箱拖放 `PropertyGridEditorPart` 控件到设计视图中的 `EditorZone` 控件。图 16.19 显示了设计视图中 `EditorZone` 控件内的 `PropertyGridEditorPart` 控件：

![](img/e073a4882197be4ab61103cbe0bcb394_826_0.png)

Figure 16.19: Displaying the PropertyGridEditorPart Control

你也可以通过在 `<form>` 元素中使用以下代码在 `Default.aspx` 页面中添加 `PropertyGridEditorPart` 控件：

```
<asp:EditorZone ID="EditorZone1" runat="server">
<ZoneTemplate>
<asp:PropertyGridEditorPart ID="PropertyGridEditorPart1" runat="server" />
</ZoneTemplate>
</asp:EditorZone>
```

`PropertyGridEditorPart` 控件是 `PropertyGridEditorPart` 类的对象。此控件是使用 .NET Framework 类库的 `PropertyGridEditorPart` 类创建的。`PropertyGridEditorPart` 类使用户能够修改关联的 Web Parts 或服务器控件的自定义属性。此类可在 `System.Web.UI.WebControls.WebParts` 命名空间中使用。`PropertyGridEditorPart` 类的继承层次结构如下所示：

System.Object

    System.Web.UI.Control

        System.Web.UI.WebControls.WebControl
