
```java
DocumentListener listener = new DocumentListener()
{
   public void insertUpdate(DocumentEvent event) { setColor(); }
   public void removeUpdate(DocumentEvent event) { setColor(); }
   public void changedUpdate(DocumentEvent event) { }
};
```

`setColor` 方法使用 `getText` 方法从文本字段获取当前用户输入的字符串，并设置颜色。

我们的程序有一个限制。用户可以在文本字段中输入格式错误的输入，例如“twenty”，或者将字段留空。目前，我们捕获 `parseInt` 方法抛出的 `NumberFormatException`，并且当文本字段中的条目不是数字时，我们只是不更新颜色。在下一节中，你将看到如何从一开始就防止用户输入无效输入。

> **注意：** 除了监听文档事件之外，你还可以向文本字段添加动作事件监听器。每当用户按下 Enter 键时，动作监听器都会收到通知。我们不推荐这种方法，因为用户并不总是记得在完成数据输入后按下 Enter 键。如果你使用动作监听器，还应安装焦点监听器，以便跟踪用户何时离开文本字段。

### 清单 10.19 textChange/ColorFrame.java

```java
package textChange;

import java.awt.*;
import javax.swing.*;
import javax.swing.event.*;

/**
 * A frame with three text fields to set the background color.
 */
public class ColorFrame extends JFrame
{
   private JPanel panel;
   private JTextField redField;
   private JTextField greenField;
   private JTextField blueField;

   public ColorFrame()
   {
      DocumentListener listener = new DocumentListener()
      {
         public void insertUpdate(DocumentEvent event) { setColor(); }
         public void removeUpdate(DocumentEvent event) { setColor(); }
         public void changedUpdate(DocumentEvent event) {}
      };

      panel = new JPanel();

      panel.add(new JLabel("Red:"));
      redField = new JTextField("255", 3);
      panel.add(redField);
      redField.getDocument().addDocumentListener(listener);

      panel.add(new JLabel("Green:"));
      greenField = new JTextField("255", 3);
      panel.add(greenField);
      greenField.getDocument().addDocumentListener(listener);

      panel.add(new JLabel("Blue:"));
      blueField = new JTextField("255", 3);
      panel.add(blueField);
      blueField.getDocument().addDocumentListener(listener);

      add(panel);
      pack();
   }

   /**
    * Set the background color to the values stored in the text fields.
    */
   public void setColor()
   {
      try
      {
         int red = Integer.parseInt(redField.getText().trim());
         int green = Integer.parseInt(greenField.getText().trim());
         int blue = Integer.parseInt(blueField.getText().trim());
         panel.setBackground(new Color(red, green, blue));
      }
      catch (NumberFormatException e)
      {
         // don't set the color if the input can't be parsed
      }
   }
}
```

**javax.swing.JComponent 1.2**

- `Dimension getPreferredSize()`
- `void setPreferredSize(Dimension d)`

  获取或设置此组件的首选大小。

**javax.swing.text.Document 1.2**

- `int getLength()`

  返回文档中当前字符数。

- `String getText(int offset, int length)`

  返回文档指定部分中包含的文本。

  **参数：**

  - `offset` — 文本的起始位置
  - `length` — 所需字符串的长度

- `void addDocumentListener(DocumentListener listener)`

  注册监听器，以便在文档更改时收到通知。

**javax.swing.event.DocumentEvent 1.2**

- `Document getDocument()`

  获取作为事件源的文档。

**javax.swing.event.DocumentListener 1.2**

- `void changedUpdate(DocumentEvent event)`

  每当一个属性或一组属性发生变化时调用。

- `void insertUpdate(DocumentEvent event)`

  每当文档中发生插入操作时调用。

- `void removeUpdate(DocumentEvent event)`

  每当文档的一部分被移除时调用。

## 10.4.2 格式化输入字段

在前面的示例程序中，我们希望程序用户输入数字，而不是任意字符串。也就是说，只允许用户输入数字 0 到 9 和连字符（-）。如果连字符出现，它必须是输入字符串的*第一个*符号。

