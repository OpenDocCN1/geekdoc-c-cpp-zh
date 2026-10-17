
```csharp
int age = 25;
Console.WriteLine(age);
```

你也可以这样更改变量的值：

```csharp
int age = 25;
age = 26;
Console.WriteLine(age);
```

变量还有作用域。作用域定义了程序中可以访问变量的区域。

C# 中三种类型的作用域：局部、类和全局。

- 局部变量：在方法或块内声明。
- 类变量：声明在类内部，但在任何方法之外。
- 全局变量：声明在任何类之外。

以下是局部变量的示例：

```csharp
void MyMethod() {
    int x = 5;
    Console.WriteLine(x);
}
```

以下是类变量的示例：

```csharp
class MyClass {
    int y = 10;
    void MyMethod() {
        Console.WriteLine(y);
    }
}
```

以下是全局变量的示例（注意：C# 没有真正的全局变量，但静态字段有类似的用途）：

```csharp
class MyClass {
    static int z = 20;
}
```

总结来说，变量对于在 C# 中存储和操作数据至关重要。

![](img/f42c8ff43e199c1b82aa844e9d40e211_23_0.png)

# 综合运用

不仅仅是制作一辆汽车，让我们尝试制作一些稍微复杂的东西。我们将添加不同类型和型号的汽车，以及颜色、里程、车身类型、轮子、价格等特征。让我们从目前为止创建的汽车开始：

```python
class Car:
    def __init__(self, make, model, color, mileage, body_type, wheels, price):
        self.make = make
        self.model = model
        self.color = color
        self.mileage = mileage
        self.body_type = body_type
        self.wheels = wheels
        self.price = price
```

这是代码的输出：

```python
car1 = Car('Toyota', 'Corolla', 'white', 20000, 'sedan', 4, 20000)
```

现在，我们将使用 DataFrame 来减少报告中的列数。让我们使用 `COLUMNS` 属性来实现此：

```python
df = df[['make', 'model', 'color', 'mileage', 'price']]
```

这是我们现在的情况：

![](img/f42c8ff43e199c1b82aa844e9d40e211_24_0.png)

查看输出，我们看到汽车并没有那么多，所以我们不需要汽车重量或每百里的成本。与其再添加一列来显示更多信息，不如使用 `COLUMNS` 属性将列重新添加到表格中。

我们将使用 `COLUMNS` 属性添加我们想要看到的列：

```python
df = df.COLUMNS(['weight', 'cost_per_100'])
```

这是现在的输出：

![](img/f42c8ff43e199c1b82aa844e9d40e211_24_1.png)

现在，我们将使用条件格式来高亮这些列。我们还看到可以使用 `PRESTYLE` 属性根据条件高亮单元格。

```python
df.style.apply_map(
    lambda x: 'background-color: red' if x > 20000 else 'background-color: green', 
    subset=['cost_per_100']
)
```

这是现在的输出：

![](img/f42c8ff43e199c1b82aa844e9d40e211_24_2.png)

# PROC TEMPLATE：LIST

`LIST` 语句定义了包含成员的 `TEMPLATE` 的结构或顺序。这允许对成员进行定义、模板化和更新。

`LIST` 语句定义了定义所有成员的 `TEMPLATE` 顺序。

以下是一个使用 `LIST TEMPLATE` 定义 Table `TEMPLATE` 的示例。

```
PROC TEMPLATE mytable;
  LIST row;
    id;
    name;
  END;
END;
```

在此示例中，`LIST` 语句定义了行（`row`），包含了表的所有成员。

`LIST` 语句还可以定义一个指向表中元素的变量列表。

```
PROC TEMPLATE mytable;
  LIST row;
    id;
    name;
  END;
  LIST col;
    name;
    type;
  END;
END;
```

在此示例中，`LIST` 语句定义了列（`col`），包含了表的所有成员。

如何使用 `LIST TEMPLATE` 定义一个 Table `TEMPLATE`。

| ID | Path | Type | Size |
|---|---|---|---|
| 1 | /data/sample/file1 | char | 10 |
| 2 | /data/sample/file2 | char | 20 |
| 3 | /data/sample/file3 | char | 30 |
| 4 | /data/sample/file4 | char | 40 |
| 5 | /data/sample/file5 | char | 50 |
| 6 | /data/sample/file6 | char | 60 |
| 7 | /data/sample/file7 | char | 70 |
| 8 | /data/sample/file8 | char | 80 |
| 9 | /data/sample/file9 | char | 90 |
| 10 | /data/sample/file10 | char | 100 |

这是在示例数据集上使用 `LIST TEMPLATE` 的输出结果。

