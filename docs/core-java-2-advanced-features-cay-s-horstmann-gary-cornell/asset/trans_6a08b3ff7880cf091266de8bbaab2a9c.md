
你可以选择希望排序器使用的规范化程度。值 `Collator.NO_DECOMPOSITION` 完全不对字符串进行规范化。这个选项速度更快，但可能不适用于以多种形式表示字符的文本。默认值 `Collator.CANONICAL_DECOMPOSITION` 使用规范化形式 D。这对于包含重音符号但不包含连字的文本很有用。最后，“完全分解”使用规范化形式 KD。示例见表 7.7。

**表 7.7** 分解模式之间的差异

| 不分解 | 规范分解 | 完全分解 |
| --- | --- | --- |
| Å ≠ Å | Å = Å | Å = Å |
| ™ ≠ TM | ™ ≠ TM | ™ = TM |

让排序器多次分解同一个字符串是浪费的。如果一个字符串要与其他字符串进行多次比较，你可以将分解结果保存在 `collation key` 对象中。`getCollationKey` 方法返回一个 `CollationKey` 对象，你可以用它进行进一步、更快的比较。下面是一个示例：

```java
String a = . . .;
CollationKey akey = coll.getCollationKey(a);
if (akey.compareTo(coll.getCollationKey(b)) == 0) // fast comparison
    . . .
```

最后，即使不进行排序，你也可能希望将字符串转换为其规范化形式——例如，在将字符串存储到数据库或与另一个程序通信时。`java.text.Normalizer` 类执行规范化过程。例如，

```java
String name = "Ångström";
String normalized = Normalizer.normalize(name, Normalizer.Form.NFD); // uses normalization form D
```

规范化后的字符串包含十个字符。“Å”和“ö”被替换为“A”和“o”序列。

然而，这通常不是存储和传输的最佳形式。规范化形式 C 先应用分解，然后按标准化顺序重新组合重音符号。根据 W3C，这是通过互联网传输数据的推荐模式。

清单 7.4 中的程序让你可以试验排序顺序。在文本字段中输入一个单词，然后单击“添加”按钮将其添加到单词列表中。每次添加另一个单词，或更改区域设置、强度或分解模式时，单词列表都会再次排序。= 号表示被认为相同的单词（见图 7.3）。

![](img/7dd923a566750151a3aab0dacd0cdaa5_416_0.png)

**图 7.3** `CollationTest` 程序

组合框中的区域设置名称使用默认区域设置的排序器按排序顺序显示。如果你使用美式英语区域设置运行此程序，请注意，“Norwegian (Norway)”排在“Norwegian (Norway)”之前，即使逗号字符的 Unicode 值大于右括号的 Unicode 值。

## 清单 7.4 `collation/CollationTest.java`

