
```java
families.setValue("System");

EventHandler<ActionEvent> listener = event ->
{
    int size = (int) group.getSelectedToggle().getUserData();
    Font font = Font.font(
        families.getValue(),
        bold.isSelected() ? FontWeight.BOLD : FontWeight.NORMAL,
        italic.isSelected() ? FontPosture.ITALIC : FontPosture.REGULAR,
        size);
    sampleText.setFont(font);
};
small.setOnAction(listener);
medium.setOnAction(listener);
large.setOnAction(listener);
extraLarge.setOnAction(listener);
bold.setOnAction(listener);
italic.setOnAction(listener);
families.setOnAction(listener);

VBox root = new VBox(0.8 * rem,
    hbox(sampleText),
    hbox(bold, italic),
    hbox(small, medium, large, extraLarge),
    hbox(families));

stage.setScene(new Scene(root));
stage.setTitle("ChoiceTest");
stage.show();

}
```

| javafx.scene.control.CheckBox |
|---|
| • `CheckBox(String text)`<br>用给定文本构造一个复选框。<br>• `boolean isSelected()`<br>• `void setSelected(boolean value)`<br>获取或设置此复选框的选中状态。 |

| javafx.scene.control.RadioButton |
|---|
| • `RadioButton(String text)`<br>用给定文本构造一个单选按钮。 |

| `javafx.scene.control.ToggleButton` |
|---|
| • `void setToggleGroup(ToggleGroup value)`<br>设置此按钮的切换组。<br>• `boolean isSelected()`<br>• `void setSelected(boolean value)`<br>获取或设置此按钮的选中状态。 |

| `javafx.scene.control.ToggleGroup` |
|---|
| • `ToggleGroup()`<br>构造一个空的切换组。<br>• `Toggle getSelectedToggle()`<br>获取此切换组中选中的项。 |

| `javafx.scene.control.Toggle` |
|---|
| • `void setUserData(Object value)`<br>• `Object getUserData()`<br>设置和获取与此切换控件关联的数据项。 |

| `javafx.scene.control.ComboBox<T>` |
|---|
| • `ComboBox()`<br>构造一个没有项的组合框。<br>• `ObservableList<T> getItems()`<br>返回此组合框中项的可变列表。 |

| `javafx.scene.control.ComboBoxBase<T>` |
|---|
| • `void setValue(T)`<br>• `T getValue()`<br>设置或获取当前选中的值。<br>• `void setOnAction(EventHandler<ActionEvent>)`<br>设置此控件的动作事件监听器。 |

### 13.5.3 菜单

我们首先介绍了你可能想要放入窗口的最常见控件，例如各种按钮、文本字段和组合框。JavaFX 还支持另一种用户界面元素——GUI 应用程序中常见的下拉菜单。

*窗口顶部的菜单栏包含下拉菜单的名称。单击某个名称会打开包含菜单项和子菜单的菜单。当用户单击菜单项时，会触发一个动作事件。图 13.19 显示了一个带有子菜单的典型菜单。*

![](img/127bccebb2cfadea3f02579edaad63c3_979_0.png)

**图 13.19** 带有子菜单的菜单

你可以通过提供菜单文本以及可选的图形装饰来构造菜单项。装饰可以是任何 Node，但最常见的是提供图像。

```java
MenuItem newItem = new MenuItem("New");
MenuItem cutItem = new MenuItem("Cut", new ImageView("menu/cut.gif"));
```

你可以用同样的方式构造 Menu 对象。

```java
Menu editMenu = new Menu("Edit");
```

通过将菜单项、分隔符和子菜单添加到菜单对象的项列表中，可以把它们加入菜单对象：

```java
editMenu.getItems().addAll(cutItem, copyItem, pasteItem);
```

或者，你可以在构造菜单时提供子节点：

```java
Menu optionsMenu = new Menu("Options", new ImageView("menu/options.gif"),
    readOnlyItem, insertItem, overwriteItem);
```

如果你不想要装饰，请将 null 作为第二个参数传入。

将顶层菜单添加到 MenuBar，再将菜单栏添加到根面板：

```java
MenuBar bar = new MenuBar(fileMenu, editMenu, helpMenu);
VBox root = new VBox(bar, ...);
```

当用户选择菜单时，会触发一个动作事件。你需要为每个菜单项安装事件处理器：

