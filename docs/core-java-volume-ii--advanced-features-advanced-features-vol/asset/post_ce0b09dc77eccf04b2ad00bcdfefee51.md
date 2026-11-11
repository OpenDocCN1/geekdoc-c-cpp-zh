
### java.util.Currency

1.4

- `static Currency getInstance(String currencyCode)`
- `static Currency getInstance(Locale locale)`
  - returns the Currency instance for the given ISO 4217 currency code or the country of the given locale.
- `String toString()`
- `String getCurrencyCode()`
- `int getNumericCode()` 7
- `String getNumericCodeAsString()` 9
  - gets the ISO 4217 alphabetic or numeric currency code of this currency.
- `String getSymbol()`
- `String getSymbol(Locale locale)`
  - gets the formatting symbol of this currency for the default locale or the given locale. For example, the symbol for USD can be "$" or "US$", depending on the locale.
- `int getDefaultFractionDigits()`
  - gets the default number of fraction digits of this currency.
- `static Set<Currency> getAvailableCurrencies()` 7
  - gets all available currencies.

### 7.3 Date and Time

When you are formatting date and time, you should be concerned with four locale-dependent issues:

- The names of months and weekdays should be presented in the local language.
- There will be local preferences for the order of year, month, and day.
- The Gregorian calendar might not be the local preference for expressing dates.
- The time zone of the location must be taken into account.

The `DateTimeFormatter` class from the `java.time` package handles these issues. Pick one of the formatting styles shown in Tables 7.4. Then, get a formatter:

```java
FormatStyle style = ...; // One of FormatStyle.SHORT, FormatStyle.MEDIUM, ...
DateTimeFormatter dateFormatter = DateTimeFormatter.ofLocalizedDate(style);
DateTimeFormatter timeFormatter = DateTimeFormatter.ofLocalizedTime(style);
```

```java
DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofLocalizedDateTime(style);
    // or DateTimeFormatter.ofLocalizedDateTime(style, style2)
```

These formatters use the current locale. To use a different locale, use the `withLocale` method:

```java
DateTimeFormatter dateTimeFormatter =
    DateTimeFormatter.ofLocalizedDateTime(style).withLocale(locale);
```

Now you can format a `LocalDate`, `LocalDateTime`, `LocalTime`, or `ZonedDateTime`:

```java
ZonedDateTime appointment = . . .;
String formatted = formatter.format(appointment);
```

### Table 7.4 Date and Time Formatting Styles

| Style | Date | Time |
|---|---|---|
| SHORT | 7/16/69 | 9:32 AM |
| MEDIUM | Jul 16, 1969 | 9:32:00 AM |
| LONG | July 16, 1969 | 9:32:00 AM EDT in en-US, 9:32:00 MESZ in de-DE (only for ZonedDateTime) |
| FULL | Wednesday, July 16, 1969 | 9:32:00 AM EDT in en-US, 9:32 Uhr MESZ in de-DE (only for ZonedDateTime) |

> **NOTE:** Here we use the `DateTimeFormatter` class from the `java.time` package. There is also a legacy `java.text.DateFormat` class from Java 1.1 that works with `Date` and `Calendar` objects.

You can use one of the static `parse` methods of `LocalDate`, `LocalDateTime`, `LocalTime`, or `ZonedDateTime` to parse a date or time in a string:

```java
LocalTime time = LocalTime.parse("9:32 AM", formatter);
```

These methods are not suitable for parsing human input, at least not without preprocessing. For example, the short time formatter for the United States will parse "9:32 AM" but not "9:32am" or "9:32 am".

> **CAUTION:** Date formatters parse nonexistent dates, such as November 31, and adjust them to the last date in the given month.

Sometimes, you need to display just the names of weekdays and months, for example, in a calendar application. Call the `getDisplayName` method of the `DayOfWeek` and `Month` enumerations.

```java
for (Month m : Month.values())
    System.out.println(m.getDisplayName(textStyle, locale) + " ");
```

Table 7.5 shows the text styles. The STANDALONE versions are for display outside a formatted date. For example, in Finnish, January is “tammikuuta” inside a date, but “tammikuu” standalone.

### Table 7.5 Values of the `java.time.format.TextStyle` Enumeration

