
label="Volume (Millions of Shares)";

rowaxis / griddisplay=on display=(tickvalues)

label="Adjusted Close)";

```

问题是额外的轴标签可能放不下；取决于文本大小和图表大小，文本可能会被截断。选项 `SHORTLABEL` 可以处理截断，但我们需要的是更多文本，且没有换行的方法。

## 使用行标题

对于 245 页图 10.5 中的图表，我们希望解释第一行的轴缩放是以百万股为单位，第二行的价格代表调整后的收盘价。第 246 页“添加侧边栏”中策略是创建外部图例。另一种策略是移除轴的标签并引入 `ROWHEADERS` 块，如下所示：

```
rowaxes;
rowaxis / griddisplay=on display=(tickvalues);
rowaxis / griddisplay=on display=(tickvalues);
endrowaxes;

rowheaders;
layout gridded / columns=1;
entry "Volume" / textattrs=GraphText;
entry "Millions of Shares" / textattrs=GraphText;
endlayout;
layout gridded / columns=1;
entry "Price" / textattrs=GraphText;
entry "(Adjusted Close)" / textattrs=GraphText;
endlayout;
rowheaders;
```

通过在 `GRIDDED` 布局中嵌套 `ENTRY` 语句，我们可以在任何需要的地方获得多行文本。如果没有 `GRIDDED` 布局，每行只能使用一个 `ENTRY` 语句。

![](img/a9ccb6123dee40d424cb295a3a99c16c_257_0.png)

为了给图表留出更多空间，我们可以旋转行标题使其显示为轴标签。注意，`GRIDDED` 布局必须指定 `COLUMNS=2`。

```
rowaxes;
rowaxis / griddisplay=on display=(tickvalues);
rowaxis / griddisplay=on display=(tickvalues);
endrowaxes;

rowheaders;
layout gridded / columns=2;
entry "Price" / textattrs=GraphText rotate=90;
entry "(Adjusted Close)" / textattrs=GraphText rotate=90;
endlayout;
layout gridded / columns=2;
entry "Volume" / textattrs=GraphText rotate=90;
entry "(Millions of Shares)" / textattrs=GraphText rotate=90;
endlayout;
rowheaders;
```

## 微软股票性能

![](img/a9ccb6123dee40d424cb295a3a99c16c_258_0.png)

通过移除冗余的轴信息将其移动到外部列和行位置，实现了图表的整洁外观。在这个例子中，行标题的使用提供了轴标签所需的灵活性。

## 调整行和列的大小

默认情况下，网格的行和列深度宽度相同。你可以使用 `LAYOUT LATTICE` 语句上的 `ROWWEIGHTS=` 和 `COLUMNWEIGHTS=` 指定不同的行深或列宽或两者。考虑以下设置：

```
LAYOUT LATTICE / ROW=2 COLUMNS=2
ROWWEIGHTS=(.6 .4) COLUMNWEIGHTS=(.45 .65)
```

250 页的图 10.6 使用了这些设置。`ROWWEIGHTS=` 指定第一行占据60%的行空间，第二行占据40%。`COLUMNWEIGHTS=` 指定第一列占据45%的列空间，第二列占据65%。这些设置可能会影响分配给单元格标题以及行列标题的空间。

# 图 10.6 具有不同行列的 LAYOUT LATTICE

| 具有不同行列的 LATTICE LAYOUT | |
| --- | --- |
| Column Header | Column Header |
| Header (column 1) | Header (column 2) |
| Sidebar (top) | |
| Column 1 Axis | Column 2 Axis |
| 0 20 40 | 0 20 40 |
| Cell Header (1) | Cell Header (2) |
| Row Header | Row 1 Axis | Row 2 Axis | Row Header |
| 60 40 | 60 40 |
| (row 1) (left) | Plot 1 | Plot 2 | Sidebar (row 1) (right) |
| 20 0 | 20 0 |
| Cell Header (3) | Cell Header (4) |
| 60 | 60 |
| Row Header | Row 2 Axis | Plot 3 | Plot 4 | Row2 Header |
| (row 2) | | (row 2) |
| 0 20 40 | 0 20 40 |
| Column 1 Axis | Column 2 Axis |
| Sidebar (bottom) | |
| Column2 Header | Column2 Header |
| Header (column.1) | Header (column.2) |

在传统的股票图中，分配给价格信息的区域比分配给成交量的区域大。这里是对行进行的调整：

```
layout lattice / columns=2 rows=2 rowweights=(.6 .4)
rowdatarange=union columndatarange=union
rowgutter=3px columngutter=3px;
```

# 定义带有额外功能的网格

## 图 10.7 调整深度的 LATTICE

![](img/a9ccb6123dee40d424cb295a3a99c16c_260_0.png)

下一个示例展示了另一种使用 `ROWWEIGHTS=` `COLUMNWEIGHTS=` 的方法。252 页的图 10.8 显示了一个双行一列的网格，包含二维图和一个一维图。第一行是直方图、密度图、代表每个观测值的边缘图（直方图下方的短垂直线）以及图例的叠加。第二行包含一维箱线图。X 轴具有统一比例，以确保箱线图与直方图对齐。默认情况下，每行分配相同的总高度。然而，由于显示第二行（箱线图）的空间远小于第一行所需的空间，可以使用 `ROWHEIGHTS=` 选项重新划分行空间。例如，在这种情况下可以使用 `ROWWEIGHTS=PREFERRED` 选项来自动将行设置为合适的高度，如下示例所示。

## 图 10.8 使用 ROWWEIGHTS=PREFERRED 的图

![](img/a9ccb6123dee40d424cb295a3a99c16c_261_0.png)

来源于弗雷明汉心脏研究 (SASHELP.HEART)

```sas
proc template;
define statgraph distribution;
begingraph;
entrytitle "Distribution of Cholesterol";
entryfootnote align=left
  "From Framingham Heart Study (SASHELP.HEART)";