```java
exitItem.setOnAction(event -> Platform.exit());
```

CheckMenuItem 和 RadioMenuItem 控件会在项旁边显示一个勾选标记。它们的工作方式与复选框和单选按钮完全相同。你必须将单选按钮添加到切换组。当组中的某一项被选中时，所有其他项都会自动取消选择。

```java
CheckMenuItem readOnlyItem = new CheckMenuItem("Read-only");

ToggleGroup group = new ToggleGroup();
RadioMenuItem insertItem = new RadioMenuItem("Insert");
insertItem.setToggleGroup(group);
insertItem.setSelected(true);
RadioMenuItem overtypeItem = new RadioMenuItem("Overtype");
overtypeItem.setToggleGroup(group);
```

在我们的示例应用程序中，选中“只读”项会停用“保存”和“另存为”菜单项。你可以通过安装事件监听器来实现这一点：

```java
readOnlyItem.setOnAction(event ->
{
    saveItem.setDisable(readOnlyItem.isSelected());
    saveAsItem.setDisable(readOnlyItem.isSelected());
});
```

或者，正如你将在第 84 页的第 13.6.2 节“绑定”中看到的，你可以使用更优雅的方法并绑定属性：

```java
saveItem.disableProperty().bind(readOnlyItem.selectedProperty());
saveAsItem.disableProperty().bind(readOnlyItem.selectedProperty());
```

禁用的菜单项会变灰——见图 13.20。

*加速键*是键盘快捷键，让你无需打开菜单即可选择菜单项。例如，许多程序将加速键 Control+O 和 Control+S（在 Mac 上为 Command+O 和 Command+S）附加到文件菜单中的打开和保存项。使用 setAccelerator 方法可将加速键附加到菜单项。

```java
openItem.setAccelerator(KeyCombination.keyCombination("Shortcut+O"));
```

![](img/127bccebb2cfadea3f02579edaad63c3_981_0.png)

**图 13.20** 禁用的菜单项

“Shortcut”修饰键在 Windows/Linux 上表示 Control 键，在 Mac 上表示 Command 键。加速键会显示在菜单项旁边——见图 13.21。

键入加速键组合会自动选择该菜单选项并触发一个动作事件，就像用户手动选择了该菜单选项一样。你只能将加速键附加到菜单项，而不能附加到菜单。

![](img/127bccebb2cfadea3f02579edaad63c3_981_1.png)

**图 13.21** 加速键

即使添加修饰键，可用的加速键数量也有限。此外，很少有用户有足够的脑力记住像 Control+Shift+F11 这样的快捷键。在 Linux 和 Windows 上，*键盘助记符*允许用户通过按 Alt 键并键入带下划线的字母来用键盘导航菜单。例如，在图 13.22 所示的菜单中，依次按下 Alt+H C 会选择帮助菜单，然后选择“关于 Core Java”项。与键盘快捷键不同，助记符让你用相当容易记住的键组合访问所有菜单项。

![](img/127bccebb2cfadea3f02579edaad63c3_982_0.png)

**图 13.22** 键盘助记符

你可以通过在菜单项构造函数中在助记符字母前添加下划线，为菜单或菜单项创建键盘助记符：

```java
MenuItem aboutProgramItem = new MenuItem("_About this program");
MenuItem aboutCoreJavaItem = new MenuItem("About _Core Java");
Menu helpMenu = new Menu("_Help", null, aboutProgramItem, aboutCoreJavaItem);
```

> **注意：** 为了减少“视觉噪声”（这种做法并不妥当），大多数用户界面环境（包括 JavaFX）都会隐藏助记符，直到你按下 Alt 键。macOS 根本不支持助记符。

*上下文菜单*是不附加到菜单栏而是浮动在某处的菜单（见图 13.23）。创建上下文菜单的方式与创建常规菜单相同，只是上下文菜单没有标题。然后，将上下文菜单附加到控件。右键单击控件时，上下文菜单会弹出。（在 Mac 上，按住 Control 键并单击。）

```java
ContextMenu contextMenu = new ContextMenu(cutItem, copyItem, pasteItem);
textArea.setContextMenu(contextMenu);
```

![](img/127bccebb2cfadea3f02579edaad63c3_982_1.png)

**图 13.23** 上下文菜单
