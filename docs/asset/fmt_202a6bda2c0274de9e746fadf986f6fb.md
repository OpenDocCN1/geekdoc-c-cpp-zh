
```java
LISTING 8.11
********************************************************************
// VariableParameters.java      Author: Lewis/Loftus
// 演示变变长度参数列表的使用。
********************************************************************
public class VariableParameters {
  //--
  // 使用构造函数创建两个 Family 对象，该构造函数
  // 接受任意数量的 String 对象作为参数。
  //----------------------------------------------------------------------
  public static void main(String[] args) {
    Family lewis = new Family("John", "Sharon", "Justin", "Kayla",
    "Nathan", "Samantha");
    Family camden = new Family("Stephen", "Annie", "Matt", "Mary",
    "Simon", "Lucy", "Ruthie", "Sam", "David");

    System.out.println(lewis);
    System.out.println();
    System.out.println(camden);
  }
}
```

John

Sharon

Justin

Kayla

Nathan

Samantha

Stephen

Annie

Matt

Mary

Simon

Lucy

Ruthie

Sam

David

## 8.5 变变长度参数列表

```java
LISTING 8.12
// *****************************************************************
// Family.java Author: Lewis/Loftus
// 演示变变长度参数列表的使用。
// *****************************************************************
public class Family {
    private String[] members;

    // 构造函数：通过存储作为参数传递的
    // （可能的、多个）名称来设置此家庭。
    public Family (String ... names) {
        members = names;
    }

    // 返回此家庭的字符串表示。
    public String toString() {
        String result = "";
        for (String name : members) 
            result += name + "\n";
        return result;
    }
}
```

列表 8.12 显示了 `Family` 类。构造函数只是存储对数组参数的引用，直到需要它为止。通过对构造函数使用变长参数，我们可以轻松地创建任何规模的家庭。

- 自测习题（答案见附录 N）

- **SR 8.20** Java 方法如何能够具有变长度的参数列表？

- **SR 8.21** 编写一个方法，接受多个数量的整数参数（每个参数代表旅程中一段的距离），并返回旅行的总距离。

8.22 编写一个 `travelTime` 方法，它接受一个整数参数 `average`（平均速度），随后是多个数量的整数参数（每个参数代表旅程中一段的距离），并返回旅行的总时间。

## 8.6 二维数组

我们到目前为止检查的数组都是一维数组，从意义上说，它们代表简单的值列表。正如名称，二维数组在两个维度上有值，这些维度通常被认为是表格的行和列。图 8.4 图形比较了一维数组和二维数组。我们必须使用两个索引来引用二维数组中的值，指定行和列。

方括号 `[]` 用于表示数组的每个维度。因此，存储整数的二维数组类型是 `int[][]`。从技术上讲，Java 将二维数组表示为数组的数组。二维整数数组实际上是一个指向一维整数数组的一维引用数组。

列表 8.13 所示的 `TwoDArray` 程序实例化了一个二维整数数组。和一维数组一样，维度的大小在创建数组时指定。维度的大小可以是不同的。

`TwoDArray` 程序中使用嵌套的 `for` 循环为数组加载值，并以表格格式打印这些值。仔细跟踪处理过程，查看嵌套循环如何访问二维数组中的每个元素。注意外层循环由 `table.length` 控制，内层循环由 `table[row].length` 控制。

```java
LISTING 8.13
********************************************************************
// TwoArray.java Author: Lewis/Loftus
// 演示二维数组的使用。
********************************************************************
public class TwoArray {
    //
    // 创建一个整数二维数组，填充值，
    // 然后打印出来。
    public static void main(String[] args) {
        int[][] table = new int[5][10];

        // 加载表格
        for (int row=0; row < table.length; row++) {
            for (int col=0; col < table[row].length; col++) {
                table[row][col] = row * 10 + col;
            }
        }

        // 打印表格
        for (int row=0; row < table.length; row++) {
            for (int col=0; col < table[row].length; col++) {
                System.out.print(table[row][col] + "\t");
            }
            System.out.println();
        }
    }
}
```

