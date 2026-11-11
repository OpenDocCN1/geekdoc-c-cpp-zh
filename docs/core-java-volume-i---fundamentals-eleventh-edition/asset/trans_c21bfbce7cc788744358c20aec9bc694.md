
此对话框还显示一个*可展开内容*节点，单击“显示详细信息”即可显示——在我们的示例中，是一个包含异常堆栈跟踪的文本区域。下面说明如何设置这样的节点：

```java
TextArea stackTrace = new TextArea();
alert.getDialogPane().setExpandableContent(stackTrace);
```

如果希望接受用户的文本输入，请使用 `TextInputDialog`，如图 13.27 所示。

![](img/127bccebb2cfadea3f02579edaad63c3_990_0.png)

**图 13.27** 文本输入对话框

`showAndWait` 方法返回一个 `Optional<String>`；如果用户单击了取消按钮或关闭了对话框，则该值为空。下面是一种处理方式：

```java
TextInputDialog dialog = new TextInputDialog();
dialog.setHeaderText("What is your name?");
dialog.showAndWait().ifPresentOrElse(
    result -> { do something with result },
    () -> { deal with cancellation }
);
```

`ChoiceDialog` 类类似。你提供默认选项以及选项数组或列表。如果默认值不为 null，则在显示对话框时选中它（见图 13.28）。`showAndWait` 方法返回一个 `Optional`，其中包含选中项；如果对话框被取消，则为空。

```java
ChoiceDialog<String> dialog = new ChoiceDialog<>("System", Font.getFamilies());
dialog.setHeaderText("Pick a font:");
Optional<String> choice = dialog.showAndWait();
```

泛型 `ChoiceDialog<T>` 类的类型参数是选项的类型。你可以提供任意类型的选项，前提是其 `toString` 方法为组合框生成有意义的字符串。

![](img/127bccebb2cfadea3f02579edaad63c3_991_0.png)

**图 13.28** 选择对话框

> **注意：** 与 `ComboBox<T>` 控件不同，`ChoiceDialog<T>` 控件不允许你设置字符串转换器。

最后，还有一个 `FileChooser`，允许用户选择一个或多个文件。该对话框是系统原生对话框，外观与其他 JavaFX 对话框不同。你可以指定默认目录以及文件扩展名过滤器。

```java
FileChooser dialog = new FileChooser();
dialog.setInitialDirectory(new File("images"));
dialog.getExtensionFilters().addAll(
    new FileChooser.ExtensionFilter("GIF images", "*.gif"),
    new FileChooser.ExtensionFilter("JPEG images", "*.jpg"));
File result = dialog.showSaveDialog(stage);
```

显示对话框时，请提供 `Stage` 对象，如下所示。如果传入 null，则不会阻止向该 `Stage` 输入。

`showSaveDialog` 方法生成一个对话框，让你选择现有文件或输入新名称。`showOpenDialog` 方法只允许选择现有文件。还有一个 `showOpenMultipleDialog` 方法，返回所有已选文件的 `List`。如果对话框被取消，这三个方法都返回 null。

要选择目录，请改用 `DirectoryChooser`：

```java
DirectoryChooser dialog = new DirectoryChooser();
File result = dialog.showDialog(stage);
```

## 文档标题示例

这是一个示例段落，用于演示图像中文档结构的提取结果。段落中可能包含一些说明文字。

- 项目一
- 项目二
- 项目三

| 列1 | 列2 |
| --- | --- |
| A | B |
| C | D |

![](img/127bccebb2cfadea3f02579edaad63c3_993_0.png)

> 这是一个引用示例。

```java
136    VBox buttons = new VBox(8 * rem,
137        information, warning, error, confirmation,
138        multipleButtons, expandableContent, textInput, choiceDialog,
139        fileChooser, directoryChooser);
140    buttons.setPadding(new Insets(8 * rem));
141
142    HBox root = new HBox(textArea, buttons);
143
144    stage.setScene(new Scene(root));
145    stage.setTitle("DialogDemo");
146    stage.show();
147 }
148 }
```

### `javafx.scene.control.Alert`

- `Alert(Alert.AlertType alertType)`  
  构造给定类型的警报对话框。`Alert.AlertType` 枚举的值为 `INFORMATION`、`WARNING`、`ERROR`、`CONFIRMATION` 和 `NONE`。
- `Alert(Alert.AlertType alertType, String contentText, ButtonType... buttons)`  
  构造具有给定消息和按钮的给定类型警报对话框。`ButtonType` 枚举的值为 `OK`、`CANCEL`、`YES`、`NO`、`NEXT`、`PREVIOUS`、`FINISH`、`APPLY` 和 `CLOSE`。`CANCEL` 和 `CLOSE` 都会取消对话框。