layout lattice / rowweights=PREFERRED
columndatarange=union rowgutter=2px;
columnaxes;
columnaxis / display=(ticks values);
endcolumnaxes;
layout overlay / yaxisopts=(offset=.04 griddisplay=auto_on);
discretelegend "Normal" / location=inside
autoalign=(topright topleft) opaque=true;
histogram Cholesterol / scale=percent binaxis=false;
densityplot Cholesterol / normal() name="Normal";
fringeplot Cholesterol / datatransparency=.7;
endlayout;
boxplot yvar=Cholesterol / orient=horizontal boxwidth=.9;
endlayout;
endgraph;
run;
proc sgrender data=sashelp.heart template=distribution;
run;
```

注：关于此模板的通用版本（可以在不重新定义模板的情况下显示任何连续变量的分布），请参阅第 14 章“使用动态变量和宏变量创建灵活模板”，第 327 页。

## 定义带有附加特征的网格

当网格（lattice）包含二维和一维图表的混合时，`PREFERRED` 选项通常用于调整行和列的大小。在本示例中，系统会自动将第二行的高度设置为仅恰好显示箱线图所需的高度。它将第一行的高度设置为可用高度的剩余部分。如果您愿意，也可以使用数字权重来手动设置行。例如，在上一个示例中使用 `ROWWEIGHTS=(.9)` 选项代替 `ROWWEIGHTS=PREFERRED` 选项会产生类似的结果。它将可用高度的 90% 分配给第一行，10% 分配给第二行。

如果一行包含一维和二维图的混合，`PREFERRED` 选项会将行高设置为该行中一维图的最大偏好高度。对于列，它对列宽执行相同的操作。这可能会产生不理想的结果。例如，下面的图显示了一个使用默认行和列尺寸的单行单列网格。它在第一列包含二维图表，在第二列水平方向上包含一维箱线图。

![](img/a9ccb6123dee40d424cb295a3a99c16c_262_0.png)

默认情况下，行高设置为最大可用高度（所示），这可以轻松容纳所有图表。如果将行高设置为 `PREFERRED`，则行高将设置为第二列箱线图的偏好高度，这将导致第一列中的图表被压缩，如下。

## 偏好行高

![](img/a9ccb6123dee40d424cb295a3a99c16c_263_0.png)

`PREFERRED` 选项应用于仅包含一维图表的行和列。对于包含一维和二维图表混合的行或列，请改用数字权重。

关于 `ROWWEIGHTS=PREFERRED` 和 `COLUMNWEIGHTS=PREFERRED` 选项的更多信息，请参阅《SAS Graph Template Language: Reference》中的“LAYOUT LATTICE Statement”。

### 调整图的大小

在定义网格大大时，您通常对图表的良好整体宽高比略有所了解。例如，如果您正在创建一个行三列的网格，图表的默认宽高比为 4:3。它看起来像这样：

### 拟合线比较

![](img/a9ccb6123dee40d424cb295a3a99c16c_263_1.png)

### 调整图的大小

如果图的高度相对于宽度较小，图看起来会更好。您可以通过在 `BEGINGRAPH` 语句中设置 `DESIGNWIDTH=` 和 `DESIGNHEIGHT=` 选项，在模板定义中建立一个良好的默认图表尺寸。经过一些实验，您可能会认为 2:1 的宽高比看起来很好：

```sas
begingraph / designwidth=400px designheight=200px ;
```

### 拟合线比较

![](img/a9ccb6123dee40d424cb295a3a99c16c_264_0.png)

`DESIGNWIDTH=` 和 `DESIGNHEIGHT=` 选项作为模板定义的一部分设置了图的大小，这样当您以后需要更大或更小版本的图时，可以使用 `ODS GRAPHICS` 语句，而不是重置设计尺寸并重新编译模板。您需要在 `ODS GRAPHICS` 语句中指定 `WIDTH=` 或 `HEIGHT=`。另一个维度将根据编译后的模板中通过 `DESIGNWIDTH=` 和 `DESIGNHEIGHT=` 选项指定的宽高比自动为您计算。

```sas
ods graphics / reset width=300px;
proc sgrender data=sashelp.heart template=fitcompare;
```

### 拟合线比较

![](img/a9ccb6123dee40d424cb295a3a99c16c_264_1.png)

如果您在 `ODS GRAPHICS` 语句中同时提供了 `HEIGHT=` 和 `WIDTH=` 选项，它们将完全覆盖设计宽高比。如果未指定 `WIDTH=` 或 `HEIGHT=`，则设计尺寸生效。对于所有包含图表的多单元格布局，强烈建议设置 `DESIGNHEIGHT=` 和 `DESIGNWIDTH=` 选项。

## 第 11 章 使用分类面板

| 分类面板简介 | 257 |
| --- | --- |
| GTL 中的分类面板 | 257 |
| LAYOUT DATAPANEL 语句 | 258 |
| LAYOUT DATALATTICE 语句 | 260 |
| DATAPANEL 和 DATALATTICE 的编码区别 | 262 |
| LAYOUT PROTOTYPE 语句 | 262 |
| 内容组织 | 263 |
| 规划面板时考虑的因素概述 | 263 |
| 网格维度和填充顺序 | 263 |
| 间隙 (Gutters) | 265 |
| 图形宽高比 | 266 |
| 单元尺寸 | 268 |
| 原型方向 | 270 |
| 设置面板特征 | 271 |
| 控制行或列的数据范围 | 271 |
| 设置轴选项 | 273 |
| 控制分类标题 | 275 |
| 使用侧边栏 | 277 |
| 控制分类器的交互 | 280 |
| 最后一个面板的显示 | 280 |
| 用户对面板生成的控制 | 283 |
| 稀疏数据 | 287 |
| 缺失值 | 290 |
| 在分类面板中使用非计算图表 | 291 |
| 每个单元格添加插入图 | 293 |
| 使用 PROC SGPanel 创建分类面板 | 295 |

分类面板是一个具有一个或多个单元格的图，每个单元格显示一个公共图（称为原型）。显示在单元格中的原型结果通过将输入数据划分为由一个或多个分类变量的值定义的子集。GTL 提供了两种可以生成分类面板的布局：

`LAYOUT DATAPANEL`

支持类变量列表。行和列数由语句选项控制。每个单元格的标题都用类变量的值进行标记。

`LAYOUT DATALATTICE`

支持最多两个类变量，一个用于行变量，一个用于列变量。为行变量的每个值创建一个行单元格，为类变量的每个值创建一个列单元格。行和列均有标记。

## LAYOUT DATAPANEL 语句

本节中的示例使用 `LAYOUT DATAPANEL` 语句来指定包含两个分类变量的列表：`DIVISION`（两个不同值）和 `PRODUCT`（三个不同值）。这些唯一值共有六种组合（交叉点），从而生成一个包含六个单元格的面板。

请注意关于 `LAYOUT DATAPANEL` 语句的以下细节：

- `LAYOUT DATAPANEL` 语句上的 `CLASSVARS=` 选项可以指定一个或多个分类器的列表。
- 在生成的图中，数据交叉点通过单元格标题进行识别。

以下模板代码生成第 259 页的图 11.1。

```sas
proc template;
  define statgraph datapanel_intro;
  begingraph;
    entrytitle "Office Furniture Sales";
    layout datapanel classvars=(product division) / columns=2;
    layout prototype;
      seriesplot x=month y=actual;
    endlayout;
  endlayout;
  endgraph;
run;
```

## 分类面板介绍

### 图 11.1 使用 LAYOUT DATAPANEL 创建的分类面板

#### 办公家具销售

| Product = TABLE | Product = TABLE |
| --- | --- |
| Division = EDUCATION | Division = CONSUMER |

![](img/a9ccb6123dee40d424cb295a3a99c16c_268_0.png)

| Product = CHAIR | Product = CHAIR |
| --- | --- |
| Division = EDUCATION | Division = CONSUMER |

![](img/a9ccb6123dee40d424cb295a3a99c16c_268_1.png)

| Product = DESK | Product = DESK |
| --- | --- |
| Division = EDUCATION | Division = CONSUMER |

![](img/a9ccb6123dee40d424cb295a3a99c16c_268_2.png)

在模板中，注意位于 `LAYOUT DATAPANEL` 块内部的 `LAYOUT PROTOTYPE` 块。这个嵌套块是 `DATAPANEL` 布局的必要组成部分，它定义了所有单元格的图形内容。`COLUMNS=2` 设置强制执行了实际的两列布局。生成的实际行数取决于数据中交叉的数量。

对于某些数据，数据交叉的数量可能很大。因此，在渲染分类面板图表时，通常使用 `WHERE` 表达式来限制交叉数量：