输出

| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |

|---|---|---|---|---|---|---|---|---|---|

| 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |

| 20 | 21 | 22 | 23 | 24 | 25 | 26 | 27 | 28 | 29 |

| 30 | 31 | 32 | 33 | 34 | 35 | 36 | 37 | 38 | 39 |

| 40 | 41 | 42 | 43 | 44 | 45 | 46 | 47 | 48 | 49 |

和一维数组一样，初始化列表可以用于实例化二维数组，其中每个元素都是一个初始化列表。这种技术用于 `SodaSurvey` 程序，如列表 8.14 所示。

## LISTING 8.14

```java
****************************************************
// SodaSurvey.java               Author: Lewis/Loftus
// 演示二维数组的使用。
********************************************************************

import java.text.DecimalFormat;

public class SodaSurvey
{
    // 确定并打印每行（汽水）和每列（人）
    // 的调查得分。
    //
    public static void main(String[] args)
    {
        int[][] scores = { {3, 4, 5, 2, 1, 4, 3, 2, 4, 4},
                         {2, 4, 3, 4, 5, 3, 2, 1, 2},
                         {3, 5, 4, 5, 3, 2, 5, 5},
                         {1, 1, 3, 1, 2, 1, 3, 2, 4} };

        final int SODAS = scores.length;
        final int PEOPLE = scores[0].length;

        int[] sodaSum = new int[SODAS];
        int[] personSum = new int[PEOPLE];

        for (int soda=0; soda < SODAS; soda++)
            for (int person=0; person < PEOPLE; person++)
            {
                sodaSum[soda] += scores[soda][person];
                personSum[person] += scores[soda][person];
            }

        DecimalFormat fmt = new DecimalFormat("0.#");
        System.out.println("Averages:\n");
    }
}
```

## 8.6 二维数组

# 列表 8.14 续

```java
for (int soda=0; soda < SODAS; soda++)
    System.out.println('Soda #' + (soda+1) + ":" +
    fmt.format((float)sodaSum[soda]/PEOPLE));

System.out.println();
for (int person=0; person < PEOPLE; person++)
    System.out.println("Person #" + (person+1) + ":" +
    fmt.format((float)personSum[person]/SODAS));
```

### 输出

平均值：

Soda #1: 3.2

Soda #2: 2.6

Soda #3: 4.2

Soda #4: 1.9

Person #1: 2.2

Person #2: 3.5

Person #3: 3.2

Person #4: 3.5

Person #5: 2.5

Person #6: 3

Person #7: 2

Person #8: 2.8

Person #9: 3.2

Person #10: 3.8

假设一家汽水饮料制造商对四种新口味进行了口味测试，以查看人们的喜爱程度。制造商让 10 个人尝试每种新口味，并给出 1 到 5 分的，其中 1 分表示糟糕，5 分表示优秀。名为 `SodaSurvey` 的二维数组存储了调查结果。每行对应一种汽水，该行中的每一列对应品尝过该饮料的人。更通地说，每行包含所有测试者对一种特定口味的评分，而每列包含一个人对所有汽水的评分。

`SodaSurvey` 程序计算并打印每种汽水和每位受访者的平均评分。每种汽水和人的总和首先存储在一维整数数组中。然后计算并打印平均值。

## 多维数组

数组可以有一、二、三甚至更多个维度。任何超过一维的数组被称为多维数组。

将二维数组想象成表格是非常容易的。三维数组可以画成立方体。然而，一旦超过三维，多维数组可能看起来难以可视化。考虑随后的每一个维度仅仅是前一个维度的细分。对于较大的多维数组，通常这种方式来思考是最好的。

例如，假设我们想存储全美各大学的学生人数，并以有意义的方式进行分类。我们可以将其表示为四维的整数数组。第一维度代表州。第二维度代表每个州内的大学。第三维度代表每个大学内的学院。第四维度代表每个学院内的系部。每个位置存储的值是特定系部的人数。图 8.5 显示了这些细分情况。