### `javafx.scene.control.Dialog<T>`

- `Optional<T> showAndWait()`  
  显示对话框并等待用户输入。返回一个表示用户输入的 `T` 类型对象，该对象包装在 `Optional` 中；如果对话框被关闭，则返回空 `Optional`。
- `void setHeaderText(String value)`  
  设置在此对话框标题栏中显示的文本。
- `void setGraphic(Node value)`  
  设置在此对话框中显示的图形。
- `DialogPane getDialogPane()`  
  获取包含此对话框所有控件的窗格。

### `javafx.scene.control.DialogPane`

- `void setExpandableContent(Node content)`  
  设置一个可展开和隐藏的节点。

| 类 | 成员 |
| --- | --- |
| `javafx.scene.control.TextInputDialog` | • `TextInputDialog()`<br>构造用于输入字符串的对话框。 |
| `javafx.scene.control.ChoiceDialog` | • `ChoiceDialog(T defaultChoice, T... choices)`<br>• `ChoiceDialog(T defaultChoice, Collection<T> choices)`<br><br>构造用于选择 T 类型项的对话框。如果 defaultChoice 不为 null，则将其选中。 |
| `javafx.stage.FileChooser` | • `FileChooser()`<br>构造文件选择器。<br><br>• `File showOpenDialog(Window ownerWindow)`<br>• `List<File> showOpenMultipleDialog(Window ownerWindow)`<br>返回所选文件；如果对话框被关闭，则返回 null。显示对话框时，ownerWindow 会被阻止接收输入。<br><br>• `File showSaveDialog(Window ownerWindow)`<br>显示一个用于选择现有文件或输入新文件的对话框，并返回所选文件；如果对话框被关闭，则返回 null。显示对话框时，ownerWindow 会被阻止接收输入。<br><br>• `void setInitialDirectory(File value)`<br>设置此文件选择器的初始目录。 |
| `FileChooser.ExtensionFilter` | • `ExtensionFilter(String description, String... extensions)`<br>• `ExtensionFilter(String description, List<String> extensions)`<br>构造一个扩展名过滤器，接受具有任意给定扩展名的文件。扩展名字符串的格式为 `*.extension`。 |

### `javafx.stage.DirectoryChooser`

- `DirectoryChooser()`  
  构造目录选择器。
- `File showDialog(Window ownerWindow)`  
  显示一个用于选择现有目录或创建新目录的对话框，并返回所选目录；如果对话框被关闭，则返回 null。显示对话框时，ownerWindow 会被阻止接收输入。
- `void setInitialDirectory(File value)`  
  设置此目录选择器的初始目录。

## 13.5.5 高级控件

当然，JavaFX 和 Swing 一样有选项卡窗格、树和表格，还有一些 Swing 从未拥有的用户界面控件，例如日期选择器和手风琴控件。在本节中，我想通过向你展示三个远超 Swing 所能提供的功能的高级控件，来消除任何残留的 Swing 怀旧情绪。

图 13.29 展示了你可以使用 JavaFX 开箱即用地制作的众多图表之一，无需安装任何第三方库。

![](img/127bccebb2cfadea3f02579edaad63c3_997_0.png)

**图 13.29** 一个 JavaFX 饼图

### 而且易如反掌：

```java
PieChart chart = new PieChart();
chart.getData().addAll(
    new PieChart.Data("Asia", 4298723000.0),
    new PieChart.Data("North America", 355361000.0),
    new PieChart.Data("South America", 616644000.0),
    new PieChart.Data("Europe", 742452000.0),
    new PieChart.Data("Africa", 1110635000.0),
    new PieChart.Data("Oceania", 38304000.0));
chart.setTitle("Population of the Continents");
```

总共有六种图表类型可供使用和自定义。有关更多信息，请参见 https://docs.oracle.com/javase/8/javafx/user-interface-tutorial/charts.htm。

在 Swing 中，你可以在 `JEditorPane` 中显示 HTML，但对于大多数实际 HTML，渲染效果很差。这是可以理解的——实现浏览器是艰难的工作。事实上，它如此困难，以至于大多数浏览器都构建在开源 WebKit 引擎之上。JavaFX 也是如此。`WebView` 显示一个嵌入式原生 WebKit 窗口（见图 13.30）。

![](img/127bccebb2cfadea3f02579edaad63c3_998_0.png)

**图 13.30** 浏览网页（图片来源：Cay Horstmann）

