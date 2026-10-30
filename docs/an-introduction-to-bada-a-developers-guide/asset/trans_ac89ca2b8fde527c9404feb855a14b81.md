

# 提示、陷阱和相关主题

所有容器，包括 Form 容器，都必须在堆内存上创建。但是，一旦 Form 已附加到 Frame，应用程序框架将在应用程序终止时负责其删除。如果开发者删除控件，将会导致问题。

## 食谱 2.2：向 Form 添加软键并获取操作

### 问题描述

你想向 Form 添加软键。

### 食谱

本食谱需要以下配置：

**使用的命名空间：**
`Osp::Ui`、`Osp::Ui::Controls`，如果软键显示图像则 additionally `Osp::Media`、`Osp::Graphics`

**需要 #include 的头文件：**
`FUi.h`、`FUiControls.h`，如果软键显示图像则 additionally `FMedia.h`、`FGraphics.h`

**必需库：**
`FUi`、`FUiControls`，如果软键显示图像则 additionally `FMedia`、`FGraphics`

**必需的权限级别：**
`Normal`

**必需的权限组：**
`IMAGE`

Form 由指示区域、标签和标题区域、客户端区域以及软键区域组成。Form 的样式决定是否显示指示器、标签、标题、选项键或软键。

软键可以显示文本或位图。软键在被按下时会生成操作事件。如果应用程序想要处理软键生成的操作事件，它应该实现一个操作事件监听器并使用 `AddSoftkeyActionListener()` 方法将其注册到软键。

本食谱详细说明了为 Form 创建左右软键的步骤，并描述了 Form 接收和处理软键操作事件所需实现的代码（见图 R2.2）。在本食谱中，左侧软键包含图标，右侧软键包含文本。

![](img/a257d5fd53a79a244a20e587cd2f08f6_279_0.png)

图 R2.2 带软键的 Form。

本食谱假设已按照“向基于 Frame 的 App 添加 Form”食谱中的方法 2 的步骤将 Form 添加到应用程序的 Frame。它还假设已按照“向 Form 添加简单按钮控件”食谱中描述的步骤实现 Osp::Ui::IActionEventListener 接口类。

要显示带有左右软键的软键区域，需要使用 FORM_STYLE_SOFTKEY_0（与左侧软键相关）和 FORM_STYLE_SOFTKEY_1（与右侧软键相关）样式参数调用 Form 构造函数。

以下代码片段是将在 MainForm 的 Initialize() 方法中实现的代码示例：

```
Form::Construct(FORM_STYLE_NORMAL|FORM_STYLE_TITLE|
FORM_STYLE_INDICATOR|FORM_STYLE_SOFTKEY_0|FORM_STYLE_SOFTKEY_1);
```

需要在 MainForm 中为每个软键添加操作 ID，以便在 OnActionPerformed() 事件处理程序中处理事件时可以识别软键操作事件：

```
static const int ID_SOFTKEY_LEFT = 101;
static const int ID_SOFTKEY_RIGHT = 102;
```

在 OnActionPerformed() 事件处理程序中，软键操作事件通过在创建软键时注册的操作 ID 来识别，并可以实现相关的处理。

以下代码片段是 MainForm 的 OnActionPerformed() 方法的示例：

```
void
MainForm::OnActionPerformed(const Osp::Ui::Control& source, int actionId)
{
    switch(actionId)
    {
    case ID_SOFTKEY_LEFT:
    {
        // Add left softkey handling code here
    }
    break;
    case ID_SOFTKEY_RIGHT:
    {
        // Add right softkey handling code here
    }
    break;
    default:
        break;
    }
}
```

软键应在 MainForm 初始化期间创建 - OnInitializing()：

+   1. 创建 Image 对象并初始化。
+   2. 将图像文件解码为解码后的位图容器，传递图像文件的本地文件路径和颜色格式参数。
+   3. 设置左侧软键以显示图标并分配“Normal”和“Pressed”图像。
+   4. 设置右侧软键以显示文本字符串。
+   5. 为两个软键分配唯一的操作 ID。
+   6. 将 MainForm 类实现的 IActionEventListener 注册到软键。

以下代码片段是将在 MainForm 的 OnInitializing() 方法中添加到创建左右软键的代码示例：

