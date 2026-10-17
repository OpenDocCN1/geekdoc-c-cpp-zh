
## 练习

### Level 1

#### 1. 追加结构相同的数据集

- a. 获取启动程序 `p11oe001`。
- b. 提交两个 `PROC CONTENTS` 步骤以比较两个数据集中的变量。

  `orion.price_current` 中有多少个变量？

  `orion.price_new` 中有多少个变量？

  `orion.price_new` 是否包含 `orion.price_current` 中没有的变量？

- c. 在 `PROC CONTENTS` 步骤之后添加一个 `PROC APPEND` 步骤，将 `orion.price_new` 追加到 `orion.price_current`。不需要 `FORCE` 选项。

  为什么不需要 `FORCE` 选项？

- d. 提交程序并确认 `orion.price_new` 中的 88 条观测值已添加到 `orion.price_current` 中，现在现在应该有 259 条观测值（171 条原始观测值加上 88 条追加的观测值）。

### Level 2

#### 2. 追加结构不同的数据集

- a. 编写并提交两个 `PROC CONTENTS` 步骤以比较 `orion.qtr1_2007` 和 `orion.qtr2_2007` 中的变量。

  `orion.qtr1_2007` 中有多少个变量？

  `orion.qtr2_2007` 中有多少个变量？

  哪个变量不在两个数据集中？

- b. 编写一个 `PROC APPEND` 步骤，将 `orion.qtr1_2007` 追加到名为 `Work.ytd` 的不存在的数据集。
- c. 提交 `PROC APPEND` 步骤并确认 22 条观测值已复制到 `Work.ytd`。
- d. 编写另一个 `PROC APPEND` 步骤，将 `orion.qtr2_2007` 追加到 `Work.ytd`。需要 `FORCE` 选项。

  为什么不需要 `FORCE` 选项？（注：原文此处为"not needed"，可能为原题笔误）

- e. 提交第二个 `PROC APPEND` 步骤并确认 `orion.qtr2_2007` 中的 36 条观测值已添加到 `Work.ytd`，现在现在应该有 58 条观测值。

### Level 3

#### 3. 使用 Append 语句步骤比较变量

- a. 编写并提交三个 `PROC CONTENTS` 步骤来比较 `orion.shoes_eclipse`、`orion.shoes_tracker` 和 `orion.shoes`。
- b. 编写一个带有两个 `APPEND` 语句的 `PROC DATASETS` 步骤，将 `orion.shoes_eclipse` 和 `orion.shoes_tracker` 追加到 `orion.shoes` 中。

> 关于 `DATASETS` 过程的文档可以在 SAS Help and Documentation 的 Contents 选项卡中找到（SAS Products ⇒ Base SAS ⇒ Base SAS 9.2 Procedures Guide ⇒ Procedures ⇒ The `DATASETS` Procedure）

- c. 提交 `PROC DATASETS` 步骤并确认 `orion.shoes` 包含 34 条观测值（10 条原始观测值加上来自 `orion.shoes_eclipse` 和 `orion.shoes_tracker` 的 14 条观测值）。

## 10.3 数据集的合并 (Concatenating)

### 目标

- 使用 DATA 步骤中的 `SET` 语句合并两个或多个 SAS 数据集。
- 使用 `RENAME=` 数据集选项更改变量名称。
- 比较 `APPEND` 过程与 `SET` 语句。（自学）
- 使用 DATA 步骤中的 `SET` 和 `BY` 语句交错合并两个或多个 SAS 数据集。（自学）

## 追加 (Appending) 与 合并 (Concatenating)

追加和合并涉及将 SAS 数据集一个接一个地组合成单个 SAS 数据集。

| SAS 数据集 | |
| :--- | :--- |
| | |
| + |
| SAS 数据集 | |

- 追加（Appending）将第二个数据集中的观测值直接添加到原始数据集的末尾。
- 合并（Concatenating）复制第一个数据集的所有观测值，然后将一个或多个连续数据集的所有观测值复制到一个新集中。

## SET 语句

DATA 步骤中的 `SET` 语句从一个或多个 SAS 数据集中读取观测值。

```
DATA SAS-data-set;
SET SAS-data-set1 SAS-data-set2...;
<additional SAS statements>
RUN;
```

- `SET` 语句中可以包含任意数量的数据集。
- 第一个数据集的观测值首先出现在新集中。第二个数据集的观测值紧随第一个数据集之后，依此类推。

必须了解你的数据。默认情况下，如果 `SET` 语句中所有 SAS 数据集中相同变量的类型不同，则会发生编译错误。

## 结构相同的数据集

合并 `EmpsDK` 和 `EmpsFR` 以创建一个名为 `EmpsAll11` 的新数据集。

| EmpsDK | | | EmpsFR | | | |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| First | Gender | Country | First | Gender | Country |
| Lars | M | Denmark | Pierre | M | France |
| Kari | F | Denmark | Sophie | F | France |
| Jonas | M | Denmark | | | |

数据集包含相同的变量。

```sas
data EmpsAll11;
set EmpsDK EmpsFR;
run;
```

## 编译

| First | Gender | Country |
| :--- | :--- | :--- |
| Lars | M | Denmark |
| Kari | F | Denmark |
| Jonas | M | Denmark |

| First | Gender | Country |
| :--- | :--- | :--- |
| Pierre | M | France |
| Sophie | F | France |

```sas
data EmpsAll11;
set EmpsDK EmpsFR;
run;
```