从表面上看，这个输入验证任务听起来很简单。我们可以向文本字段安装键监听器，并消费所有不是数字或连字符的键事件。不幸的是，这种简单的方法虽然通常被推荐用于输入验证，但在实践中效果并不好。首先，并非所有有效输入字符的组合都是有效数字。例如，-3 和 3-3 不是有效数字，即使它们由有效输入字符组成。但更重要的是，还有其他更改文本的方式，不涉及键入字符键。取决于外观风格，某些键组合可用于剪切、复制和粘贴文本。例如，在 Metal 外观风格中，Ctrl+V 键组合会将粘贴缓冲区的内容粘贴到文本字段中。也就是说，我们还需要监控用户不会粘贴无效字符。通过过滤击键来防止无效内容开始显得像一项真正的苦差事。这当然不是应用程序程序员应该担心的事情。

也许令人惊讶的是，在 Java SE 1.4 之前，没有用于输入数值的组件。从《Core Java》第一版开始，我们提供了一个 `IntTextField` 的实现——一个用于输入格式正确的整数的文本字段。在后来的版本中，我们更改了实现，以从 Java 每个版本中添加的各种不成熟的验证方案中提取尽可能有限的优势。最后，在 Java SE 1.4 中，Swing 设计者直面这个问题，并提供了一个通用的 `JFormattedTextField` 类，它不仅可以用于数字输入，还可以用于日期，甚至更特殊的格式化值，例如 IP 地址。

### 10.4.2.1 整数输入

让我们从一个简单的案例开始：用于整数输入的文本字段。

```java
JFormattedTextField intField = new JFormattedTextField(NumberFormat.getIntegerInstance());
```

`NumberFormat.getIntegerInstance` 返回一个格式化器对象，它使用当前区域设置格式化整数。在美国区域设置中，逗号用作数字分隔符，允许用户输入诸如 1,729 的值。第 7 章详细说明如何选择其他区域设置。

与任何文本字段一样，你可以设置列数：

```java
intField.setColumns(6);
```

你可以使用 `setValue` 方法设置默认值。该方法接受一个 `Object` 参数，因此需要将默认 `int` 值包装在 `Integer` 对象中：

```java
intField.setValue(new Integer(100));
```

通常，用户会在多个文本字段中输入内容，然后单击按钮读取所有值。单击按钮时，你可以使用 `getValue` 方法获取用户提供的值。该方法返回一个 `Object` 结果，你需要将其强制转换为适当的类型。如果用户编辑了值，`JFormattedTextField` 会返回 `Long` 类型的对象。但是，如果用户没有做任何更改，则返回原来的 `Integer` 对象。因此，你应该将返回值强制转换为共同的超类 `Number`：

```java
Number value = (Number) intField.getValue();
int v = value.intValue();
```

格式化文本字段本身并没有太多有趣之处，直到你考虑当用户提供非法输入时会发生什么。这就是下一节的主题。

### 10.4.2.2 失去焦点时的行为

考虑当用户向文本字段提供输入时会发生什么。用户输入内容，并最终决定离开该字段，也许通过鼠标单击另一个组件。然后文本字段*失去焦点*。I 形光标不再在文本字段中可见，击键被定向到另一个组件。

当格式化文本字段失去焦点时，格式化器会查看用户生成的文本字符串。如果格式化器知道如何将文本字符串转换为对象，则该文本有效。否则无效。你可以使用 `isEditValid` 方法检查文本字段的当前内容是否有效。

失去焦点时的默认行为称为“提交或还原”。如果文本字符串有效，则将其*提交*。格式化器将其转换为对象。该对象成为字段的当前值（即你在上一节中看到的 `getValue` 方法的返回值）。然后该值被转换回字符串，成为字段中可见的文本字符串。例如，整数格式化器将输入 `1729` 识别为有效，将当前值设置为 `new Long(1729)`，并将其转换回带逗号的字符串：`1,729`。

相反，如果文本字符串无效，则当前值不变，文本字段*还原*为表示旧值的字符串。例如，如果用户输入坏值，例如 `x1`，则当文本字段失去焦点时，旧值会被恢复。

> **注意：** 整数格式化器认为，如果文本字符串以整数开头，则该字符串有效。例如，`1729x` 是有效字符串。它会被转换为数字 1729，然后格式化为字符串 `1,729`。
