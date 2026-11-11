
![](img/7dd923a566750151a3aab0dacd0cdaa5_724_0.png)

**图 10.38** JSpinner 组件的几种变体

默认情况下，微调器管理一个整数，按钮会使其递增或递减 1。你可以通过调用 `getValue` 方法获取当前值。该方法返回一个 Object。将其强制转换为 Integer，并取出包装的值。

```java
JSpinner defaultSpinner = new JSpinner();
...
int value = (Integer) defaultSpinner.getValue();
```

你可以将增量改为 1 以外的值，并提供上下界。下面是一个起始值为 5、增量为 0.5、范围在 0 到 10 之间的微调器：

```java
JSpinner boundedSpinner = new JSpinner(new SpinnerNumberModel(5, 0, 10, 0.5));
```

有两个 `SpinnerNumberModel` 构造器，一个只接受 int 参数，一个接受 double 参数。如果任何一个参数是浮点数，则使用第二个构造器。它将微调器的值设置为 Double 对象。

微调器并不仅限于数值。你可以让微调器遍历任意值集合。只需将一个 `SpinnerListModel` 传给 `JSpinner` 构造器。你可以通过一个数组或实现了 `List` 接口的类（如 `ArrayList`）来构造 `SpinnerListModel`。在我们的示例程序中，我们显示了一个包含所有可用字体名称的微调器控件。

```java
String[] fonts = GraphicsEnvironment.getLocalGraphicsEnvironment().getAvailableFontFamilyNames();
JSpinner listSpinner = new JSpinner(new SpinnerListModel(fonts));
```

然而，我们发现遍历的方向有些令人困惑，因为它与组合框的方向相反。在组合框中，较大的值在较小值的下方，因此你会期望向下箭头导航到较大的值。但微调器递增数组索引，因此向上箭头会产生较大的值。`SpinnerListModel` 中并没有提供反转遍历顺序的规定，但一个临时的匿名子类可以得到所需结果：

```java
JSpinner reverseListSpinner = new JSpinner(
    new SpinnerListModel(fonts)
    {
        public Object getNextValue()
        {
            return super.getPreviousValue();
        }

        public Object getPreviousValue()
        {
            return super.getNextValue();
        }
    });
```

尝试这两个版本，看看哪一个更符合你的直觉。

微调器的另一个好用途是用于日期，用户可以递增或递减日期。通过下面的调用，你可以获得一个以今天日期初始化的微调器：

```java
JSpinner dateSpinner = new JSpinner(new SpinnerDateModel());
```

然而，如果你查看图 10.38，你会看到微调器文本同时显示日期和时间，例如：

```
8/05/07 9:05 PM
```

对于日期选择器来说，时间没有任何意义。事实证明，要让微调器只显示日期是有些困难的。下面是一个神奇的调用方式：

```java
JSpinner betterDateSpinner = new JSpinner(new SpinnerDateModel());
String pattern = ((SimpleDateFormat) DateFormat.getDateInstance()).toPattern();
betterDateSpinner.setEditor(new JSpinner.DateEditor(betterDateSpinner, pattern));
```

使用相同的方法，你还可以制作一个时间选择器：

```java
JSpinner timeSpinner = new JSpinner(new SpinnerDateModel());
pattern = ((SimpleDateFormat) DateFormat.getTimeInstance(DateFormat.SHORT)).toPattern();
timeSpinner.setEditor(new JSpinner.DateEditor(timeSpinner, pattern));
```

你可以通过定义自己的微调器模型，在微调器中显示任意序列。在我们的示例程序中，有一个微调器会遍历字符串 "meat" 的所有排列。通过点击微调器箭头，你可以得到 "mate"、"meta"、"team" 以及其余的 24 种排列。

要定义你自己的模型，请扩展 `AbstractSpinnerModel` 类并定义以下四个方法：

```java
Object getValue()
void setValue(Object value)
Object getNextValue()
Object getPreviousValue()
```

`getValue` 方法返回模型存储的值。`setValue` 方法设置一个新值。如果新值不合适，它应该抛出 `IllegalArgumentException`。

> **注意：** `setValue` 方法在设置新值后必须调用 `fireStateChanged` 方法。否则，微调器文本框将不会被更新。

