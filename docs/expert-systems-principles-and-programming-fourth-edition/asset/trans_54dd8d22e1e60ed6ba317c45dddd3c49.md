

9.16 修改第 493 页问题 8.33 所开发的程序，使单独的模块用于打印具有指定光谱类的所有恒星、具有指定星等的所有恒星，以及同时匹配光谱类和星等的所有恒星及其距离地球的光年信息。

9.17 修改第 490 页问题 8.15 所开发的程序，以包含第 439 页问题 7.13 的宝石表中找到的其余宝石。对于硬度或密度只有一个数值的宝石，修改规则，使得与指定值相差在 0.01 以内的任何值均可接受。包括规则，以验证并在硬度不在 1 到 10 之间（包含 1 和 10）且密度不在 1 到 6 之间（包含 1 和 6）时重新提示用户。

9.18 下表列出了高中提供的可用课程、讲师姓名以及课程可用的班次。给定一个表示要安排的课程的事实，以及表示首选和非首选讲师和班次的偏好，编写一个程序，建议上课的合适讲师和班次。要确定“最佳”讲师和班次，请对每个可能的候选者按以下方式打分：初始分为零；首选讲师或班次每个加一分；非首选讲师或班次每个减一分；对讲师或班次无偏好则分数不变；分数最高的讲师和班次为“最佳”。

| Course | Instructor | Periods Offered |
| :--- | :--- | :--- |
| 代数 | Jones | 1, 2, 3 |
| 代数 | Smith | 3, 4, 5, 6 |
| 美国历史 | Vale | 5 |
| 美国历史 | Hill | 1, 2 |
| 艺术 | Jenkins | 1, 3, 5 |
| 生物学 | Dolby | 1, 2, 5 |
| 化学 | Dolby | 3, 6 |
| 化学 | Vinson | 6 |
| 法语 | Blake | 2, 4 |
| 地质学 | Vinson | 1 |
| 几何 | Jones | 5, 6 |
| 几何 | Smith | 1 |
| 德语 | Blake | 5 |
| 文学 | Henning | 2, 3, 4, 5, 6 |
| 文学 | Davis | 1, 2, 3, 4, 5 |
| 音乐 | Jenkins | 2, 4 |
| 体育 | Mack | 1, 2, 3, 4, 5 |
| 体育 | King | 1, 2, 3, 4, 6 |
| 体育 | Simpson | 2, 3, 4, 5, 6 |
| 物理 | Vinson | 2, 3, 5 |
| 西班牙语 | Blake | 1, 3 |
| 德克萨斯历史 | Vale | 2, 3, 4 |
| 德克萨斯历史 | Hill | 5, 6 |
| 世界历史 | Vale | 2, 3, 4 |
| 世界历史 | Hill | 4 |

9.19 修改第 489 页问题 8.14 所开发的程序，以打印配置的总价格。如果选定的小装置数量超过可用机架位数量，或者小装置所需功率超过机箱提供的功率，应打印警告消息。

9.20 列出为以下模式的槽生成的模式节点规范：

(a) (blip (altitude 100))
(b) (blip (altitude ?x&:(> ?x 100)))
(c) (stop-light (color -red))
(d) (balloon (color blue|white))

9.21 为以下模式组绘制模式网络：

(data (x red) (y ?y) (z ?y))
(data (x -red))
(item (b ?y) (c ?x&:(> ?x ?y)))
(item (a red) (b blue|yellow))

9.22 为以下规则绘制模式网络和连接网络。列出每个节点处计算的表达式。

```
(defrule rule1
    (phase name testing)
    (data (x ?y) (y ?y))
    (data (x ?y) (y ?x&:(> ?x ?y)))
    =>)
```

```
(defrule rule2
    (phase name testing)
    (data (x ?y) (y ?y))
    (data (x ?y&-red) (y ?x&-green))
    =>)
```

9.23 重写以下规则以使其更高效：

```
(defrule bad-rule
    (items (x ?x1) (y ?y1) (z ?z1))
    (items (x ?x2) (y ?y2) (z ?z2))
    (items (x ?x3) (y ?y3) (z ?z3))
    (test (and (or (eq ?x3 green)
        (eq ?x2 ?x3)
        (> ?y1 ?x1)
        (< ?z1 ?x1)
        (neq ?z3 ?x1)))
    =>)
```

9.24 下图显示了假设设备的故障网络。箭头指示故障传播的方向。例如，如果组件 A 有故障，则组件 B 和 C 也会有故障。