```java
package collation;

import java.awt.*;
import java.awt.event.*;
import java.text.*;
import java.util.*;
import java.util.List;

import javax.swing.*;

/**
 * This program demonstrates collating strings under various locales.
 * @version 1.15 2015-06-05
 * @author Cay Horstmann
 */
public class CollationTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            JFrame frame = new CollationFrame();
            frame.setTitle("CollationTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame contains combo boxes to pick a locale, collation strength and decomposition rules,
 * a text field and button to add new strings, and a text area to list the collated strings.
 */
class CollationFrame extends JFrame
{
   private Collator collator = Collator.getInstance(Locale.getDefault());
   private List<String> strings = new ArrayList<>();
   private Collator currentCollator;
   private Locale[] locales;
   private JComboBox<String> localeCombo = new JComboBox<>();
   private JTextField newWord = new JTextField(20);
   private JTextArea sortedWords = new JTextArea(20, 20);
   private JButton addButton = new JButton("add");
   private EnumCombo<Integer> strengthCombo = new EnumCombo<>(Collator.class, "Primary",
         "Secondary", "Tertiary", "Identical");
   private EnumCombo<Integer> decompositionCombo = new EnumCombo<>(Collator.class,
         "Canonical Decomposition", "Full Decomposition", "No Decomposition");

   public CollationFrame()
   {
      setLayout(new GridBagLayout());
      add(new JLabel("Locale"), new GBC(0, 0).setAnchor(GBC.EAST));
      add(new JLabel("Strength"), new GBC(0, 1).setAnchor(GBC.EAST));
      add(new JLabel("Decomposition"), new GBC(0, 2).setAnchor(GBC.EAST));
      add(addButton, new GBC(0, 3).setAnchor(GBC.EAST));
      add(localeCombo, new GBC(1, 0).setAnchor(GBC.WEST));
      add(strengthCombo, new GBC(1, 1).setAnchor(GBC.WEST));
      add(decompositionCombo, new GBC(1, 2).setAnchor(GBC.WEST));
      add(newWord, new GBC(1, 3).setFill(GBC.HORIZONTAL));
      add(new JScrollPane(sortedWords), new GBC(0, 4, 2, 1).setFill(GBC.BOTH));

      locales = (Locale[]) Collator.getAvailableLocales().clone();
      Arrays.sort(
            locales, (l1, l2) -> collator.compare(l1.getDisplayName(), l2.getDisplayName()));
      for (Locale loc : locales)
         localeCombo.addItem(loc.getDisplayName());
      localeCombo.setSelectedItem(locale.getDefault().getDisplayName());

      strings.add("America");
      strings.add("able");
      strings.add("Zulu");
      strings.add("zebra");
      strings.add("\u00C5ngstr\u00F6m");
      strings.add("A\u00D8ngstr\u00D6m");
      strings.add("Angstrom");
      strings.add("Apple");
      strings.add("office");
      strings.add("\uFB03ce");
      strings.add("Java\u2122");
      strings.add("JavaTM");
      updateDisplay();

      addButton.addActionListener(event ->
      {
         strings.add(newWord.getText());
         updateDisplay();
      });

      ActionListener listener = event -> updateDisplay();

      localeCombo.addActionListener(listener);
      strengthCombo.addActionListener(listener);
      decompositionCombo.addActionListener(listener);
      pack();
   }

   /**
    * Updates the display and collates the strings according to the user settings.
    */
   public void updateDisplay()
   {
      Locale currentLocale = locales[localeCombo.getSelectedIndex()];
      localeCombo.setLocale(currentLocale);

      currentCollator = Collator.getInstance(currentLocale);
      currentCollator.setStrength(strengthCombo.getValue());
      currentCollator.setDecomposition(decompositionCombo.getValue());

      Collections.sort(strings, currentCollator);

      sortedWords.setText("");
      for (int i = 0; i < strings.size(); i++)
      {
         String s = strings.get(i);
         if (i > 0 && currentCollator.compare(s, strings.get(i - 1)) == 0)
            sortedWords.append("=");
         sortedWords.append(s + "\n");
      }
      pack();
   }
}
```

## java.text.Collator 1.1

- `static Locale[] getAvailableLocales()`
  - 返回一个 Locale 对象数组，这些对象有可用的 Collator 对象。
- `static Collator getInstance()`
- `static Collator getInstance(Locale l)`
  - 返回默认区域设置或给定区域设置的排序器。
- `int compare(String a, String b)`
  - 如果 a 排在 b 之前，则返回负值；如果它们被认为相同，则返回 0；否则返回正值。
- `boolean equals(String a, String b)`
  - 如果 a 和 b 被认为相同，则返回 true，否则返回 false。
- `void setStrength(int strength)`
- `int getStrength()`
  - 设置或获取排序器的强度。更强的排序器能区分更多单词。强度值为 Collator.PRIMARY、Collator.SECONDARY 和 Collator.TERTIARY。
- `void setDecomposition(int decomp)`
- `int getDecomposition()`
  - 设置或获取排序器的分解模式。排序器对字符串的分解越多，它在判断两个字符串是否应被视为相同时就越严格。分解值为 Collator.NO_DECOMPOSITION、Collator.CANONICAL_DECOMPOSITION 和 Collator.FULL_DECOMPOSITION。
- `CollationKey getCollationKey(String a)`
  - 返回一个排序键，其中包含字符的分解形式，可以快速与另一个排序键进行比较。
