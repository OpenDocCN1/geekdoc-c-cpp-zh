
## 清单 7.2 `dateFormat/DateTimeFormatterTest.java`

```java
package dateFormat;

import java.awt.*;
import java.awt.event.*;
import java.time.*;
import java.time.format.*;
import java.util.*;

import javax.swing.*;

/**
 * This program demonstrates formatting dates under various locales.
 * @version 1.00 2016-05-06
 * @author Cay Horstmann
 */
public class DateTimeFormatterTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            JFrame frame = new DateTimeFormatterFrame();
            frame.setTitle("DateTimeFormatterTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame contains combo boxes to pick a locale, date and time formats, text fields to display
 * formatted date and time, buttons to parse the text field contents, and a "lenient" check box.
 */
class DateTimeFormatterFrame extends JFrame
{
   private Locale[] locales;
   private LocalDate currentDate;
   private LocalTime currentTime;
   private ZonedDateTime currentDateTime;
   private DateTimeFormatter currentDateFormat;
   private DateTimeFormatter currentTimeFormat;
   private DateTimeFormatter currentDateTimeFormat;
   private JComboBox<String> localeCombo = new JComboBox<>();
   private JButton dateParseButton = new JButton("Parse");
   private JButton timeParseButton = new JButton("Parse");
   private JButton dateTimeParseButton = new JButton("Parse");
   private JTextField dateText = new JTextField(30);
   private JTextField timeText = new JTextField(30);
   private JTextField dateTimeText = new JTextField(30);
   private EnumCombo<FormatStyle> dateStyleCombo = new EnumCombo<>(FormatStyle.class,
         "Short", "Medium", "Long", "Full");
   private EnumCombo<FormatStyle> timeStyleCombo = new EnumCombo<>(FormatStyle.class,
         "Short", "Medium");
   private EnumCombo<FormatStyle> dateTimeStyleCombo = new EnumCombo<>(FormatStyle.class,
         "Short", "Medium", "Long", "Full");

   public DateTimeFormatterFrame()
   {
      setLayout(new GridBagLayout());
      add(new JLabel("Locale"), new GBC(0, 0).setAnchor(GBC.EAST));
      add(localeCombo, new GBC(1, 0, 2, 1).setAnchor(GBC.WEST));

      add(new JLabel("Date"), new GBC(0, 1).setAnchor(GBC.EAST));
      add(dateStyleCombo, new GBC(1, 1).setAnchor(GBC.WEST));
      add(dateText, new GBC(2, 1, 2, 1).setFill(GBC.HORIZONTAL));
      add(dateParseButton, new GBC(4, 1).setAnchor(GBC.WEST));

      add(new JLabel("Time"), new GBC(0, 2).setAnchor(GBC.EAST));
      add(timeStyleCombo, new GBC(1, 2).setAnchor(GBC.WEST));
      add(timeText, new GBC(2, 2, 2, 1).setFill(GBC.HORIZONTAL));
      add(timeParseButton, new GBC(4, 2).setAnchor(GBC.WEST));

      add(new JLabel("Date and time"), new GBC(0, 3).setAnchor(GBC.EAST));
      add(dateTimeStyleCombo, new GBC(1, 3).setAnchor(GBC.WEST));
      add(dateTimeText, new GBC(2, 3, 2, 1).setFill(GBC.HORIZONTAL));
      add(dateTimeParseButton, new GBC(4, 3).setAnchor(GBC.WEST));

      locales = (Locale[]) Locale.getAvailableLocales().clone();
      Arrays.sort(locales, Comparator.comparing(Locale::getDisplayName));
      for (Locale locale : locales)
         localeCombo.addItem(locale.getDisplayName());
      localeCombo.setSelectedItem(Locale.getDefault().getDisplayName());
      currentDate = LocalDate.now();
      currentTime = LocalTime.now();
      currentDateTime = ZonedDateTime.now();
      updateDisplay();

      ActionListener listener = event -> updateDisplay();

      localeCombo.addActionListener(listener);
      dateStyleCombo.addActionListener(listener);
      timeStyleCombo.addActionListener(listener);
      dateTimeStyleCombo.addActionListener(listener);

      dateParseButton.addActionListener(event ->
      {
         String d = dateText.getText().trim();
         try
         {
            currentDate = LocalDate.parse(d, currentDateFormat);
            updateDisplay();
         }
         catch (Exception e)
         {
            dateText.setText(e.getMessage());
         }
      });

      timeParseButton.addActionListener(event ->
      {
         String t = timeText.getText().trim();
         try
         {
            currentTime = LocalTime.parse(t, currentTimeFormat);
            updateDisplay();
         }
         catch (Exception e)
         {
            timeText.setText(e.getMessage());
         }
      });

      dateTimeParseButton.addActionListener(event ->
      {
         String t = dateTimeText.getText().trim();
         try
         {
            currentDateTime = ZonedDateTime.parse(t, currentDateTimeFormat);
            updateDisplay();
         }
         catch (Exception e)
         {
            dateTimeText.setText(e.getMessage());
         }
      });

      pack();
   }

   /**
    * Updates the display and formats the date according to the user settings.
    */
   public void updateDisplay()
   {
      Locale currentLocale = locales[localeCombo.getSelectedIndex()];
      FormatStyle dateStyle = dateStyleCombo.getValue();
      currentDateFormat = DateTimeFormatter.ofLocalizedDate(
            dateStyle).withLocale(currentLocale);
      dateText.setText(currentDateFormat.format(currentDate));
      FormatStyle timeStyle = timeStyleCombo.getValue();
      currentTimeFormat = DateTimeFormatter.ofLocalizedTime(
            timeStyle).withLocale(currentLocale);
      timeText.setText(currentTimeFormat.format(currentTime));
      FormatStyle dateTimeStyle = dateTimeStyleCombo.getValue();
      currentDateTimeFormat = DateTimeFormatter.ofLocalizedDateTime(
            dateTimeStyle).withLocale(currentLocale);
      dateTimeText.setText(currentDateTimeFormat.format(currentDateTime));
   }
}
```

