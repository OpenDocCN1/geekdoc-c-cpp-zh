
| First | Gender | Country |
|---|---|---|
| Cho | F | Japan |

![](img/1698e3a97543d6895ff5297aae8fd042_484_0.png)

## 交叉合并（自学）

| First | Gender | Country |
|---|---|---|
| Chang | M | China |
| Li | M | China |
| Ming | F | China |

| First | Gender | Region |
|---|---|---|
| Cho | F | Japan |
| Tomi | M | Japan |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Li | M | China |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
```

| First | Gender | Country |
|---|---|---|
| Li | M | China |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
```

| First | Gender | Country |
|---|---|---|
| | | F | China |

## 交叉合并（学学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
```

| First | Gender | Country |
|---|---|---|
| Ming | F | China |

## 交叉合并（自学）

| First | Gender | Country |
|---|---|---|
| Chang | M | China |
| Tomi | M | Japan |
| Ming | F | China |

| First | Gender | Region |
|---|---|---|
| Cho | F | Japan |
| Tomi | M | Japan |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| First | Gender | Country |
|---|---|---|
| Chang | M | China |
| Tomi | M | Japan |
| Ming | F | China |

| First | Gender | Region |
|---|---|---|
| Cho | F | Japan |
| Tomi | M | Japan |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| First | Gender | Country |
|---|---|---|
| Chang | M | China |
| Li | M | China |
| Ming | F | China |

| First | Gender | Region |
|---|---|---|
| Cho | F | Japan |
| Tomi | M | Japan |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| First | Gender | Country |
|---|---|---|
| Chang | M | China |
| Li | M | China |
| Ming | F | China |

| First | Gender | Region |
|---|---|---|
| Cho | F | Japan |
| Tomi | M | Japan |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 交叉合并（自学）

| EmpsCN | | | | EmpsJP | | | |
|---|---|---|---|---|---|---|---|
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | China | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
by First;
run;
```

| First | Gender | Country |
|---|---|---|
| Tomi | M | Japan |

## 练习

## 第一级

## 4. 合并结构相似数据集

a. 编写并提交一个 `DATA` 步将 `orion.mnth7_2007`、`orion.mnth8_2007` 和 `orion.mnth9_2007` 合并为名为 `Work.thirdqtr` 的数据集。

- `Work.thirdqtr` 中来自 `orion.mnth7_2007` 的观测值有多少？
- `Work.thirdqtr` 中来自 `orion.mnth8_2007` 的观测值有多少？
- `Work.thirdqtr` 中来自 `orion.mnth9_2007` 的观测值有多少？

b. 编写并提交一个 `PROC PRINT` 语句来创建报告：

| Obs | Order_ID | Type | Employee_ID | Customer_ID | Order_Date | Delivery_Date |
|---|---|---|---|---|---|---|
| 1 | 124261897 | 2 | 999999 | 90 | 02JUL2007 | 04JUL2007 |
| 2 | 124273731 | 1 | 121107 | 10 | 07JUL2007 | 07JUL2007 |
| 3 | 124273202 | 3 | 999999 | 24 | 11JUL2007 | 14JUL2007 |
| 4 | 124287201 | 3 | 999999 | 27 | 12JUL2007 | 17JUL2007 |
| 5 | 124287683 | 5 | 121105 | 10 | 17JUL2007 | 17JUL2007 |
| 6 | 124283678 | 1 | 121027 | 10 | 18JUL2007 | 18JUL2007 |
| 7 | 124283811 | 1 | 120195 | 41 | 19JUL2007 | 19JUL2007 |
| 8 | 124284855 | 2 | 999999 | 2806 | 19JUL2007 | 23JUL2007 |
| 9 | 124292327 | 3 | 999999 | 70165 | 28JUL2007 | 29JUL2007 |
| 10 | 124293120 | 1 | 120124 | 171 | 30JUL2007 | 30JUL2007 |

## 第二级

## 5. 合并结构不同的数据集

a. 获取启动程序 `p11e05`。
b. 提交两个 `PROC CONTENTS` 语句来比较数据集的变量。这两个数据集中不同的变量名是什么？

```sas
orion.sales      orion.nonsales
```
