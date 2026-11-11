
```text
computeButton=Rechnen
colorName=black
defaultPaperSize=210x297
```

然后按上一节所述为属性文件命名，例如：

```text
MyProgramStrings.properties
MyProgramStrings_en.properties
MyProgramStrings_de_DE.properties
```

可以像下面这样简单地加载资源包：

```java
ResourceBundle bundle = ResourceBundle.getBundle("MyProgramStrings", locale);
```

要查找特定字符串，请调用

```java
String computeButtonLabel = bundle.getString("computeButton");
```

> **注意：** 在 Java 9 之前，用于存储属性的文件必须是 ASCII 文件。如果你使用的是旧版 Java，并且需要在属性文件中放入 Unicode 字符，请使用 `\uxxxx` 编码对其进行编码。例如，要指定 `colorName=Grün`，请使用
> 
> ```text
> colorName=Gr\u00FCn
> ```
> 
> 可以使用 native2ascii 工具生成这些编码。

### 7.7.3 资源包类

要提供非字符串资源，请定义扩展 ResourceBundle 类的类。使用标准命名约定为类命名，例如

```text
MyProgramResources.java
MyProgramResources_en.java
MyProgramResources_de_DE.java
```

使用与加载属性文件相同的 getBundle 方法加载该类：

```java
ResourceBundle bundle = ResourceBundle.getBundle("MyProgramResources", locale);
```

> **注意：** 搜索资源包时，如果类中的资源包和属性文件具有相同的基本名称，则优先使用类中的资源包。

每个资源包类都实现一个查找表。需要为每个想要本地化的设置提供键字符串，并使用该键字符串检索设置。例如，

```java
var backgroundColor = (Color) bundle.getObject("backgroundColor");
double[] paperSize = (double[]) bundle.getObject("defaultPaperSize");
```

实现资源包类的最简单方法是扩展 ListResourceBundle 类。ListResourceBundle 允许你将所有资源放入一个对象数组，然后为你执行查找。遵循以下代码大纲：

```java
public class baseName_language_country extends ListResourceBundle
{
   private static final Object[][] contents =
   {
      { key1, value1 },
      { key2, value2 },
      . . .
   };
   public Object[][] getContents() { return contents; }
}
```

例如，

```java
public class ProgramResources_de extends ListResourceBundle
{
   private static final Object[][] contents =
   {
      { "backgroundColor", Color.black },
      { "defaultPaperSize", new double[] { 210, 297 } }
   };
   public Object[][] getContents() { return contents; }
}
public class ProgramResources_en_US extends ListResourceBundle
{
   private static final Object[][] contents =
   {
      { "backgroundColor", Color.blue },
      { "defaultPaperSize", new double[] { 216, 279 } }
   };
   public Object[][] getContents() { return contents; }
}
```

或者，你的资源包类可以扩展 ResourceBundle 类。然后需要实现两个方法，分别用于枚举所有键和查找给定键的值：

```java
Enumeration<String> getKeys()
Object handleGetObject(String key)
```

ResourceBundle 类的 getObject 方法会调用你提供的 handleGetObject 方法。

- **java.util.ResourceBundle 1.1**
  - `static ResourceBundle getBundle(String baseName, Locale loc)`
  - `static ResourceBundle getBundle(String baseName)`  
    加载具有给定名称的资源包类，用于给定区域设置或默认区域设置，以及其父类。如果资源包类位于某个包中，则基本名称必须包含完整包名，例如 `intl.ProgramResources`。资源包类必须是 public，以便 `getBundle` 方法可以访问它们。
  - `Object getObject(String name)`  
    从资源包或其父资源包中查找对象。
  - `String getString(String name)`  
    从资源包或其父资源包中查找对象，并将其强制转换为字符串。
  - `String[] getStringArray(String name)`  
    从资源包或其父资源包中查找对象，并将其强制转换为字符串数组。
  - `Enumeration<String> getKeys()`  
    返回一个枚举对象，用于枚举此资源包的键。它也会枚举父资源包中的键。
  - `Object handleGetObject(String key)`  
    如果你定义自己的资源查找机制，则应重写此方法，以查找与给定键关联的资源值。