`LIST` 语句定义了所有内容成员以及每个部分的描述。

如何使用 `LIST TEMPLATE` 定义一个 Table `TEMPLATE`。

`LIST` 语句定义了模板中成员的顺序。

如何在输出中使用 `LIST` 语句。

```
PROC TEMPLATE mytable;
  LIST row;
    id;
    name;
  END;
  LIST col;
    name;
    type;
  END;
END;
```

这是在示例数据集上使用 `LIST` 语句的输出结果。

| ID | Path | Type | Size |
|---|---|---|---|
| 1 | /data/sample/file1 | char | 10 |
| 2 | /data/sample/file2 | char | 20 |
| 3 | /data/sample/file3 | char | 30 |
| 4 | /data/sample/file4 | char | 40 |
| 5 | /data/sample/file5 | char | 50 |
| 6 | /data/sample/file6 | char | 60 |
| 7 | /data/sample/file7 | char | 70 |
| 8 | /data/sample/file8 | char | 80 |
| 9 | /data/sample/file9 | char | 90 |
| 10 | /data/sample/file10 | char | 100 |

`LIST` 语句定义了模板中成员的顺序。

# 录录 A：与旧版本 SAS 的兼容性

## 运行 PROC TEMPLATE 示例

# Styles

### 使用层级样式表 (CSS)

### 样式属性名称的更改

### 同时定义多个元素

### 继承

### CLASS 语句

书中的示例旨在尽可能适用于许多版本的 SAS。某些存储过程和属性在 SAS 9.3 之前不可用，且 SAS 9.2 与之前的版本之间存在差异。可以通过一些变通方法使书中的示例适用于其他版本。这些方法在此处列出。

## 运行 PROC TEMPLATE 示例

虽然书中的示例适用于许多 SAS 版本，但如果你使用的是 SAS 9.3，可以简化大部分示例。我们提到过 SAS 9.3 增加了 `PROC ODTABLE`，它将编译模板和将其绑定到数据集步骤合并为了一个步骤。以下代码段本质上是等：

```
/* 使用 PROC TEMPLATE */
PROC TEMPLATE;
DEFINE TABLE mytable;
COLUMN name age height;
END;
RUN;

%render(mytable, sashepclass);
```

```
/* 使用 PROC ODTABLE */
PROC ODTABLE DATA = sashepclass;
COLUMN name age height;
RUN;
```

上述两种方法的主要区别在于，在 `PROC TEMPLATE` 代码中，表模板将保留在磁盘上，而 `PROC ODTABLE` 创建的临时表定义在表格渲染后就会被丢弃。

`NAME` 选项。以下代码段提供了等效的行为：

```
/* 使用 PROC TEMPLATE */
PROC TEMPLATE;
DEFINE TABLE mytable;
COLUMN name age height;
END;
RUN;
```

```
/* 使用 PROC ODTABLE */
PROC ODTABLE NAME = mytable;
COLUMN name age height;
RUN;
```

# Styles

`PROC TEMPLATE` 元素在 SAS 9.2 中发生了变化。许多更改被类似于以前版本那样的简单代码所取代。SAS 9.2 中对 `PROC TEMPLATE` 属性的更改允许与 CSS 属性名称保持一致，具备了同时创建多个样式元素的能力，并增加了 CSS 样式而非 `PROC TEMPLATE` 属性，尽管为了兼容 9.2 之前的版本，并非所有示例都已完成。

# 使用样式表 (CSS)

直到 SAS 9.2 才引入了 CSS 支持。这是一个全新的功能，因此没有方法可以模拟这种行为。现在你可以使用 SAS Enterprise Guide 样式编辑器创建适用于 ODS 输出类型的样式。

| background | background/color |
| bottommargin | marginbottom |
| bullet | liststyle |
| cellheight | height |
| cellwidth | width |
| font_face | fontFamily |
| font_size | fontsize |
| font_style | style |
| font_weight | fontweight |
| font_width | fontwidth |
| foreground | color |
| htmclass | class |
| htmcontentype | contentype |
| htdctype | doctype |
| indent | textindent |
| just | textalign |
| leftmargin | marginleft |
| fontweight | height |
| outpwidth | width |
| rightmargin | marginright |
| topmargin | margintop |
| valign | verticalalign |

# 附录 A 索引

以下索引列出了书中使用的术语、缩写、图形和表格。术语按字母顺序列出，方便查询。

此索引是书中使用的关键术语列表，为读者提供快速参考。