## 清单 7.3 `dateFormat/EnumCombo.java`

```java
package dateFormat;

import java.util.*;
import javax.swing.*;

/**
 * A combo box that lets users choose from among static field
 * values whose names are given in the constructor.
 * @version 1.5 2015-06-05
 * @author Cay Horstmann
 */
public class EnumCombo<T> extends JComboBox<String>
{
   private Map<String, T> table = new TreeMap<>();

   /**
    * Constructs an EnumCombo yielding values of type T.
    * @param cl a class
    * @param labels an array of strings describing static field names
    * of cl that have type T
    */
   public EnumCombo(Class<?> cl, String... labels)
   {
      for (String label : labels)
      {
         String name = label.toUpperCase().replace(' ', '_');
         try
         {
            java.lang.reflect.Field f = cl.getField(name);
            @SuppressWarnings("unchecked") T value = (T) f.get(cl);
            table.put(label, value);
         }
         catch (Exception e)
         {
            label = "(" + label + ")";
            table.put(label, null);
         }
         addItem(label);
      }
      setSelectedItem(labels[0]);
   }

   /**
    * Returns the value of the field that the user selected.
    * @return the static field value
    */
   public T getValue()
   {
      return table.get(getSelectedItem());
   }
}
```

## java.time.format.DateTimeFormatter 8

- `static DateTimeFormatter ofLocalizedDate(FormatStyle dateStyle)`
- `static DateTimeFormatter ofLocalizedTime(FormatStyle timeStyle)`
- `static DateTimeFormatter ofLocalizedDateTime(FormatStyle dateTimeStyle)`
- `static DateTimeFormatter ofLocalizedDateTime(FormatStyle dateStyle, FormatStyle timeStyle)`
  返回用指定样式格式化日期、时间或日期和时间的 DateTimeFormatter 实例。
- `DateTimeFormatter withLocale(Locale locale)`
  返回具有给定区域设置的此格式化器的副本。
- `String format(TemporalAccessor temporal)`
  返回格式化给定日期/时间后得到的字符串。

```java
Collator coll = Collator.getInstance(locale);
words.sort(coll); // Collator implements Comparator<Object>
```

由于 Collator 类实现了 Comparator 接口，你可以将 Collator 对象传递给 List.sort(Comparator) 方法，以对字符串列表进行排序。

排序器有几项高级设置。你可以设置排序器的*强度*，以选择其区分程度。字符差异被分为*主级*、*次级*或*三级*。例如，在英语中，“A”和“Z”之间的差异被视为主级，“A”和“Ä”之间的差异为次级，而“A”和“a”之间的差异为三级。

通过将排序器的强度设置为 Collator.PRIMARY，你告诉它只关注主级差异。通过将强度设置为 Collator.SECONDARY，你指示排序器考虑次级差异。也就是说，当强度设置为“次级”或“三级”时，两个字符串更有可能被视为不同，如表 7.6 所示。

**表 7.6** 不同强度的排序规则（英语区域设置）

| 主级 | 次级 | 三级 |
|---|---|---|
| Angstrom = Ångström | Angstrom ≠ Ångström | Angstrom ≠ Ångström |
| Able = able | Able = able | Able ≠ able |

当强度设置为 Collator.IDENTICAL 时，不允许任何差异。此设置主要与一个相当技术性的排序器设置——*分解模式*——结合使用时有用，我们接下来会讨论它。

有时，一个字符或字符序列在 Unicode 中可以有不止一种描述方式。例如，“Å”可以是 Unicode 字符 U+00C5，也可以表示为一个普通 A（U+0041）后跟一个 °（“combining ring above”；U+030A）。也许更令人惊讶的是，字母序列“ffi”可以用单个字符“Latin small ligature ffi”来描述，其代码为 U+FB03。（有人可能会争辩说，这是一个呈现问题，不应导致不同的 Unicode 字符，但规则不是我们制定的。）

Unicode 标准为字符串定义了四种*规范化形式*（D、KD、C 和 KC）。详情请参见 www.unicode.org/unicode/reports/tr15/tr15-23.html。在规范化形式 C 中，带重音字符总是被组合。例如，A 与一个上方的组合环 ° 组成的序列会组合成单个字符 Å。在形式 D 中，带重音字符总是被分解为基本字母和组合重音：Å 会变成 A 后跟 °。形式 KC 和 KD 还会分解连字或商标符号等字符。

