
### Case 4: month is 2: `2月`
If `day` < 28
    Then `tomorrowDay` = `day` + 1
Else
    If `day` = 28
      Then If (`year` is a leap year)
        Then `tomorrowDay` = 29 'not a leap year
        `tomorrowDay` = 1
        `tomorrowMonth` = 3
    EndIf
  Else If `day` = 29
    Then If (`year` is a leap year)
      Then `tomorrowDay` = 1
      `tomorrowMonth` = 3
    Else 'not a leap year
    `tomorrowMonth` = 3
    Output("Cannot have Feb.", `day`)
EndIf
EndIf
EndCase
Output("Tomorrow's date is,", `tomorrowMonth`, `tomorrowDay`, `tomorrowYear`)

## 2.4 佣金问题

我们的第三个例子更符合商业计算场景。它包含了计算和决策的混合，因此引发了有趣的测试问题。我们使用这个例子的主要目的是讨论数据流和基于切片的测试。

### 2.4.1 问题描述

亚利桑那地区的一名步枪销售员出售密苏里州枪匠制造的步枪锁、枪托和枪管。锁的价格为45美元元，枪托为30美元，枪管为25美元。销售员必须

每月至少出售一个锁机、一把枪托和一个枪管（但不一定得是整支步枪），生产限制规定了销售人员每月最多售出 70 个锁机、80 根枪托和 90 根枪管。每次访问城镇后，销售员都会向密苏里州的枪械制造师发送电报，告知已售出的锁机和枪管数量。在月底，销售员会发送一封非常短的电报，显示售出了 -1 个锁机。此时，制造师就知道每月销售已完成，并按如下方式计算销售员的佣金：1000 美元（含）以内的销售额提取 10%，接下来的 800 美元提取 15%，超过 1800 美元的任何销售额提取 20%。

#### 示例 ■ 27

### 2.4.2 讨论

这个例子有些刻意，是为了让读者能快速看到算术过程。考虑其他多个变量的加函数可能更符合现实，例如填写美国 1040 所得税表时的各种计算。（我们稍后会讨论。）这个问题分为三个独立的部分：输入数据程序（在其中我们可以处理输入数据验证，正如三角形和 NextDate 程序中所做的那样）、销售计算以及佣金计算部分。这次我们将省略输入数据部分。我们将使用哨兵控制循环来复制模板惯例，这在 MIS 数据采集应用中是典型的做法。

### 2.4.3 实现

```
Program Commission (INPUT, OUTPUT)

Dim locks, stocks, barrels As Integer

dim lockPrice, stockPrice, barrelPrice As Real

dim totalLocks, totalStocks, totalBarrels As Integer

Dim lockSales, stockSales, barrelSales As Real

Dim sales, commission : REAL
```

```
lockPrice = 45.0

stockPrice = 30.0

barrelPrice = 25.0

totalLocks = 0

totalStocks = 0

totalBarrels = 0
```

```
Input (locks)

While NOT (locks) = -1) '输入设备使用 -1 表示数据结束

Input (stocks, barrels)

totalLocks = totalLocks + locks

totalStocks = totalStocks + stocks

totalBarrels = totalBarrels + barrels
```

```
EndWhile

Output("Locks sold:", totalLocks)

Output("Stocks sold:", totalStocks)

Output("Barrels sold:", totalBarrels)

lockSales = lockPrice * totalLocks

stockSales = stockPrice * totalStocks
```

© 2010 Taylor & Francis Group, LLC

# 软件测试

```
barrelSales = barrelPrice * totalBarrels
sales = lockSales + stockSales + barrelSales
Output("Total sales:"), sales)
```

```
If (sales > 1800.0)

Then

  commission = 0.10 * 1000.0

  commission = commission + 0.15 * 800.0

  commission = commission + 0.20 * (sales-1800.0)

Else If (sales > 1000.0)

Then

  commission = 0.10 * 1000.0

  commission = commission + 0.15*(sales-1000.0)

EndIf

EndIf
```