- 学习算法，12-15, 22, 45, 102
- 反向传播，38-42, 88, 92
- 卷积神经网络，55-60, 110-115
- 梯度下降，25-28, 75, 80
- 集成方法，65-70, 120-125
- 特征提取，18-21, 95-100
- 生成式模型，80-85, 140-145
- 超参数，30-35, 130-135
- 图像处理，150-155, 180-185
- 深度学习，45-50, 160-165
- 核方法，50-55, 170-175
- 损失函数，25-30, 180-185
- 机器学习学习，10-20, 190-200
- 神经网络，40-45, 210-220
- 优化，25-35, 220-230
- 模式识别，5-15, 230-240
- 强化学习，70-80, 250-260
- 回归分析，20-30, 260-270
- 监督学习，15-25, 270-280
- 迁移学习，85-95, 290-300
- 无监督学习，75-85, 310-320
- 计算机视觉，150-160, 330-340
- 波处理处理，190-200, 350-360
- 交叉验证，110-120, 370-380
- 产量优化，60-70, 390-400
- 零样本学习，90-95, 410-420

章节开头标题的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

侧边标题正文的样式。

# HTML 特有样式属性

以下属性主要用于 HTML 输出类型；特殊情况已另行说明。

**`CLASS=string`**

指定用于元素的 CSS 类名，以代替 ODS 预定义的类名。

**`CONTENTTYPE=string`**

指定文档的内容类型。这通常用于 HTML 文件开头的 `<meta>` 标签中，用于告诉浏览器文档的类型。

**`DOCTYPEYPE=string`**

指定在 HTML 文档顶部打印的 `<!DOCTYPE>` 声明。

**`HREFTARGET=string`**

指定 target= HTML 属性中使用的框架名称。

**`HTMLID=string`**

即时查找答案，或掌握新知识。立即订阅。查看定价选项。

**`HTMLSTYLE=string`**

指定要添加到 style= HTML 属性或 CSS 类中的额外 CSS 样式内容。

**`PAGEBREAKHTML=string`**

指定用于分页的标记。这必须在 Body 样式元素中指定。

**`TAGATTR=string`**

指定在 HTML 元素标签内包含的额外标记。这可以向 HTML 标签添加 ODS 直接不支持的属性。该属性也用于 ExcelXP 标签，用以添加 Excel 特有的格式。

# 分组指标属性

### CAPITAL

指定须须末端的标记。接受的值有 SERIF、BRACKET 和 NONE。

### CONTOUR

指定距离箱体的点距离统计量。接受的值有 MEDIAN、MEAN 和 MAX。

### CORRELATION

指定绘图的属性。可以使用逗号分隔多个属性。

### DIRECTION

指定方向。接受的值有水平和垂直。

### LINES

指定线条的颜色。

### MARKERS

指定标记的大小。下方列出了符号：

### HORIZONTAL

指定刻度的颜色。

### NEUTRALCOLOR

指定 y 刻度的颜色。

### STARTCOLOR

指定第一个刻度的颜色。

### TICKELS

指定所有标记的位置。接受的值有 INSIDE、OUTSIDE 或 ACROSS。

### TRANSPAREY

指定区域的透明度。值为 0 将完全透明。

# 附录 C：颜色名称由 SAS/GRAPH 定义

## 引言

### 基础颜色

### 黑色

# 蓝色

# 棕色

# 绿色

### 橄榄色

### 橙色

### 粉色

## 紫色

## 白色

### 黄

## 引言

下表描述了 SAS/GRAPH 定义的颜色 RGB 等效值和视觉样本。这些颜色可以在任何接受颜色的属性中使用。注意：关于此附录的颜色，请参 http://support.sas.com/。

### 基础颜色

| 名称 | 描述 | RGB | 样本 |
|---|---|---|---|
| 黑色 | BLACK | black | #000000 |
| 蓝色 | BLUE | blue | #0000FF |
| 棕色 | BROWN | brown | #A65000 |
| Charcoal | CHARCOAL | charcoal | #4E4E4 |
| 奶油色 | CREAM | cream | #ESDD8 |
| 青色 | CYAN | cyan | #00FFFF |
| 金色 | GOLD | gold | #FFAA00 |
| 灰色 | GRAY | gray | #808080 |
| 绿色 | GREEN | green | #00FF00 |
| 丁香紫 | LILAC | lilac | #E0609 |
| 石灰绿 | LIME | lime | #C0FF1 |
| 品红色 | MAGENTA | magenta | #FF00FF |
| 酒红色 | MAROON | maroon | #700000 |
| 橄榄色 | OLIVE | olive | #2A8307 |
| 橙色 | ORANGE | orange | #FF800 |
| 粉色 | PINK | pink | #FF0080 |
| 紫色 | PURPLE | purple | #70307 |
