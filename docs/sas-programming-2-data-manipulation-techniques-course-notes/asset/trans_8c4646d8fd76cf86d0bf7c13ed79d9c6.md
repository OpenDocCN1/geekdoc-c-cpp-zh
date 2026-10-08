

## 4.1 使用格式化输入读取原始数据文件

| 语句 | 说明 |
| --- | --- |
| INFILE 'raw-data-file-name': | INFILE 语句指定要通过 INPUT 语句读取的原始数据文件的物理名称。 |

'*raw-data-file-name'* 是操作系统环境用于访问原始数据文件的物理名称。 |

 示例：
| Windows | infile 's:\workshop\offers.dat'; |
| UNIX | infile '/users/userid/offers.dat'; |
| z/OS (OS/390) | infile 'useridid.workshop.rawdata(offers)'; |

PAD 和 LRECL= 选项对于读取通常在 Windows 和 UNIX 环境中常见的变长度记录非常有用。关于 PAD 和 LRECL= 选项的更多信息，请参阅 SAS 帮助文档。

INPUT 规范；INPUT 语句描述了原始数据文件中值的排列，并将输入值分配给相应的 SAS 变量。

![](img/d3bde6e6ab06b1fc622215d982111742_130_0.png)

© 2014, SAS Institute Inc., Cary, North Carolina, USA. ALL RIGHTS RESERVED.

## 4-8 第4章 读取原始数据文件

要将指针向后移动 $n$ 个位置，请使用 $+(-n)$。

SAS 格式符的形式如下：

```
$informatat<w>.<d>
```

其中

$ 表示字符格式符。

informat 是 SAS 格式符或用户定义格式符的名称。

w 指定在输入数据中读取的列数。

. 是必需的分隔符。

![](img/d3bde6e6ab06b1fc622215d982111742_131_0.png)

下表给了一些格式符的简要定义。详细信息可以在 SAS OnlineDoc 中找到。

| 格式符 | 定义 |
|---|---|
| $|n| Sw. | 读取标准字符数据。 |
| w.d | 读取标准数值数据。 |
| COMMAw.d DOLLARw.d | 读取非标准数值数据并移除嵌入的逗号、空格、美元符号、百分比符号和连字符。 |
| COMMAw.d DOLLARw.d | 操作类似于 $COMMA.d$ 和 $DOLLARw.d$，但反转了小数点和逗号的角色。这种惯例在许多欧洲国家很常见。 |
| EUROXw.d | 读取非标准数值数据并移除欧洲货币中嵌入的字符。 |

## 4.1 使用格式化输入读取数据文件

| 格式符 | 定义 |
|---|---|
| PERCENT | 操作类似于 COMMA.d，但如果后面跟着百分比符号（%），则将数字除以 100。 |

如果未指定 *d*，则它默认为 0。这意味着 COMMA. 和 COMMA7.0 是等价的。

如果数据包含小数点，SAS 会忽略 *d* 值并读取输入数据中实际存在的小位数。如果数据不包含小数，*d* 指定了要补全的小位数。

DOLLAR.d 是 COMMA.d 的别名，DOLLARX.d 是 COMMAX.d 的别名。

通过 SAS 帮助文档可以获得更多关于 EUROX.d 的信息。

### SAS 日期格式符示例
显示非标准原始数据值和转换后的 SAS 数值的数据格式符示例：

| 格式符 | 原始数据值 | SAS 日期值 |
|---|---|---|
| MDYY6 | 010160 | 0 |
| MMDDYY8 | 01/01/60 | 0 |
| MMDDYY10 | 01/01/1960 | 0 |
| DDMMYY6 | 311260 | 365 |
| DDMMYY8 | 31/12/60 | 365 |
| DDMMYY10 | 31/12/1960 | 365 |
| DATE7 | 31DEC59 | -1 |
| DATE9 | 31DEC1959 | -1 |

ANYDTDTEW 格式符可用于读取具有多种格式的数据。关于 ANYDTDTEW. 的更多信息请参考 SAS 帮助文档。

## 使用格式化输入读取数据

使用格式化输入从 offers.dat 中的原始数据创建一个名为 discounts 的 SAS 数据集。

| 说明 | 列 | 部分 offers.dat |
| --- | --- | --- |
| 客户类型 | 1-4 | 104012/02/11 Outdoors 15% |
| 优惠日期 | 5-12 | 202010/07/11 Golf 7% |
| 项目组 | 14-21 | 103009/22/11 Shoes 10% |
| 折扣 | 22-24 | 103009/22/11 Clothes 10% |
| | | 202007/08/11 Clothes 15% |
| | | 203007/08/11 Clothes 25% |

## 编写 INPUT 规范

识别每个输入的起始位置、变量名和格式符。

```
input @1 Cust_type 4.
```

| 说明 | 列 | 部分 offers.dat |
| --- | --- | --- |
| 客户类型 | 1-4 | 104012/02/11 Outdoors 15% |
| 优惠日期 | 5-12 | 202010/07/11 Golf 7% |
| 项目组 | 14-21 | 103009/22/11 Shoes 10% |
| 折扣 | 22-24 | 103009/22/11 Clothes 10% |
| | | 202007/08/11 Clothes 15% |
| | | 203007/08/11 Clothes 25% |

## 4.3 答案
继续编写 INPUT 语句以读取日期。（提示：使用 MMDYY8 格式符）。

```
input @1 Cust_type 4. @5 off_date mmdd8.
```

| 说明 | 1-4 | 1-5 | 1-2 | 1-5 |
|---|---|---|---|
| 客户类型 | | 104012/02/11 Outdoors 15% | | |
| 优惠日期 | | 202010/07/11 Golf 7% | | |
| 项目组 | | | 103009/22/11 Shoes 10% | | |
| 折扣 | | | | 103009/22/11 Clothes 10% |

| | | | 202007/08/11 Clothes 15% | |
| | | | | 203007/08/11 Clothes 25% |

## 编译：格式化输入

```
data work.discounts;
infile "&path\offers.dat";
input @1 Cust_type 4.
@5 dtyy8.
@14 Item_gp $8.
@22 percent3.;
```

| 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Cust_type | Order_dt | Item_gp | Discount |
| N 8 | N 8 | $8 | N 8 |

## 执行：格式化输入

```
data work.discounts;
infile "&path\offers.dat";
input @1 Cust type 4.
@5 dt mmdd8.
@14 gp $8.
@22 percent3.
run;
```

| 输入缓冲区 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 |
| Cust_type | Order_dt | Item_gp | Discount |
| N 8 | N 8 | $8 | N 8 |

## 执行：格式化输入

```
data work.discounts;
infile "&path\offers.dat"; Specify input file
input @1 Cust type 4.
@5 dt mmdd8.
@14 gp $8.
@22 percent3.
run;
```

| 输入缓冲区 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5|
| Cust_type | Order_dt | Item_gp | Discount |
| N 8 | N 8 | $8 |

