

# 第二部分：使用对象

你现在可以根据需要添加对象或进行操作的对象，切换图层，并且可以按需更改属性。例如，要专注于鹿对象，你可以使用图层管理器快速隐藏其他图层。

## 使用场景资源管理器

场景资源管理器是所有场景对象和显示属性的一站式商店。它以分层列表的形式显示场景中的所有对象以及各种显示属性。它允许你过滤显示内容，以便只看到你想要的内容，并自定义显示内容，使只有你想要看到的属性可见。场景资源管理器还允许你选择、重命名、隐藏、排序、冻结、链接和删除对象，并更改对象颜色。

场景资源管理器对话框，如图 6.19 所示，使用 Tools↔ New Scene Explorer 菜单命令（Alt+Ctrl+O）打开。每个后续的场景资源管理器视图都会编号，但这些单独的视图也可以使用每个场景资源管理器窗口顶部的 View 字段进行命名。每个新视图或命名视图都可以通过 Tools↔ Saved Scene Explorers 菜单调用，并且 Tools↔ Manage Scene Explorers 打开一个简单的对话框，你可以在其中加载、保存、删除和重命名已保存的视图。

### Note

场景资源管理器视图会随 Max 文件自动保存并重新加载。

场景资源管理器中的所有场景对象都按层次顺序列出，子对象在其父对象下方缩进。你可以通过单击父对象左侧的加号 (+) 或减号 (–) 图标来展开或收缩子对象。

## 选择和过滤对象

如果你在场景资源管理器对话框中单击一个对象，该对象行将被高亮显示。按住 Ctrl 键可以单击以选择多个对象，或者你可以使用 Shift 键选择一系列相邻对象。按住 Ctrl 键也可以将所选对象从当前选择中移除。

Select 菜单还包括选择对象的选项。All (Ctrl+A)、None (Ctrl+D) 和 Invert (Ctrl+I) 菜单命令按预期工作，选择所有对象、取消选择所有对象以及选择当前选择的反向选择。你也可以使用对话框底部的按钮访问这些命令。

Select Children (Ctrl+C) 选项会在选择父对象时自动选择所有子对象。Select Influences 选项会选择附加到所选对象的全部影响对象。影响对象是控制或塑造另一个对象的对象。例如，当一个球体被约束为跟随动画路径时，该路径就是球体的一个影响对象。另一个例子是蒙皮网格受双足骨骼驱动。Select Dependencies 选项会选择依赖于所选对象的任何对象，例如实例和引用。

当启用 Select↔ Sync Selection 选项时，在场景资源管理器对话框中选择的任何对象都会自动在视口中被选中。这也可以反向工作，导致在视口中选择的任何对象都会在场景资源管理器对话框中被选中。

场景资源管理器识别任何定义的 Selection Sets，并允许你从界面底部的下拉列表中选择这些集合。

## FIGURE 6.19

场景资源管理器对话框显示所有场景对象及其显示属性。

- Display Bones
- Display Object Refs
- Display Groups
- Display Space Warps
- Display Helpers
- Display Camera
- Display Lights
- Display Shapes
- Display Geometry

![](img/ebbb4844f027f7d1c580e48108d2b6cb_240_0.png)

- Lock Cell Editing
- Configure
  - Advanced Filter
- Enable
  - Advanced Filter
- Invert Display
- Display None
- Display All
- Display Hidden Objects
- Display Frozen Objects
- Display Containers

- Filter Selection Set
- Sync Selection
- Select Invert
- Select None
- Select All

## Part II: Working with Objects

显示工具栏包含几个对象类型图标。黄色图标表示已选中并允许在场景资源管理器中查看。要过滤掉特定对象类型，请禁用其图标，然后该类型的所有对象都将不再在列表中显示。这些相同的命令也在 Display ▸ Object Types 菜单中可用。

Display 菜单还包括显示子对象、影响和依赖项的一些附加命令。你还有一个 Display in Track View 的选项。此选项会打开 Track View，并显示所选对象的轨道。