```
// Create left softkey (SOFTKEY_0)
// Create a Bitmap and decode image
Bitmap* pBitmap = null;
Image* pImage = new Image();
pImage->Construct();
pBitmap = pImage->DecodeN(L"/Res/bada.png", BITMAP_PIXEL_FORMAT_ARGB8888);

SetSoftkeyIcon(SOFTKEY_0, *pBitmap, pBitmap);

delete pImage;
delete pBitmap;

// Create right softkey (SOFTKEY_1)
SetSoftkeyText(SOFTKEY_1, "Right");

// Assign action IDs for both the softkeys
SetSoftkeyActionId(SOFTKEY_0, ID_SOFTKEY_LEFT);
SetSoftkeyActionId(SOFTKEY_1, ID_SOFTKEY_RIGHT);

// Register event listener
AddSoftkeyActionListener(SOFTKEY_0, *this);
AddSoftkeyActionListener(SOFTKEY_1, *this);
```

## 提示、陷阱和相关主题

如果同时为同一个软键设置图标和文本，则文本优先于图标。软键可以使用 SetSoftkeyEnabled() 方法启用或禁用，将 enable 参数设置为 true 或 false。

## 相关食谱

- Add a Form to a Frame-based App
- Add a Simple Button Control to a Form

## 食谱 2.3：向 Form 添加选项菜单并获取用户选择

### 问题描述

你想向 Form 添加选项菜单并获取用户的选择。

### 食谱

本食谱需要以下配置：

使用的命名空间：
Osp::Ui, Osp::Ui::Controls

需要 #include 的头文件：
FUi.h, FUiControls.h

必需库：
FUi, FUiControls

必需的权限级别：
Normal

必需的权限组：
None

Form 由指示区域、标签和标题区域、客户端区域以及软键区域组成。Form 的样式决定是否显示指示器、标签、标题、选项键或软键。

选项菜单是从显示器命令区域的选项键激活的菜单控件。它可用于向用户呈现多个选项，并显示在表单内容之上。它是一个分层菜单，可以包含最多两级，由主项和子项组成。菜单项只能以文本字符串呈现；位图无法显示。

选项菜单控件不会添加到容器中，因此在不再需要时必须显式删除。应用程序框架在应用程序终止时不会删除选项菜单。

本食谱详细说明了为 Form 创建选项键并添加两级选项菜单的步骤，并描述了 Form 接收和处理选项键和选项菜单操作事件所需实现的代码（见图 R2.3）。

本食谱假设已按照“向基于 Frame 的 App 添加 Form”食谱中方法 2 详细说明的步骤将 Form 添加到应用程序的 Frame。它还假设已按照“向 Form 添加简单按钮控件”食谱中描述的步骤实现 Osp::Ui::IActionEventListener 接口类。

要在显示器的软键区域显示选项键，需要使用 FORM_STYLE_OPTIONKEY 样式参数调用 Form 构造函数。

以下代码片段是将在 MainForm 的 Initialize() 方法中实现的代码示例：

```
Form::Construct(FORM_STYLE_NORMAL|FORM_STYLE_TITLE|
FORM_STYLE_INDICATOR|FORM_STYLE_OPTIONKEY);
```

![](img/a257d5fd53a79a244a20e587cd2f08f6_283_0.png)

![](img/a257d5fd53a79a244a20e587cd2f08f6_283_1.png)

![](img/a257d5fd53a79a244a20e587cd2f08f6_283_2.png)

图 R2.3 具有两级的选项菜单。

## 提示、陷阱和相关主题

本食谱中显示的示例为选项菜单的菜单层次结构具有两级固定结构。也可以在运行时动态添加、更改和删除项目。如果要更改选项菜单的内容，可以使用多种方法来添加、更改和删除主项和子项。这些方法为：`AddItem()`、`AddSubItem()`、`SetItemAt()`、`SetSubItemAt()`、`RemoveItem()` 和 `RemoveSubItem()`。

如果需要确定主项是否有关联的子项以及有多少个，可以使用 `GetSubItemCount()` 方法。

在示例中，菜单中的第一个主项（`ID_OPTION1`）具有关联的子项。在此场景中，无需在 `OnActionPerformed()` 事件处理程序中为此操作 ID 实现代码，因为子项的显示由选项菜单对象自动执行。但是，如果在 `OnActionPerformed()` 事件处理程序中为此操作 ID 有代码，它将在子项显示后执行。

当用户选择子项或没有关联子项的主项时，选项菜单对象将为表单处理生成适当的事件，并且菜单将从显示中移除。

由于选项菜单在没有子项可显示时从显示中移除的方式，不建议在选择该主项时为其动态创建任何子项。

如果项目的文本字符串太长，显示时会截断：

- 主项将在两行文本（英文）处截断，并在字符串末尾添加‘…’。
- 子项将在一行文本（英文）处截断，并在字符串末尾添加‘…’。

## 相关食谱

- Add a Form to a Frame-based App
- Add a Simple Button Control to a Form

## 食谱 2.4：向 Form 添加简单按钮控件

### 问题描述

你想向 Form 添加 Button 控件。