## 执行

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| EOF | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Pierre | M | 法国 |
| Sophie | F | 法国 |

```sas
data EmpsAll11;
set EmpsDK EmpsFR;
run;
```

## PDV (程序数据变量)

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

![](img/1698e3a97543d6895ff5297aae8fd042_472_0.png)

## 执行

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Pierre | M | 法国 |
| Sophie | F | 法国 |

```sas
data EmpsAll11;
set EmpsDK
run;
initialize PDV
```

![](img/1698e3a97543d6895ff5297aae8fd042_472_1.png)

## PDV

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

## 执行

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Pierre | M | 法国 |
| Sophie | F | 法国 |

```sas
data EmpsAll11;
set EmpsDK EmpsFR;
run;
Implicit OUTPUT:
Implicit RETURN;
```

## PDV

| 名字 | 性别 | 国家 |
|---|---|---|
| Pierre | M | 法国 |
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |
| Pierre | M | 法国 |

## 执行

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Pierre | M | 法国 |
| Sophie | F | 法国 |

```sas
data EmpsAll11;
set EmpsDK EmpsFR;
run;
```

## PDV

| 名字 | 性别 | 国家 |
|---|---|---|
| Sophie | F | 法国 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |
| Pierre | M | 法国 |

![](img/1698e3a97543d6895ff5297aae8fd042_474_0.png)

## 执行

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Pierre | M | 法国 |
| Sophie | F | 法国 |

```sas
data EmpsAll11;
set EmpsDK EmpsFR;
run;
Implicit OUTPUT:
Implicit RETURN;
```

## PDV

| 名字 | 性别 | 国家 |
|---|---|---|
| Sophie | F | 法国 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |
| Pierre | M | 法国 |
| Sophie | F | 法国 |

![](img/1698e3a97543d6895ff5297aae8fd042_474_1.png)

## 执行

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Pierre | M | 法国 |
| Sophie | F | 法国 |

```sas
data EmpsAll11;
set EmpsDK EmpsFR;
run;
```

## 名字 | 性别 | 国家 |
|---|---|---|
| Sophie | F | 法国 |
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |
| Pierre | M | 法国 |
| Sophie | F | 法国 |

## 执行

| 名字 | 性别 | 国家 |
|---|---|---|
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |

| 名字 | 性别 | 国家 |
|---|---|---|
| Pierre | M | 法国 |
| Sophie | F | 法国 |

```sas
data EmpsAll11;
set EmpsDK EmpsFR;
run;
```

## EmpsAll11

| 名字 | 性别 | 国家 |
|---|---|---|
| Sophie | F | 法国 |
| Lars | M | 丹麦 |
| Kari | F | 丹麦 |
| Jonas | M | 丹麦 |
| Pierre | M | 法国 |
| Sophie | F | 法国 |

## 合并数据集

合并 `EmpsCN` 和 `EmpsJP` 创建数据集 `EmpsAll12`。

| 名字 | 性别 | 国家 |
|---|---|---|
| Chang | M | 中国 |
| Li | M | 中国 |
| Ming | F | 中国 |

| 名字 | 性别 | 区域 |
|---|---|---|
| Cho | F | 日本 |
| Tomi | M | 日本 |

数据集之间没有包含相同的变量。

```sas
data EmpsAll12;
set EmpsCN EmpsJP;
run;
```

## 10.05 练习

合并 `EmpsCN` 和 `EmpsJP` 后，`EmpsAll12` 中有多少个变量？

| 名字 | 性别 | 国家 | 名字 | 性别 | 区域 |
|---|---|---|---|---|---|
| Chang | M | 中国 | Cho | F | 日本 |
| Li | M | 中国 | Tomi | M | 日本 |
| Ming | F | 中国 | | | |

```sas
data EmpsAll12;
set EmpsCN EmpsJP;
run;
```

## 10.07 多选题调查（自学）

如果你想在合并时创建一个新变量，你会使用哪种方法？

- a. `APPEND` 过程
- b. `SET` 语句

## 交叉合并（自学）

交叉合并（Interleaving）是指根据一个或多个共同变量，将两个或多个数据集的观测值交错排列。

在 DATA 步中使用带有 `BY` 语句的 `SET` 语句可以交叉合并 SAS 数据集。

```sas
DATA SAS-data-set;
  SET SAS-data-set1 SAS-data-set2;
  BY <DESCENDING> by-variable(s);
  <additional SAS statements>
RUN;
```

> 数据集必须按 `BY` 变量排序。

使用 `SORT` 过程按 `BY` 变量对数据集排序。

通常，对较小的 SAS 数据集进行排序然后进行交叉合并，比合并多个 SAS 数据集后再对生成的较大文件进行排序要高效得多。

## 交叉合并（自学）

| EmpsCN | | | EmpsJP | | | |
|---|---|---|---|---|---|---|
| First | Gender | Country | First | Gender | Region |
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | | | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
run;
```

| First | Gender | Country |
|---|---|---|
| Chang | M | China |

## 交叉合并（自学）

| EmpsCN | | | EmpsJP | | | |
|---|---|---|---|---|---|---|
| First | Gender | Country | First | Gender | Region |
| Chang | M | China | Cho | F | Japan |
| Li | M | China | Tomi | M | Japan |
| Ming | F | | | | | |

哪个值在前面？

```sas
data EmpsAll12;
set EmpsCN EmpsJP(rename=(Region=Country));
run;
```

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
set EmpsCN (rename=(Region=Country));
by First;
run;
```