二维数组相当常见。但在程序中决定创建多维数组时，应该小心。在处理在多个级别管理的大量数据时，可能需要额外的信息以及管理这些信息的方法。例如，在之前的示例中，更有可能是每个州都由一个对象来表示，该对象可能包含一个用于存储每所大学信息的数组等。

**核心概念**

在面向对象的系统中，使用超过两个维度的数组是稀少的。

Java 数组还有另一个重要的特征需要考虑。正如我们之前所确定的，Java 不直接支持多维数组。

![](img/7f8e069c1898b741edc17dfeed34b0c1_439_0.png)

图 8.5 四维数组的可视化

相反，它们被表示为指向数组对象的引用的数组。这些数组本身可以包含指向其他数组的引用。数组可以根据需要无限增加维度。由于这种表示每个维度的技术，任何维度的数组长度可以是不同的。这些数组有时被称为“不规则数组”（ragged arrays）。例如，二维数组每行的元素数量可能不相同。在这种情况下，必须小心确保数组得到妥当的管理。

## 自我复习题（答案见附录 N）

- SR 8.23 多维数组在 Java 中是如何实现的？

- SR 8.24 有一个名为 `scored` 的二维数组，存储了一个班级学生的测试成绩。编写代码打印出一个代表数组中分数范围的值。它打印的是最高分值减去最低分值的值。每个测试成绩都表示为一个整数。

![](img/7f8e069c1898b741edc17dfeed34b0c1_440_0.png)

## 8.7 多边形和折线

数组在绘制复杂形状时很有帮助。例如，多边形是一个多边形，在 Java 中使用一系列指示多边形顶点的 (x, y) 点来定义。数组通常用于存储坐标列表。

多边形使用 `Graphics` 类绘制，类似于我们绘制矩形和椭圆。与这些形状一样，多边形可以填充或不填充绘制。绘制多边形的方法是 `drawPolygon` 和 `fillPolygon`。这两个方法都重载了。一个版本使用整数数组来定义多边形，另一个使用 `Polygon` 对象。在使用数组的版本中，第一个参数是 x 坐标，第二个是 y 坐标，第三是点数。

**核心概念**

多边形总是闭合的。

与多边形类似，折线的不同在于第一点和最后一点不会自动连接。折线是不填充的。与多边形类似，折线包含一系列由线段连接的点。`drawPolyline` 的前两个参数是 x 坐标，第二个是 y 坐标，第三是点数。

列表 8.15 所示程序使用多边形绘制了一枚火箭。列表 8.16 所示的 `RocketPanel` 类中，数组 `xRocket` 和 `yRocket` 定义了构成火箭主体的多边形点。`xwindow` 和 `ywindow` 指定了火箭窗口的点。

# 列表 8.16 续

```java
private int[] xFlame = {70, 70, 75, 80, 90, 100, 110, 115, 120, 130, 130};
private int[] yFlame = {155, 170, 165, 190, 170, 175, 160, 185, 160, 175, 155};
//
// 构造函数：设置此面板的基本特征。
//
public RocketPanel() {
{
    setBackground(Color.black);
    setPreferredSize(new Dimension(200, 200));
}

//
// 使用多边形和折线绘制火箭。
//
public void paintComponent(Graphics page) {
{
    super.paintComponent(page);
    page.setColor(Color.cyan);
    page.fillPolygon(xRocket, yRocket, xRocket.length);

    page.setColor(Color.gray);
    page.fillPolygon(xWindow, yWindow, xWindow.length);

    page.setColor(Color.red);
    page.drawPolyline(xFlame, yFlame, xFlame.length);
}
```

`xFlame` 和 `yFlame` 数组定义了折线的点，这些点用于创建从火箭尾部喷出的火焰图像。由于它是作为折线而非多边形绘制的，因此火焰不是封闭或填充的。

# 多边形类 (Polygon Class)

多边形也可以使用 `Polygon` 类对象来定义，该类定义在 Java 标准类库的 `java.awt` 包中。两个版本的重载 `drawPolygon` 和 `fillPolygon` 方法接受单个 `Polygon` 对象作为参数。

# 8.7 多边形与折线