## Cross-Ref

Track View 界面在第 36 章“在 Track View 中使用函数曲线”中有更详细的介绍。■

## 查找对象

你也可以使用 Find 字段按名称在层次结构中搜索特定对象。所有匹配输入字符的对象都会被选中。如果你启用 Select ▸ Find Case Sensitive 选项，大写字符会与小写字符区分开。

如果选择 Select ▸ Find Using Wildcards 选项，你可以使用通配符来定位对象。可接受的通配符包括用于连续多个字符的星号 (*) 和用于单个字符的问号 (?)。例如，hedra* 的条目会选择所有以“hedra”开头的对象，而不管结尾如何，而 hedra?1 会找到“hedra01”和“hedra11”，但找不到“hedra02”或“hedra0001”。

Select ▸ Find Using Regular Expressions 选项提供了另一种搜索特定对象的方法。正则表达式通常用于各种脚本语言，并且需要特定的语法才能定位对象。表 6.5 列出了一些常见的正则表达式字符。

## TABLE 6.5

### Common Regular Expression Syntax

| Character | Description | Example |
|---|---|---|
| [htk] | Used to define a group of search characters | Matches all objects beginning with the letters h, t, and k |
| Eye\|light\|key | Used to separate words to search for | Matches all objects beginning with eye, light, or key |
| \w | Used to identify any letter or number, just like the ? wildcard | Matches any number or letter |
| \s | Used to identify any white space | Matches any space between words, no matter the length |
| \d | Used to identify any single digit number | Matches any single-digit number, 0 through 9 |
| [^geft] | Used to match all objects except for the ones inside the brackets | Matches all objects except for those that begin with g, e, f, or t |
| t.*1 | Used to match multiple letters in between two specified characters | Matches all objects that begin with the letter t and end with the number 1 |

## Chapter 6: Selecting Objects and Setting Object Properties

如果正则表达式看起来令人困惑，你也可以使用如图 6.20 所示的高级搜索对话框进行搜索。此对话框可通过 Select Search 或单击 Configure Advanced Filter 按钮打开。在 Property 字段中，你可以按 Name、Type、Color、Faces 或其他可用列进行搜索。在 Condition 中，选项包括 Starts With、Does Not Start With、Contains String、Does Not Contain String、Regular Expression Matches 和 Inverse Regular Expression Matches。可以将多个条件添加到搜索列表中。

## FIGURE 6.20

高级搜索对话框允许你使用下拉列表选择搜索条件。

![](img/ebbb4844f027f7d1c580e48108d2b6cb_242_0.png)

## 在场景资源管理器中编辑

场景资源管理器中列出的任何显示属性都可以通过简单地单击复选框来启用该属性。如果在启用或禁用属性时选择了多个对象，则同一属性会同时为所有所选对象启用或禁用。

### Note

如果启用了 Lock Cell Editing 按钮，则无法更改任何属性。

如果你单击列名，可以按降序或升序对所有列出的对象进行排序。单击列名一次即可按升序排序，再次单击即可按降序排序。你也可以右键单击并从弹出菜单中选择排序顺序。例如，如果你单击 Faces 列，所有对象都会被排序，使面数最少的对象列在界面的顶部，面数最多的对象列在底部。

你也可以通过拖放来重新排列列。选择 Customize Configure Columns 菜单会打开如图 6.21 所示的 Configure Columns 对话框。此对话框列出了所有可用的剩余显示属性列。要将其添加到场景资源管理器，只需从 Configure Columns 对话框中选择它并将其拖放到所需位置即可。

Configure Columns 对话框包含大量可作为场景资源管理器列添加的属性，包括 Revit Category、Revit Family、Revit Level、Revit Type 和 Application Origin。

### Tip

每个列的宽度可以通过拖动两侧来更改。要重置所有列宽，请右键单击列名并从弹出菜单中选择 Best Fit (all columns)。

