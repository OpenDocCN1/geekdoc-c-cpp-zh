
- `String getText()`
- `void setText(String text)`  
  获取或设置此文本组件的文本。
- `boolean isEditable()`
- `void setEditable(boolean b)`  
  获取或设置可编辑属性，该属性决定用户是否可以编辑此文本组件的内容。

### 11.3.1 文本字段

向窗口添加文本字段的常见方式是将其添加到面板或其他容器中——就像添加按钮一样：

```
var panel = new JPanel();
var textField = new JTextField("Default input", 20);
panel.add(textField);
```

这段代码添加一个文本字段，并通过在其中放置字符串 "Default input" 来初始化它。此构造方法的第二个参数设置宽度。在此例中，宽度为 20 个“列”。遗憾的是，列是一种相当不精确的度量。一列是文本所用字体中一个字符的预期宽度。其思路是，如果你预计输入不超过 *n* 个字符，就应将 *n* 指定为列宽。在实践中，这种度量效果并不太好，为稳妥起见，你应该在最大输入长度上加 1 或 2。另外，请记住，列数只是给 AWT 的一个提示，用于给出*首选*大小。如果布局管理器需要增大或缩小文本字段，它可以调整其大小。你在 `JTextField` 构造方法中设置的列宽并不是用户可输入字符数的上限。用户仍然可以输入更长的字符串，但当文本超过字段长度时，输入内容会滚动。用户往往觉得滚动的文本字段很烦人，因此你应该把字段设置得足够宽裕。如果需要在运行时重置列数，可以使用 `setColumns` 方法。

![](img/0e7b74ef51a065c077b42cd87b362288_927_0.png)

**提示：**

使用 `setColumns` 方法更改文本框大小后，请调用周围容器的 revalidate 方法。

```
textField.setColumns(10);
panel.revalidate();
```

`revalidate` 方法会重新计算容器中所有组件的大小和布局。使用 `revalidate` 方法后，布局管理器会调整容器大小，文本字段更改后的大小将变得可见。

`revalidate` 方法属于 `JComponent` 类。它不会立即调整组件大小，而只是将其标记为需要调整大小。如果多个组件请求调整大小，这种方法可以避免重复计算。但是，如果要重新计算 `JFrame` 内的所有组件，则必须调用 `validate` 方法——`JFrame` 并不继承 `JComponent`。

一般来说，用户会在文本字段中添加文本（或编辑现有文本）。这些文本字段经常一开始是空白的。要创建空白文本字段，只需省略 `JTextField` 构造方法中的字符串参数：

```
var textField = new JTextField(20);
```

你可以随时使用上一节提到的 `JTextComponent` 父类中的 `setText` 方法来更改文本字段的内容。例如：

```
textField.setText("Hello!");
```

并且，如上一节所述，你可以通过调用 `getText` 方法了解用户输入了什么。此方法返回用户输入的精确文本。要删除文本字段数据中多余的前导和尾随空格，请对 `getText` 的返回值应用 `trim` 方法：

```java
String text = textField.getText().trim();
```

要更改用户文本显示的字体，请使用 `setFont` 方法。

**javax.swing.JTextField 1.2**

- `JTextField(int cols)`  
  构造一个具有指定列数的空 `JTextField`。
- `JTextField(String text, int cols)`  
  构造一个新的 `JTextField`，其中包含初始字符串和指定列数。
- `int getColumns()`
- `void setColumns(int cols)`  
  获取或设置此文本字段应使用的列数。

**javax.swing.JComponent 1.2**

- `void revalidate()`  
  使组件的位置和大小被重新计算。
- `void setFont(Font f)`  
  设置此组件的字体。

**java.awt.Component 1.0**

- `void validate()`  
  重新计算组件的位置和大小。如果该组件是容器，则重新计算其各个组件的位置和大小。
- `Font getFont()`  
  获取此组件的字体。

### 11.3.2 标签和组件标注

标签是包含文本的组件。它们没有装饰（例如，没有边框）。它们也不响应用户输入。你可以使用标签来标识组件。例如，与按钮不同，文本字段没有用于标识它们的标签。要为本身不带标识符的组件添加标签：

- 1. 使用正确的文本构造一个 JLabel 组件。
- 2. 将其放置得离要标识的组件足够近，以便用户能够看出该标签标识的是正确的组件。

JLabel 的构造方法允许你指定初始文本或图标，并且可以选择指定内容的对齐方式。使用 SwingConstants 接口中的常量来指定对齐方式。该接口定义了许多有用的常量，例如 LEFT、RIGHT、CENTER、NORTH、EAST 等。JLabel 类是实现该接口的多个 Swing 类之一。因此，你可以通过以下任一方式指定右对齐标签：

```
var label = new JLabel("User name: ", SwingConstants.RIGHT);
```

或者

```
var label = new JLabel("User name: ", JLabel.RIGHT);
```

setText 和 setIcon 方法让你可以在运行时设置标签的文本和图标。

**提示：**

你可以在按钮、标签和菜单项中同时使用纯文本和 HTML 文本。我不建议在按钮中使用 HTML——它会干扰外观风格。但标签中的 HTML 可能非常有效。只需用 `<html>. . .</html>` 包裹标签字符串，如下所示：

```java
label = new JLabel("<html><b>Required</b> entry:</html>");
```

请注意，第一个带有 HTML 标签的组件可能需要一些时间才能显示，因为必须加载相当复杂的 HTML 渲染代码。

标签可以像任何其他组件一样放置在容器内。这意味着你可以使用之前见过的技术，将标签放置在需要的位置。

**javax.swing.JLabel 1.2**

- `JLabel(String text)`
- `JLabel(Icon icon)`
- `JLabel(String text, int align)`
- `JLabel(String text, Icon icon, int align)`  
  构造一个标签。align 参数是 `SwingConstants` 常量 `LEFT`（默认）、`CENTER` 或 `RIGHT` 之一。
- `String getText()`
- `void setText(String text)`  
  获取或设置此标签的文本。
- `Icon getIcon()`
- `void setIcon(Icon icon)`  
  获取或设置此标签的图标。

### 11.3.3 密码字段

密码字段是一种特殊的文本字段。为了防止爱窥探的旁观者看到你的密码，用户输入的字符实际上不会显示出来。相反，每个输入的字符都由一个*回显字符*表示，例如圆点（•）。Swing 提供了一个 `JPasswordField` 类来实现这种文本字段。

密码字段是模型-视图-控制器架构模式强大能力的另一个示例。密码字段使用与常规文本字段相同的模型来存储数据，但其视图已改为将所有字符显示为回显字符。

**`javax.swing.JPasswordField`** 1.2

---

- `JPasswordField(String text, int columns)`  
  构造一个新的密码字段。
- `void setEchoChar(char echo)`  
  设置此密码字段的回显字符。这只是建议性的；特定的外观风格可能会坚持自己选择的回显字符。值为 0 会将回显字符重置为默认值。
- `char[] getPassword()`  
  返回此密码字段中包含的文本。为了更强的安全性，使用后应覆盖返回数组的内容。（密码不会以 `String` 形式返回，因为字符串会一直留在虚拟机中，直到被垃圾回收。）

### 11.3.4 文本区域

