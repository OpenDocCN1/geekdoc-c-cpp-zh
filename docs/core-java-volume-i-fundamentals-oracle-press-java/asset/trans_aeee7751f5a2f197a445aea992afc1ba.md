
重新发现它。

## 11.6.1.6 网格包布局诀窍

在实践中，以下诀窍能让网格包布局相对省心：

- 1. 在纸上勾勒出组件布局。
- 2. 找到一个网格，使小组件各自包含在一个单元格中，而较大的组件跨多个单元格。
- 3. 用 0、1、2、3、……标记网格的行和列。现在你就可以读出 gridx、gridy、gridwidth 和 gridheight 的值。
- 4. 对每个组件，问自己它是否需要水平或垂直填满其单元格。如果不需要，你希望它如何对齐？这会告诉你 fill 和 anchor 参数。
- 5. 将所有权重设为 100。不过，如果你希望某一行或某一列始终保持其默认大小，就把属于该行或该列的所有组件的 weightx 或 weighty 设为 0。
- 6. 编写代码。仔细复查你对 `GridBagConstraints` 的设置。一个错误的约束就可能毁掉整个布局。
- 7. 编译、运行，然后享受成果。

## 11.6.1.7 用于驯服网格包约束的辅助类

网格包布局最繁琐的方面是编写设置约束的代码。大多数程序员为此编写辅助函数或一个小型辅助类。我会在字体对话框示例的完整代码之后给出这样一个类。这个类具有以下特点：

- 它的名字很短：用 `GBC` 代替 `GridBagConstraints`。
- 它扩展了 `GridBagConstraints`，因此可以使用更短的名称（例如 `GBC.EAST`）来表示常量。
- 添加组件时使用 `GBC` 对象，例如

    ```java
    add(component, new GBC(1, 2));
    ```

- 有两个构造函数用于设置最常见的参数：`gridx` 和 `gridy`，或者 `gridx`、`gridy`、`gridwidth` 和 `gridheight`。

    ```java
    add(component, new GBC(1, 2, 1, 4));
    ```

- 对于成对出现的 x/y 字段，提供了便捷的 setter：

    ```java
    add(component, new GBC(1, 2).setWeight(100, 100));
    ```

- setter 方法返回 `this`，因此可以链式调用：

    ```java
    add(component, new GBC(1, 2).setAnchor(GBC.EAST).setWeight(100, 100));
    ```

- `setInsets` 方法会为你构造 `Insets` 对象。要获得一像素的内边距，只需调用

    ```java
    add(component, new GBC(1, 2).setAnchor(GBC.EAST).setInsets(1));
    ```

