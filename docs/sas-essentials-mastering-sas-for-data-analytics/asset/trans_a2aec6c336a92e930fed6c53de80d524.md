

[img/6113440fee6085d6edba5f406f541c12_474_0.png)

**图 A.1** SAS 字体示例。（来源：使用 SAS®软件创建，版本 9.4。版权所有 2012，SAS Institute Inc., Cary, NC, USA。保留所有权利。经 SAS Institute Inc., Cary, NC 许可复制。）

在 Windows 中，你也可以指定机器上已安装的任何字体。例如，以下语句使用了 Times New Roman 字体。

```
TITLE F="TIMES" "This is an example use of the TIMES font.";
```

你还可以在此类语句中指定高度和颜色。（默认高度通常为 H=1）。例如：

```
TITLE1 F="COURIER H=2 C=RED "Specify the height of the font.";
```

某些字体还有粗体、斜体和宽字体。更多信息请参阅 SAS 文档。

## A.2 指定 SAS 颜色选择

SAS 过程中可以使用的颜色选择包括：

- 黑色 (Black)
- 蓝色 (Blue)
- 棕色 (Brown)
- 奶油色 (Cream)
- 青色 (Cyan)
- 金色 (Gold)
- 灰色 (Gray)
- 绿色 (Green)
- 淡紫色 (Lilac)
- 石柠绿 (Lime)
- 品红色 (Magenta)
- 深红色 (Maroon)
- 橙色 (Orange)
- 粉色 (Pink)
- 紫色 (Purple)
- 红色 (Red)
- 玫瑰 (Rose)
- 三鱼色 (Salmon)
- 褐色 (Tan)
- 紫罗 (Violet)
- 白色 (White)
- 黄色 (Yellow)

如果你没有明确指定颜色，SAS 的默认颜色为黑色。你可以使用如 LIGHT 等前缀修改这些颜色，例如创建 LIGHTBLUE。其他前缀还包括：

并非所有组合都有效，因此你可能需要尝试以获得你所需的颜色。有数千种其他 SAS 颜色可用。如果你知道颜色的标准 RGB 规范（通常机构会为官方文档指定 RGB 颜色），你可以在颜色选项中使用该规范。例如，CX3230B2 是“亮蓝 (Brilliant Blue)”的 RGB 代码。这里是两个示例（H 为高度选项）：

```
TITLE H=2 C=RED "This produces a Red title."
TITLE2 H=1.5 C=CX3230B2 "This title is Brilliant Blue";
```

## A.3 为 PROC GPLOT 和 PROC UNIVARIATE 指定模式

在 SAS 中指定模式时，你使用直方图的模式代码，通常在 PFILL 语句中，形式如下：

```
PFILL=Mabccc
```

其中 a、b 和 ccc 代码的定义列于表 A.1。这些模式也适用于 PATTERN 语句中的 VALUE= 选项，用于填充各种 SAS/GRAPH 类型的条形或曲线下方区域。

## 表 A.1 自定义模式代码

| 代码 | 含义 |
| --- | --- |
| a | 范围从 1 到 5（线的粗细/密度，1=最细） |
| b | X 表示交叉斜线，N 表示交叉斜线 |
| ccc | c 是范围从 0 到 360 的数字，0 表示无角度，45 表示 45° 角，依此类推。 |
| EMPTY 或 E | 使用 PFILL=EMPTY 指定不填充 |
| SOLID 或 S | 使用 PFILL=SOLID 指定实填充 |

例如，打开程序文件 GPTERN1.SAS。对于某些 SAS 版本，你可能需要包含语句

ODS GRAPHICS OFF;

因为此示例，适用于标准的 SAS 图表，而不是 ODS 图表。该示例代码

```
PROC UNIVARIATE DATA="C:\SASDATA\SOMEDATA" NOPRINT;
VAR AGE;
HISTOGRAM /NORMAL PFILL=M3X45;
RUN;
```

会生成（连同若干表格）一个使用 45° 角交叉斜线模式的直方图，如图 A.2 所示。要控制模式的颜色，请在 PROC 之前包含如下语句：

```
PATTERN COLOR=RED;
```

[img/6113440fee6085d6edba5f406f541c12_476_0.png)

## A.4 状图、饼图和其他图形的条形和区块模式

模式选择可用于 PROC GCHART、PROC GPLOT 和 PROC UNIVARIATE 过程指定颜色和模式，使用 PATTERN 语句：

PATTERNn options;

其中 n（范围从 1 到 30）指定使用模式的图形元素。PATTERN 语句中的以下代码允许你指定颜色和模式：

- E：空填充模式
- R1 到 R5：右倾 45° 条纹（从细到粗）
- X1 到 X5：交叉网格（从细到粗）
- L1 到 L5：左倾 45° 条纹（从细到粗）

例如，打开程序文件 GPTERN2.SAS。对于某些 SAS 版本，你可能需要包含语句

ODS GRAPHICS OFF;

因为此示例适用于标准的 SAS 图表，而不是 ODS 图表。该示例代码（GPTERN2.SAS）

```
GOOPTIONS RESET = ALL;
DATA BARS;
INPUT A B;
DATALINES;
1
2
3
4
5
;
PATTERN1 V=E C=BLUE;
PATTERN2 V=R1 C=BLACK;
PATTERN3 V=X2 C=BLACK;
PATTERN4 V=L3 C=BLACK;
PATTERN5 V=S C=BLACK;
PROC GCHART ;VBAR A
/DISCRETE WIDTH=10
SUBGROUP=B;
RUN;
QUIT;
```

生成如图 A.3 所示的图形，其中展示了各种模式的示例。每个 PATTERN 语句应用于条形，Pattern1 用于第二个，依此类推。

## A.5 SAS 线样式

在 PROC GPLOT 等过程中绘制线条时，你可以从图 A.4 所示的线条样式中选择。这些样式在 SYMBOLn 语句中指定，n 指指定的顺序。

例如，打开程序文件 GLINE.SAS。对于某些 SAS 版本，你可能需要包含语句

ODS GRAPHICS OFF;

因为此示例适用于标准的 SAS 图表，而不是 ODS 图表。该示例代码

```
GOOPTIONS RESET = ALL;
SYMBOL1 COLOR=RED;
```

[img/6113440fee6085d6edba5f406f541c12_478_0.png)

图 A.3 填充模式示例

[img/6113440fee6085d6edba5f406f541c12_479_0.png)

[img/6113440fee6085d6edba5f406f541c12_479_0.png)

