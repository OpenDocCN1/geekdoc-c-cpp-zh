
除了构造区域设置或使用预定义区域设置之外，还有两种获取区域设置对象的方法。

`Locale` 类的静态 `getDefault` 方法最初获取本地操作系统存储的默认区域设置。可以通过调用 `setDefault` 更改默认 Java 区域设置；但是，该更改只影响你的程序，不影响操作系统。

所有依赖区域设置的实用工具类都可以返回它们支持的区域设置数组。例如，

```
Locale[] supportedLocales = NumberFormat.getAvailableLocales();
```

返回 NumberFormat 类可以处理的所有区域设置。

> **提示：** 如果要测试仅包含语言和国家/地区设置的区域设置，可以在启动程序时在命令行中提供这些设置。例如，下面我们将默认区域设置设为 `de-CH`：
>
> ```bash
> java -Duser.language=de -Duser.region=CH MyProgram
> ```

一旦获得区域设置，你能用它做什么？事实证明，能做的并不多。`Locale` 类中唯一有用的方法是用于标识语言和国家/地区代码的方法。最重要的一个是 `getDisplayName`。它返回描述该区域设置的字符串。该字符串不包含晦涩难懂的两个字母代码，而是采用可以呈现给用户的格式，例如

```
German (Switzerland)
```

实际上，这里有一个问题。显示名称是以默认区域设置给出的。这可能并不合适。如果你的用户已经选择德语作为首选语言，你可能希望用德语呈现该字符串。只需将德语区域设置作为参数传入即可做到这一点。以下代码

```
Locale loc = new Locale("de", "CH");
System.out.println(loc.getDisplayName(Locale.GERMAN));
```

输出

```
Deutsch (Schweiz)
```

这个例子说明了为什么需要区域设置对象。你将它们传递给感知区域设置的方法，这些方法生成的文本会呈现给不同地区的用户。在后续章节中，你会看到许多这样的例子。

### java.util.Locale 1.1

- `Locale(String language)`  
  `Locale(String language, String country)`  
  `Locale(String language, String country, String variant)`  
  使用给定的语言、国家/地区和变体构造区域设置。不要在新代码中使用变体——而应改用 IETF BCP 47 语言标签。
- `static Locale forLanguageTag(String languageTag)` 7  
  构造与给定语言标签对应的区域设置。
- `static Locale getDefault()`  
  返回默认区域设置。
- `static void setDefault(Locale loc)`  
  设置默认区域设置。
- `String getDisplayName()`  
  返回描述该区域设置的名称，以当前区域设置表示。
- `String getDisplayName(Locale loc)`  
  返回描述该区域设置的名称，以给定区域设置表示。
- `String getLanguage()`  
  返回语言代码，即小写两字母 ISO 639 代码。
- `String getDisplayLanguage()`  
  返回语言的名称，以当前区域设置表示。
- `String getDisplayLanguage(Locale loc)`  
  返回语言的名称，以给定区域设置表示。
- `String getCountry()`  
  以大写两字母 ISO 3166 代码返回国家/地区代码。
- `String getDisplayCountry()`  
  返回国家/地区的名称，以当前区域设置表示。
- `String getDisplayCountry(Locale loc)`  
  返回国家/地区的名称，以给定区域设置表示。
- `String toLanguageTag()` 7  
  返回此区域设置的 IETF BCP 47 语言标签，例如 "de-CH"。
- `String toString()`  
  返回区域设置的描述，其中语言和国家/地区以下划线分隔（例如 "de_CH"）。仅将此方法用于调试。

## 7.2 数字格式

我们已经提到，数字和货币格式高度依赖于区域设置。Java 库在 `java.text` 包中提供了一组格式化器对象，可以格式化和解析数值。要为特定区域设置格式化数字，请执行以下步骤：

1. 获取区域设置对象，如上一节所述。
2. 使用“工厂方法”获取格式化器对象。
3. 使用该格式化器对象进行格式化和解析。

这些工厂方法是 `NumberFormat` 类的静态方法，接受一个 `Locale` 参数。共有三个工厂方法：`getNumberInstance`、`getCurrencyInstance` 和 `getPercentInstance`。这些方法分别返回可以格式化和解析数字、货币金额和百分比的对象。例如，以下是在德语中格式化货币值的方法：

```java
Locale loc = Locale.GERMAN;
NumberFormat currFmt = NumberFormat.getCurrencyInstance(loc);
double amt = 123456.78;
String result = currFmt.format(amt);
```

结果为

`123.456,78 €`

请注意，货币符号是 €，并且它位于字符串末尾。另外，请注意小数点和十进制逗号的位置是相反的。

反过来，要读取按照某个区域设置的约定输入或存储的数字，请使用 parse 方法。例如，以下代码解析用户在文本字段中输入的值。parse 方法可以处理小数点和逗号，以及其他语言中的数字字符。

```java
TextField inputField;
...
NumberFormat fmt = NumberFormat.getNumberInstance();
// get the number formatter for default locale
Number input = fmt.parse(inputField.getText().trim());
double x = input.doubleValue();
```

parse 的返回类型是抽象类型 Number。返回的对象要么是 Double 包装对象，要么是 Long 包装对象，取决于解析的数字是否为浮点数。如果你不关心这种区别，可以直接使用 Number 类的 doubleValue 方法获取包装的数值。

> **注意：** `Number` 类型的对象不会自动拆箱——不能简单地将 `Number` 对象赋给基本类型。而应使用 `doubleValue` 或 `intValue` 方法。

如果数字文本的格式不正确，该方法会抛出 `ParseException`。例如，字符串中的前导空白是*不允许的*。（调用 `trim` 将其移除。）但是，字符串中数字后面的任何字符都会被直接忽略，因此不会抛出异常。

请注意，`getXxxInstance` 工厂方法返回的类实际上并不是 `NumberFormat` 类型。`NumberFormat` 类型是一个抽象类，实际的格式化器属于它的某个子类。工厂方法只是知道如何定位属于特定区域设置的对象。

可以使用静态 `getAvailableLocales` 方法获取当前支持的区域设置列表。该方法返回一个区域设置数组，对于这些区域设置可以获取数字格式化器对象。

本节的示例程序让你可以试验各种数字格式化器（见图 7.1）。图中顶部的组合框包含所有带数字格式化器的区域设置。你可以在数字、货币和百分比格式化器之间进行选择。每次做出其他选择时，文本字段中的数字都会重新格式化。如果你浏览几个区域设置，就能很好地了解数字或货币值的多种格式化方式。你也可以输入不同的数字，并单击 Parse 按钮来调用 parse 方法，它会尝试解析你输入的内容。如果输入解析成功，就会将其传给 format 并显示结果。如果解析失败，文本字段中会显示“Parse error”消息。

![](img/7dd923a566750151a3aab0dacd0cdaa5_399_0.png)

**图 7.1** `NumberFormatTest` 程序

清单 7.1 中显示的代码相当直接。在构造器中，我们调用 `NumberFormat.getAvailableLocales`。对于每个区域设置，我们调用 `getDisplayName`，并用 `getDisplayName` 方法返回的字符串填充组合框。（这些字符串未排序；我们将在第 393 页的 7.5 节“排序规则与规范化”中处理这个问题。）每当用户选择另一个区域设置或单击某个单选按钮时，
