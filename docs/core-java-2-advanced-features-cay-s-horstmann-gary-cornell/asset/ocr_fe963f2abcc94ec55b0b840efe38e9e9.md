> **CAUTION:** Objects of type `Number` are not automatically unboxed—you cannot simply assign a `Number` object to a primitive type. Instead, use the `doubleValue` or `intValue` method.

If the text for the number is not in the correct form, the method throws a `ParseException`. For example, leading whitespace in the string is *not allowed*. (Call `trim` to remove it.) However, any characters that follow the number in the string are simply ignored, so no exception is thrown.

Note that the classes returned by the `getXxxInstance` factory methods are not actually of type `NumberFormat`. The `NumberFormat` type is an abstract class, and the actual formatters belong to one of its subclasses. The factory methods merely know how to locate the object that belongs to a particular locale.

You can get a list of the currently supported locales with the static `getAvailableLocales` method. That method returns an array of the locales for which number formatter objects can be obtained.

The sample program for this section lets you experiment with number formatters (see Figure 7.1). The combo box at the top of the figure contains all locales with number formatters. You can choose between number, currency, and percentage formatters. Each time you make another choice, the number in the text field is reformatted. If you go through a few locales, you can get a good impression of the many ways that a number or currency value can be formatted. You can also type a different number and click the Parse button to call the parse method, which tries to parse what you entered. If your input is successfully parsed, it is passed to format and the result is displayed. If parsing fails, then a “Parse error” message is displayed in the text field.

![](bbox=[0.197, 0.663, 0.716, 0.774])

**Figure 7.1** The `NumberFormatTest` program

The code, shown in Listing 7.1, is fairly straightforward. In the constructor, we call `NumberFormat.getAvailableLocales`. For each locale, we call `getDisplayName` and fill a combo box with the strings that the `getDisplayName` method returns. (The strings are not sorted; we tackle this issue in Section 7.5, “Collation and Normalization,” on p. 393.) Whenever the user selects another locale or clicks one of the radio buttons,