| Style | Example |
|---|---|
| FULL / FULL_STANDALONE | January |
| SHORT / SHORT_STANDALONE | Jan |
| NARROW / NARROW_STANDALONE | J |

> **NOTE:** The first day of the week can be Saturday, Sunday, or Monday, depending on the locale. You can obtain it like this:

```java
DayOfWeek first = WeekFields.of(locale).getFirstDayOfWeek();
```

Listing 7.2 shows the `DateFormat` class in action. You can select a locale and see how the date and time are formatted in different places around the world. Figure 7.2 shows the program (after Chinese fonts were installed). As you can see, it correctly displays the output.

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_418_0.png)

**Figure 7.2** The DateFormatTest program

You can also experiment with parsing. Enter a date, time, or date/time and click the Parse button.

We use a helper class `EnumCombo` to solve a technical problem (see Listing 7.3). We wanted to fill a combo with values such as Short, Medium, and Long and then automatically convert the user’s selection to values `FormatStyle.SHORT`, `FormatStyle.MEDIUM`, and `FormatStyle.LONG`. Instead of writing repetitive code, we use reflection: We convert the user’s choice to upper case, replace all spaces with underscores, and then find the value of the static field with that name. (See Volume I, Chapter 5 for more details about reflection.)

### Listing 7.2 DateFormat/DateTimeFormatterTest.java

```java
package dateformat;

import java.awt.*;
import java.awt.event.*;
import java.time.*;
import java.time.format.*;
import java.util.*;

import javax.swing.*;

/**
 * This program demonstrates formatting dates under various locales.
 * @version 1.01 2018-05-01
 * @author Cay Horstmann
 */
public class DateTimeFormatterTest
{
   public static void main(String[] args)
   {
      EventQueue.invokeLater(() ->
         {
            var frame = new DateTimeFormatterFrame();
            frame.setTitle("DateFormatTest");
            frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
            frame.setVisible(true);
         });
   }
}

/**
 * This frame contains combo boxes to pick a locale, date and time formats,
 * text fields to display formatted date and time, and
 * buttons to parse the text field contents.
 */
class DateTimeFormatterFrame extends JFrame
{
   private Locale[] locales;
   private LocalDate currentDate;
   private LocalTime currentTime;
   private ZoneId currentZone;
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
      add(localeCombo, new GBC(1, 0, 1, 1).setAnchor(GBC.WEST));

      add(new JLabel("Date"), new GBC(0, 1).setAnchor(GBC.EAST));
      add(dateStyleCombo, new GBC(1, 1).setAnchor(GBC.WEST));
      add(dateText, new GBC(2, 1, 1, 1).setFill(GBC.HORIZONTAL));
      add(dateParseButton, new GBC(4, 1).setAnchor(GBC.WEST));

      add(new JLabel("Time"), new GBC(0, 2).setAnchor(GBC.EAST));
      add(timeStyleCombo, new GBC(1, 2).setAnchor(GBC.WEST));
      add(timeText, new GBC(2, 2, 1, 1).setFill(GBC.HORIZONTAL));
      add(timeParseButton, new GBC(4, 2).setAnchor(GBC.WEST));

      add(new JLabel("Date and time"), new GBC(0, 3).setAnchor(GBC.EAST));
      add(dateTimeStyleCombo, new GBC(1, 3).setAnchor(GBC.WEST));
      add(dateTimeText, new GBC(2, 3, 2, 1).setFill(GBC.HORIZONTAL));
      add(dateTimeParseButton, new GBC(4, 3).setAnchor(GBC.WEST));

      locales = (Locale[]) Locale.getAvailableLocales().clone();
      Arrays.sort(locales, Comparator.comparing(Locale::getDisplayName));
      for (Locale loc : locales)
         localeCombo.addItem(loc.getDisplayName());
      localeCombo.setSelectedItem(Locale.getDefault().getDisplayName());
      currentDate = LocalDate.now();
      currentTime = LocalTime.now();
      currentDateTime = ZonedDateTime.now();
      updateDisplay();

      ActionListener listener = event -> updateDisplay();
      localeCombo.addActionListener(listener);
      dateStyleCombo.addActionListener(listener);
      timeStyleCombo.addActionListener(listener);
```