[清单 11.7](#) 展示了字体对话框示例的框架类。GBC 辅助类位于[清单 11.8](#)。以下是将组件添加到网格包中的代码：

```java
add(faceLabel, new GBC(0, 0).setAnchor(GBC.EAST));
add(face, new GBC(1, 0).setFill(GBC.HORIZONTAL).setWeight(100, 0).setInsets(1));
add(sizeLabel, new GBC(0, 1).setAnchor(GBC.EAST));
add(size, new GBC(1, 1).setFill(GBC.HORIZONTAL).setWeight(100, 0).setInsets(1));
add(bold, new GBC(0, 2, 2, 1).setAnchor(GBC.CENTER).setWeight(100, 100));
add(italic, new GBC(0, 3, 2, 1).setAnchor(GBC.CENTER).setWeight(100, 100));
add(sample, new GBC(2, 0, 1, 4).setFill(GBC.BOTH).setWeight(100, 100));
```

一旦理解了网格包约束，这类代码就相当容易阅读和调试。

### 清单 11.7 `gridbag/FontFrame.java`

```java
package gridbag;

import java.awt.Font;
import java.awt.GridBagLayout;
import java.awt.event.ActionListener;

import javax.swing.BorderFactory;
import javax.swing.JCheckBox;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextArea;

/**
 * A frame that uses a grid bag layout to arrange font selection components.
 */
public class FontFrame extends JFrame
{
   public static final int TEXT_ROWS = 10;
   public static final int TEXT_COLUMNS = 20;

   private JComboBox<String> face;
   private JComboBox<Integer> size;
   private JCheckBox bold;
   private JCheckBox italic;
   private JTextArea sample;

   public FontFrame()
   {
      var layout = new GridBagLayout();
      setLayout(layout);

      ActionListener listener = event -> updateSample();

      // construct components
37    var faceLabel = new JLabel("Face: ");
38
39    face = new JComboBox<>(new String[] { "Serif", "SansSerif", "Monospaced",
40        "Dialog", "DialogInput" });
41
42    face.addActionListener(listener);
43
44    var sizeLabel = new JLabel("Size: ");
45
46    size = new JComboBox<>(new Integer[] { 8, 10, 12, 15, 18, 24, 36, 48 });
47
48    size.addActionListener(listener);
49
50    bold = new JCheckBox("Bold");
51    bold.addActionListener(listener);
52
53    italic = new JCheckBox("Italic");
54    italic.addActionListener(listener);
55
56    sample = new JTextArea(TEXT_ROWS, TEXT_COLUMNS);
57    sample.setText("The quick brown fox jumps over the lazy dog");
58
59    sample.setEditable(false);
60    sample.setLineWrap(true);
61    sample.setBorder(BorderFactory.createEtchedBorder());
62
63    // add components to grid, using GBC convenience class
64
65    add(faceLabel, new GBC(0, 0).setAnchor(GBC.EAST));
66    add(face, new GBC(1, 0).setFill(GBC.HORIZONTAL).setWeight(100, 0).setInsets(1));
67    add(sizeLabel, new GBC(0, 1).setAnchor(GBC.EAST));
68    add(size, new GBC(1, 1).setFill(GBC.HORIZONTAL).setWeight(100, 0).setInsets(1));
69    add(bold, new GBC(0, 2, 2, 1).setAnchor(GBC.CENTER).setWeight(100, 100));
70    add(sample, new GBC(2, 0, 1, 4).setFill(GBC.BOTH).setWeight(100, 100));
71    pack();
72    updateSample();
73    }
74
75    public void updateSample()
76    {
77      var fontFace = (String) face.getSelectedItem();
78      int fontStyle = (bold.isSelected() ? Font.BOLD : 0)
79          + (italic.isSelected() ? Font.ITALIC : 0);
80      int fontSize = size.getItemAt(size.getSelectedIndex());
81      var font = new Font(fontFace, fontStyle, fontSize);
82      sample.setFont(font);
83      sample.repaint();
84    }
85  }
```

### 清单 11.8 `gridbag/GBC.java`

```java
1  package gridbag;
2
3  import java.awt.*;
4
5  /**
6   * This class simplifies the use of the GridBagConstraints class.
7   * @version 1.01 2004-05-06
8   * @author Cay Horstmann
9   */
10 public class GBC extends GridBagConstraints
11 {
12   /**
13    * Constructs a GBC with a given gridx and gridy position and all other grid
14    * bag constraint values set to the default.
15    * @param gridx the gridx position
16    * @param gridy the gridy position
17    */
18    public GBC(int gridx, int gridy)
19    {
20        this.gridx = gridx;
21        this.gridy = gridy;
22    }
23
24    /**
25     * Constructs a GBC with given gridx, gridy, gridwidth, gridheight and all
26     * other grid bag constraint values set to the default.
27     * @param gridx the gridx position
28     * @param gridy the gridy position
29     * @param gridwidth the cell span in x-direction
30     * @param gridheight the cell span in y-direction
31     */
32    public GBC(int gridx, int gridy, int gridwidth, int gridheight)
33    {
34        this.gridx = gridx;
35        this.gridy = gridy;
36        this.gridwidth = gridwidth;
37        this.gridheight = gridheight;
38    }
39
40    /**
41     * Sets the anchor.
42     * @param anchor the anchor value
43     * @return this object for further modification
44     */
45    public GBC setAnchor(int anchor)
46    {
47        this.anchor = anchor;
48        return this;
49    }
50
51    /**
52     * Sets the fill direction.
53     * @param fill the fill direction
54     * @return this object for further modification
55     */
56    public GBC setFill(int fill)
57    {
58        this.fill = fill;
59        return this;
60    }
61
62    /**
63     * Sets the cell weights.
64     * @param weightx the cell weight in x-direction
65     * @param weighty the cell weight in y-direction
66     * @return this object for further modification
67     */
68    public GBC setWeight(double weightx, double weighty)
69    {
70        this.weightx = weightx;
71        this.weighty = weighty;
72        return this;
73    }
74
75    /**
76     * Sets the insets of this cell.
77     * @param distance the spacing to use in all directions
78     * @return this object for further modification
79     */
80    public GBC setInsets(int distance)
81    {
82        this.insets = new Insets(distance, distance, distance,
83        distance);
84        return this;
85    }
86
87    /**
88     * Sets the insets of this cell.
89     * @param top the spacing to use on top
90     * @param left the spacing to use to the left
91     * @param bottom the spacing to use on the bottom
```
