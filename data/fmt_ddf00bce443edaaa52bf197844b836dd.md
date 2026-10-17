
![](img/caa3a36b6e8a0f28e72c4d26c243e580_373_0.png)

图 16.7 集成NextDate 的程序图，部分 3。

## 16.3.1 单元层级环圈复杂度

| 单元 | 环圈复杂度 | 新增决策复杂度 | 总单元复杂度 |
|---|---|---|---|
| Main | 1 | 0 | 1 |
| GetDate | 2 | 0 | 2 |
| IncrementDate | 3 | 0 | 3 |
| PrintDate | 1 | 0 | 1 |
| ValidDate | 6 | 5 | 11 |
| lastDayOfMonth | 4 | 0 | 4 |
| isLeap | 4 | 0 | 4 |
| 复杂度总和 | | | 26 |

## 16.3.2 消息集成层级环圈复杂度

在 16.3 中，从 `GetDate` 到 `Main` 以及 `isLeap` 到 `Main` 添加了边以使图强连通。（因此现在适用 $V(G) = e + p$ 公式。）

$V(G(\text{call graph})) = 9 - 7 + 1 = 3$

消息流量增量 = 1，因此总集成层级复杂度为 4，加上单元层级复杂度（25）得到总复杂度 29。

### 16.4 面向对象的复杂度

`Chidamber/Kemer` (CK) 指标是面向对象软件最好的指标（Chidamber and Kemer,1994）。CK指标的名字几乎一目易懂；某些可以从调用图中推导出；另一些使用了 16.2 节中讨论的单元层级复杂度。

- `WMC`—类加权方法数
- `DIT`—继承树深度
- `NOC`—子类数量
- `CBO`—类间耦合
- `RFC`—类响应
- `LCOM`—方法间内聚性缺失

### 16.4.1 WMC—类加权方法数

`WMC` 指标统计类中方法的数量，并根据其环圈复杂度进行加权。这种加权可以很容易扩展到包含 16.2 节中的决策复杂度概念。与过程代码一样，该指标是实现和测试工作的良好预测指标。

### 16.4.2 DIT–继承树深度

名字已经说明了一切。如果我们制作另一个类图来显示继承，这就是从根节点到叶子节点的路径长度。这可以直接从标准的 UML 类图中推导出。虽然 `DIT` 指标值较大有利于重用，但也增加了测试难度。一种策略是“扁平化”继承类，使得所有方法在一个类中。目前的指南建议 `DIT = 3`。

### 16.4.3 NOC—子类数量

继承图中 `DIT` 指标类的数量简单的每个节点的出度。这与类图的环圈复杂度非常。

### 16.4.4 CBO—类间耦合

该指标是从过程耦合继承到结构化分析设计技术的，当一个单元引用另一个单元时耦合会增加。在过程版本中，识别了几个级别的耦合。这些都可以应用于面向对象的方法。与过程代码一样，更大的耦合意味着更大的测试和维护难度。良好的类设计应该降低 `CBO` 值。

### 16.4.5 RFC—类响应

`RFC` 方法指的是由初始消息产生的消息序列的长度。在第 13 章中，我们说这也是集成测试构造（MM 路径）的“长度”。

### 16.4.6 LCOM—方法间内聚性缺失

`LCOM` 指标是过程代码内聚指标的另一个直接扩展。`LCOM` 是使用类中给定实例变量的方法的数量，并对每个实例变量进行计算。

### 16.5 系统级复杂度

虽然概念上可以考虑系统层级的环圈复杂度

部分系统复杂度源于软件单元之间的交织程度。这通过一个关联用例与类（或方法）的实例矩阵很好地展示，正如我们在第14 章中提到的。行对应用例，列对应类（或方法）。那么行列 j 中的“x”表示类（方法）j 用于支持执行用例 i。注意，对于过程代码，关联或稠密矩阵——稀疏矩阵表明这些

# 软件测试

软件之间是松散交织的，这使得维护和测试相对容易。相反，高耦合度意味着单元之间紧密耦合，因此具有高度的相互依赖性。在高耦合度下，我们可以预期简单的更改会产生更多的涟漪效应，并且在更改后更需要进行严谨的回归测试。顺便提一下，关联矩阵是控制待回归测试项的一种方便方法。

## 练习

- 1. 比较 `NextDate` 过程化实现的圈圈复杂度与其集成版本的总复杂度。然后对第 15 章中的面向对象版本进行同样的比较。
- 2. 考虑一个用于查找给定日期对应星座的日历函数。比较 `zodiac1`、`zodiac2` 和 `zodiac3` 伪代码描述的总复杂度。

`zodiac1` 使用一个 `validEntry` 过程来检查月份、日期和年份的范围。

```java
public zodiac1(month, day, year) {
  if (validEntry(month, day, year)) {
    if (month = 3 AND day >= 21 OR month = 4 AND day < 19) {
    return("Aries");
    } else if (month = 4 OR month = 5 AND day < 20) {
    return("Taurus");
    } else if (month = 5 OR month = 6 AND day < 20) {
    return("Gemini");
    } else if (month = 6 OR month = 7 AND day < 22) {
    return("Cancer");
    } else if (month = 7 OR month = 8 AND day < 22) {
    return("Leo");
    } else if (month = 8 OR month = 9 AND day < 22) {
    return("Virgo");
    } else if (month = 9 OR month = 10 AND day < 22) {
    return("Libra");
    } else if (month = 10 OR month = 11 AND day < 21) {
    return("Scorpio");
    } else if (month = 11 OR month = 12 AND day < 21) {
    return("Sagittarius");
    } else if (month = 12 OR month = 1 AND day < 19) {
    return("Capricorn");
    } else if (month = 1 OR month = 2 AND day < 18) {
    return("Aquarius");
    } else {
    return("Pisces");
    }
  } else {
    return("Invalid Date");
  }
}
```

# 软件复杂度 ■ 347

`zodiac2` 假设月份、日期和年份的值是有效的。星座被假设存储在数组 `zodiac(i)` 中。

```java
public Zodiac2(month, day, year)
  switch(month)
  {
    case 1: {if(day() > 20)
      return zodiac[0];
    else
      return zodiac[3];
    case 2: {if(day() > 19)
      return zodiac[7];
    else
      return zodiac[0];
    case 3: {if(day() > 21)
      return zodiac[1];
    else
    case 4: {if(day() > 20)
      return zodiac[10];
    else
      return zodiac[1];
    case 5: {if(day() > 21)
      return zodiac[4];
    else
      return zodiac[10];
    case 6: {if(day() > 21)
      return zodiac[2];
    else
      return zodiac[4];
    case 7: {if(day() > 23)
      return zodiac[5];
    else
      return zodiac[2];
    case 8: {if(day() > 23)
      return zodiac[5];
    else
      return zodiac[11];
    case 9: {if(day() > 23)
      return zodiac[6];
    else
      return zodiac[6];
    case 10: {if(day() > 22)
      returnreturn[10];
    else
      return zodiac[9];
    case 11: {if(day() > 23)
      return zodiac[5];
    else
      return zodiac[9];
    case 12: {if(day() > 20)
      return zodiac[3];
    else
      return zodiac[8]; }
default:
    return zodiac[12]; }
}
```
