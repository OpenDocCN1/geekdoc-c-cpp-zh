```
```java
for (Month m : Month.values())
    System.out.println(m.getDisplayName(textStyle, locale) + " ");
```
```

Table 7.5 shows the text styles. The STANDALONE versions are for display outside a formatted date. For example, in Finnish, January is “tammikuuta” inside a date, but “tammikuu” standalone.

**Table 7.5** Values of the `java.time.format.TextStyle` Enumeration

| Style | Example |
|---|---|
| FULL / FULL_STANDALONE | January |
| SHORT / SHORT_STANDALONE | Jan |
| NARROW / NARROW_STANDALONE | J |

> > **NOTE:** The first day of the week can be Saturday, Sunday, or Monday, depending on the locale. You can obtain it like this:

```
```java
DayOfWeek first = WeekFields.of(locale).getFirstDayOfWeek();
```
```

Listing 7.2 shows the `DateFormat` class in action. You can select a locale and see how the date and time are formatted in different places around the world. Figure 7.2 shows the program (after Chinese fonts were installed). As you can see, it correctly displays the output.

![](bbox=[0.28, 0.575, 0.8, 0.685])

**Figure 7.2** The DateFormatTest program

You can also experiment with parsing. Enter a date, time, or date/time and click the Parse button.

We use a helper class `EnumCombo` to solve a technical problem (see Listing 7.3). We wanted to fill a combo with values such as Short, Medium, and Long and then automatically convert the user’s selection to values `FormatStyle.SHORT`, `FormatStyle.MEDIUM`, and `FormatStyle.LONG`. Instead of writing repetitive code, we use reflection: We convert the user’s choice to upper case, replace all spaces with underscores, and then find the value of the static field with that name. (See Volume I, Chapter 5 for more details about reflection.)