`getNextValue` 和 `getPreviousValue` 方法返回当前值之后或之前应出现的值，如果遍历已经达到末尾，则返回 `null`。

> **注意：** `getNextValue` 和 `getPreviousValue` 方法**不应**更改当前值。当用户点击微调器的向上箭头时，会调用 `getNextValue` 方法。如果返回值为 `null`，则通过调用 `setValue` 对其进行设置。

在示例程序中，我们使用标准算法来确定下一个和上一个排列（参见清单 10.24）。算法的细节并不重要。

清单 10.23 展示了如何生成各种微调器类型。单击 OK 按钮即可查看微调器的值。

### 清单 10.23 — `spinner/SpinnerFrame.java`

```java
package spinner;

import java.awt.*;
import java.awt.event.*;
import javax.swing.text.*;
import javax.swing.*;

/**
 * A frame with a panel that contains several spinners and a button that displays the spinner
 * values.
 */
public class SpinnerFrame extends JFrame
{
    private JPanel mainPanel;
    private JButton okButton;

    public SpinnerFrame()
    {
        JPanel buttonPanel = new JPanel();
        okButton = new JButton("OK");
        buttonPanel.add(okButton);
        add(buttonPanel, BorderLayout.SOUTH);

        mainPanel = new JPanel();
        mainPanel.setLayout(new GridLayout(0, 3));
        add(mainPanel, BorderLayout.CENTER);

        JSpinner defaultSpinner = new JSpinner();
        addRow("Default", defaultSpinner);

        JSpinner boundedSpinner = new JSpinner(new SpinnerNumberModel(5, 0, 10, 0.5));
        addRow("Bounded", boundedSpinner);

        String[] fonts = GraphicsEnvironment.getLocalGraphicsEnvironment()
            .getAvailableFontFamilyNames();

        JSpinner listSpinner = new JSpinner(new SpinnerListModel(fonts));
        addRow("List", listSpinner);

        JSpinner reverseListSpinner = new JSpinner(new SpinnerListModel(fonts)
            {
                public Object getNextValue() { return super.getPreviousValue(); }
                public Object getPreviousValue() { return super.getNextValue(); }
            });
        addRow("Reverse List", reverseListSpinner);

        JSpinner dateSpinner = new JSpinner(new SpinnerDateModel());
        addRow("Date", dateSpinner);

        JSpinner betterDateSpinner = new JSpinner(new SpinnerDateModel());
        String pattern = ((SimpleDateFormat) DateFormat.getDateInstance()).toPattern();
        betterDateSpinner.setEditor(new JSpinner.DateEditor(betterDateSpinner, pattern));
        addRow("Better Date", betterDateSpinner);

        JSpinner timeSpinner = new JSpinner(new SpinnerDateModel());
        pattern = ((SimpleDateFormat) DateFormat.getTimeInstance(DateFormat.SHORT)).toPattern();
        timeSpinner.setEditor(new JSpinner.DateEditor(timeSpinner, pattern));
        addRow("Time", timeSpinner);

        JSpinner permSpinner = new JSpinner(new PermutationSpinnerModel("meat"));
        addRow("Word permutations", permSpinner);
        pack();
    }

    /**
     * Adds a row to the main panel.
     * @param labelText the label of the spinner
     * @param spinner the sample spinner
     */
    public void addRow(String labelText, final JSpinner spinner)
    {
        mainPanel.add(new JLabel(labelText));
        mainPanel.add(spinner);
        final JLabel valueLabel = new JLabel();
        mainPanel.add(valueLabel);
        okButton.addActionListener(event ->
        {
            Object value = spinner.getValue();
            valueLabel.setText(value.toString());
        });
    }
}
```

### 清单 10.24 `spinner/PermutationSpinnerModel.java`

```java
package spinner;

import javax.swing.*;

/**
 * A model that dynamically generates word permutations.
 */
public class PermutationSpinnerModel extends AbstractSpinnerModel
{
    private String word;

    /**
     * Constructs the model.
     * @param w the word to permute
     */
    public PermutationSpinnerModel(String w)
    {
        word = w;
    }

    public Object getValue()
    {
        return word;
    }
}
```