## 7.8 完整示例

在本节中，我们将本章的材料应用于本地化一个退休计算器。该程序计算你为退休储蓄的钱是否足够。你输入自己的年龄、每月储蓄金额等（见图 7.4）。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_444_0.png)

**图 7.4** 英文版退休计算器

文本区域和图表显示退休账户每年的余额。如果在你人生的后期数字变为负数，并且图表中的条形出现在 x 轴下方，你就需要采取一些措施——例如，多存钱、推迟退休、早点去世，或者变得更年轻。

该退休计算器支持三种区域设置（英语、德语和中文）。以下是国际化的一些亮点：

- 标签、按钮和消息被翻译成德语和中文。你可以在 RetireResources_de 和 RetireResources_zh 类中找到它们。英语用作回退——参见 RetireResources 文件。
- 每当区域设置更改时，我们会重置标签并重新格式化文本字段的内容。
- 文本字段按本地格式处理数字、货币金额和百分比。
- 计算字段使用 MessageFormat。格式字符串存储在每个语言的资源包中。
- 为了展示这是可以做到的，我们根据用户选择的语言为条形图使用不同的颜色。

清单 7.5 到 7.8 展示了代码。清单 7.9 到 7.11 是本地化字符串的属性文件。图 7.5 和图 7.6 分别展示了德语和中文的输出。要查看中文字符，请确保已安装中文字体并在 Java 运行时中配置好。否则，中文字符将显示为“缺失字符”图标。

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_445_0.png)

**图 7.5** 德文版退休计算器

![](img/4d2d7969b66c67fcc35ad395fd2f8d6c_445_1.png)

**图 7.6** 中文版退休计算器

```java
private JLabel inflationPercentLabel = new JLabel();
private JLabel investPercentLabel = new JLabel();
private RetireInfo info = new RetireInfo();
private Locale[] locales = { Locale.US, Locale.CHINA, Locale.GERMANY };
private Locale currentLocale;
private JComboBox<Locale> localeCombo = new LocaleCombo(locales);
private ResourceBundle res;
private ResourceBundle resStrings;
private NumberFormat currencyFmt;
private NumberFormat numberFmt;
private NumberFormat percentFmt;

public RetireFrame()
{
   setLayout(new GridBagLayout());
   add(languageLabel, new GBC(0, 0).setAnchor(GBC.EAST));
   add(savingsLabel, new GBC(0, 1).setAnchor(GBC.EAST));
   add(contribLabel, new GBC(2, 1).setAnchor(GBC.EAST));
   add(incomeLabel, new GBC(4, 1).setAnchor(GBC.EAST));
   add(currentAgeLabel, new GBC(0, 2).setAnchor(GBC.EAST));
   add(retireAgeLabel, new GBC(2, 2).setAnchor(GBC.EAST));
   add(deathAgeLabel, new GBC(4, 2).setAnchor(GBC.EAST));
   add(inflationPercentLabel, new GBC(0, 3).setAnchor(GBC.EAST));
   add(investPercentLabel, new GBC(2, 3).setAnchor(GBC.EAST));
   add(localeCombo, new GBC(1, 0, 3, 1));
   add(savingsField, new GBC(1, 1).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(contribField, new GBC(3, 1).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(incomeField, new GBC(5, 1).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(currentAgeField, new GBC(1, 2).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(retireAgeField, new GBC(3, 2).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(deathAgeField, new GBC(5, 2).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(inflationPercentField, new GBC(1, 3).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(investPercentField, new GBC(3, 3).setWeight(100, 0).setFill(GBC.HORIZONTAL));
   add(retireCanvas, new GBC(0, 4, 4, 1).setFill(GBC.BOTH));
   add(new JScrollPane(retireText),
         new GBC(4, 2, 1).setWeight(100, 0).setFill(GBC.BOTH));

   computeButton.setName("computeButton");
   computeButton.addActionListener(event ->
   {
      getInfo();
      updateData();
      updateGraph();
   });
   add(computeButton, new GBC(5, 3));

   retireText.setEditable(false);
   retireText.setFont(new Font("Monospaced", Font.PLAIN, 10));
}
```
