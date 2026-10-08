
`NumberFormat moneyFormat = NumberFormat.getCurrencyInstance();`
不要忘记，你还必须在程序中导入 `java.text.NumberFormat`。
b 语句是：
`System.out.println(moneyFormat.format(cost));`
c 如果区域设置是美国，输出将为 $54.89。如果区域设置是英国，输出将为 $54.89。

要将点值作为百分比输出，你首先需要通过调用 `NumberFormat` 类的静态方法 `getPercentInstance` 获取一个 `NumberFormat` 对象。然后，你将值传递给格式化对象的 `format` 方法，该方法会返回一个格式化正确的字符串。例如：

```java
NumberFormat fmt = NumberFormat.getPercentInstance();
System.out.println(fmt.format(value));
```

以下代码将提示用户并读取一个 `double` 类型的值，并打印输入值绝对值的平方根，保留两位小数：

```java
Scanner scan = new Scanner(System.in);
DecimalFormat fmt = new DecimalFormat("0.00");
double value, result;
System.out.print("Enter a double value: ");
value = scan.nextDouble();
result = Math.sqrt(Math.abs(value));
System.out.println(fmt.format(result));
```

## 3.7 枚举类型

以下是电影分级枚举类型的声明：
```java
enum Ratings {G, PG, PG13, R, NC17}
```

在列出的假设下，输出为：
```
clubs
hearts
0
2
```

# 附录 N 自测题答案 749

**SR 3.31** 通过使用枚举类型，你保证了该类型的变量只会取枚举值。

## 3.8 包装类

**SR 3.32** Java 标准类库为每种基本数据类型定义了一个包装类。在需要调用对象的情况下，由包装类创建的对象可能就足够。

**SR 3.33** 对应的包装类是 `Byte`、`Integer`、`Double`、`Character` 和 `Boolean`。

**SR 3.34** 一种方法是使用 `Integer` 的构造函数，如下：
```java
holdNumber = new Integer(number);
```
另一种方法是利用自动装箱（autoboxing），如下：
```java
holdNumber = number;
```

**SR 3.35** 以下语句使用 `Integer` 类的常量 `MAX_VALUE` 输出最大的 int 值：
`System.out.println(Integer.MAX_VALUE);`

## 3.9 组件与容器

**SR 3.36** 窗口（frame）和面板（panel）都是持有 GUI 元素的容器。然而，窗口作为一个带有标题栏的独立窗口显示，而面板不能独立显示。面板通常显示在窗口内部。

**SR 3.37** 最匹配的术语是
- a. container（容器）
- b. frame（窗口）
- c. panel（面板）
- d. heavyweight（重量级级）
- e. lightweight（轻量级）
- f. content pane（内容面板）
- g. label（标签）
- h. layout manager（布局管理器）

**SR 3.38** 如果通过向右拖动右下角来调整面板大小，该语句将从跨两行变为单行。这是因为没有包含特殊的指令来描述容器的布局，导致面板中的组件会根据面板的大小相邻排列。

**SR 3.39** 最准确的描述是：“标签（Labels）”被添加到面板中，然后该面板被添加到窗口的内容面板中。

**SR 3.40** 更改的结果是
- a. 由于新尺寸的原因，面板变得更大且是正方形的。
- b. 语句变得不可见。你只看到一个黑色面板，因为用黑色书写的语句与背景混合在了一起。
- c. 没有变化。
- d. 由于标签添加的顺序相反，该语句是“反向的”——也就是说，读出来是“请先举手”，然后是“提问权威人员”。

## 3.10 嵌套面板

**SR 3.42** 在 `NestedPanels` 程序中，创建了三个面板：`subPanel1`、`subPanel2` 和 `primary`。

**SR 3.43** 在 `NestedPanels` 程序中，`subPanel1` 和 `subPanel2` 被添加到 `primary` 面板中。`primary` 面板被显式添加到窗口的内容中。

## 3.11 图像

**SR 3.44** 在 `LabelDemo` 程序中声明了一个窗口、一个面板、一个图标和三个标签。

**SR 3.45** 在 `LabelDemo` 程序的实例化语句 `label12 = new Label("Devil Right", icon, SwingConstants.CENTER);` 中：第一个参数是文本，第二个参数是图标，第三个参数是对齐方式。

**SR 3.46** 更改的结果是
- a. 由于新尺寸的原因，面板变得更大且是正方形的。
- b. 语句变得不可见。你只看到一个黑色面板，因为用黑色书写的语句与背景混合在了一起。
- c. 没有变化。
- d. 由于标签添加的顺序相反，该语句是“反向的”——也就是说，读出来是“请先举手”，然后是“提问权威人员”。

778
附录 N 自测题答案