![](img/2c460d4de56b7ffaad3834eee20beaa0_579_0.png)

以下规则将在整个网络中传播故障：

```
(defrule propagate-device-A-fault
    (fault device-A)
    =>
    (assert (fault device-B))
    (assert (fault device-C)))
```

```
(defrule propagate-device-C-fault
    (fault device-C)
    =>
    (assert (fault device-D))
    (assert (fault device-E)))
```

```
(defrule propagate-device-E-fault
    (fault device-E)
    =>
    (assert (fault device-F)))
```

将这三条规则重写为一条通用规则和一个 defacts 构造，以像这三条规则一样传播故障。解释当向故障网络添加新设备时，每种方法必须进行的更改。

## BIBLIOGRAPHY

- (Brownston 85). 李·布朗斯顿等人，《OPS5 专家系统编程：基于规则编程导论》，Addison-Wesley，1985 年。

- (Forgy 85). 查尔斯·L·福吉，《Rete：一种多模式/多对象模式匹配问题的快速算法》，《人工智能》，19，第 17–37 页，1985 年。

- (Forgy 79). 查尔斯·L·福吉，《生产系统的高效实现》，卡内基梅隆大学博士论文，1979 年。

## CHAPTER 10
过程式编程

### 10.1 简介

本章介绍 CLIPS 提供的与 C、Ada 和 Pascal 等语言类似的过程式编程范式。偶尔使用过程式编程范式而非基于规则的编程范式来执行某些操作是有用的（且更高效）。本章首先介绍若干过程式函数，包括允许循环和条件行为的函数。deffunction 构造可用于定义可从规则或其他函数调用的新函数。defglobal 构造允许定义全局变量。与在规则或函数中定义的局部变量不同，这些变量始终保留其值。defgeneric 和 defmethod 构造允许定义泛型函数，泛型函数类似于函数，但执行的特定代码取决于提供给函数的参数的数量和类型。最后，本章介绍若干有用的实用函数。

### 10.2 过程式函数

CLIPS 提供了若干用于控制操作执行流程的函数。*while*、*if*、*switch*、*loop-for-count*、*progn$* 和 *break* 函数提供了与 Ada、Pascal 和 C 等现代高级语言中发现的控制结构类似的功能。此外，*halt* 函数允许由规则的 RHS 停止规则的执行。

CLIPS 旨在成为一种高效的基于规则的语言。这些过程式函数仅旨在审慎使用。在规则的 RHS 上编写冗长的过程式程序违背了使用基于规则语言的整个目的。通常，此类函数应仅用于在规则的 RHS 上执行简单的测试和循环。应避免在规则的 RHS 上对这些函数进行复杂嵌套。

### If 函数

if 函数的语法是：

```
(if <predicate-expression>
 then <expression>+
 [else <expression>+])
```

其中 <predicate-expression> 是单个表达式（例如谓词函数或变量），而 if 和 then 关键字后面的 <expression>+ 是基于对 <predicate-expression> 求值的返回值而求出的一个或多个表达式。请注意，else 子句是可选的。

求值 if 函数时，首先对 <predicate-expression> 表示的条件求值，以确定是执行 then 子句还是 else 子句中的操作。如果条件求值结果为 FALSE 以外的任何符号，则执行函数 then 子句中的操作。如果条件求值结果为符号 FALSE，则执行 else 子句中的操作。如果未包含 else 子句，则在条件为假时不执行任何操作。if 函数执行完毕后，CLIPS 继续执行 RHS 上的下一个操作（如果有）。

if 函数可用于在规则的 RHS 上检查值，而无需让其他规则执行测试。例如，以下规则可用于确定程序是否应继续：

```
(defrule continue-check
 ?phase <- (phase check-continue)
 ==>
 (retract ?phase)
 (printout t "Continue? ")
 (bind ?answer (read))
 (if (or (eq ?answer y) (eq ?answer yes))
 then (assert (phase continue))
 else (assert (phase halt))))
```

请注意，if 函数用于将用户的是或否响应转换为指示要采取的操作类型的事实。在此示例中，操作要么是继续，要么是停止。

if 函数的返回值是函数 then 或 else 部分中求出的最后一个表达式。如果 <predicate-expression> 求值结果为 FALSE 且没有 then 部分，则返回符号 FALSE。

### While 函数

while 函数的语法是：

```
(while <predicate-expression> [do]
 <expression>*)
```

