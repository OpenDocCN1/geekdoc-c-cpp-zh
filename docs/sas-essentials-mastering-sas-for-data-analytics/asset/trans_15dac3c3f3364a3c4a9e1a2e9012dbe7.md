

# 表 B.6 (续)

| 函数 | 说明 |
| --- | --- |
| INDEX (text, texttofind) | 搜索指定的 texttofind 字符串并返回文本开始的数字，或返回 0 |
| LEFT (text) | 将字符字符串左对齐 |
| LENGTH (text) | 返回文本字符串的长度 |
| LOWCASE (text) | 将所有字符转换为小写 |
| QUOTE (text) | 为文本添加双双引号 |
| REPEAT (text, n) | 将文本重复 n 次。例如，R=repeat("ABC", 3)；结果为 R="ABCABC" |
| REVERSE (argument) | 反转文本表达式 |
| RIGHT (argument) | 将文本右对齐 |
| SCAN (text, n,<delimiters>) | 返回文本表达式中的第 n 个单词。例如，FIRST-SCAN("JOHN SMITH", 1, ''); 返回 JOHN；LAST-SCAN("JOHN SMITH", 2, ' '); 返回 SMITH |
| SOUNDEX (text) | 将文本转换为谐音参数，例如，SOUNDEX("ALLEN")=SOUNDEX("ALAN") 匹配，而 SOUNDEX("ALLEN")=SOUNDEX("MELON") 不匹配 |
| SUBSTR (text, start,<n>) | 搜索并替换文本。例如，VAR=SUBSTR("LINCOLN", 3, 2) 返回 VAR="NC"；SUBSTR("LINCOLN", 3, 2)="XX" 返回 XX |
| TRANSLATE (text, to, from) | 将字符替换为指定的新字符。例如，TRANSLATE('LINCOLN','X','C') 返回 LINCOXN |
| TRWRD (source, target, replacement) | 替换或删除文本字符串中出现的所有单词。例如，TRWRD('SPECIAL WED MEAL', 'WED', 'MON') 返回 'SPECIAL MON MEAL' |
| TRIM (text) | 文本中的空格。（如果表达式缺失则返回空） |
| TRIMN (text) | 删除文本末尾的空格。如果表达式缺失则返回空。 |
| UPCASE (text) | 将文本转换为大写 |
| VERIFY (source, excerpt-1,< ...excerpt-n) | 搜索文本并返回第一个参数中第一个不匹配字符的位置。VERIFY("12345","54301") 返回 2，因为第二个字符不匹配第二个参数中的任何字符 |

# 动手示例

- 1. 打开程序文件 FUNC_CHAR.SAS。此程序演示了如何从一个文本值中分离出两个数值。在这种情况下，收缩压和舒张压被记录为单条文本值 120/80。运行此代码并观察这两个值是如何被提取并转换为两个数值 SBP 和 DBP 的。

```sas
DATA BP;
INPUT BP $10;
I=FIND(BP,"/");
SBP=SUBSTR(BP, 1, I-1); * 获取 / 之前的数字;
DBP=SUBSTR(BP, I+1); * 获取 / 之后的数字;
DROP I;
DATALINES;
120/80
140/90
110/70

PROC PRINT DATA=BP;RUN;
```

- 2. 注意代码 `I=FIND(BP,"/")`。在条记录中，变量 I 被设置为什么值？

- 3. 代码 `SUBSTR(BP, 1, I-1)` 起什么作用？

- 4. 代码 `SUBSTR(BP, I+1)` 起什么作用？

# 动手示例

- 1. 打开程序文件 FUNC_SCAN.SAS。该程序的目标是将一组姓名拆分为名和姓。在这种情况下，我们不关心中间的首字母。运行程序并观察表 B.7 中的结果。

```sas
DATA NAMES;
FORMAT FIRST LAST NAME $20;
INPUT @1 NAME $30;
FIRST=SCAN(NAME, 1, " ");
LAST=SCAN(NAME, -1);
MAYBE=SCAN(NAME, -2);
IF MAYBE=FIRST THEN MAYBE=""
IF LENGTH(MAYBE)=1 THEN MAYBE=""
LASTNAME=CAT(MAYBE, LAST);
FULLNAME=CAT(FIRST, TRIM(LASTNAME));
DATALINES;
Alfred J. Prufrock
Benjamin Harrison
George H. W. Bush
Vincent Van Gogh
A. C. Elliott;;
RUN;
PROC PRINT DATA=NAMES; RUN;
```

- 2. 在数据段中输入你的名字、首字母和姓。运行程序查看它们是否被正确拆分。

- 3. 查看 SCAN 函数的三次用法：

```sas
FIRST=SCAN(NAME, 1, " ");
LAST = SCAN(NAME, -1);
MAYBE=SCAN(NAME,-2);
```

它们各自的作用是什么？负数作为参数代表什么意思？

- 4. `LENGTH` 函数起什么作用？如何用它来判断是否有中间名？

- 5. `CAT` 函数起什么作用？在创建 FULLNAME 时替换它并运行代码会有什么变化？最后，注意 FULLNAME 中使用的 `TRIM` 函数。它用于删除 LASTNAME 中的任何空格。

**表 B.7 SCAN、LENGTH 和 CAT 函数**

| Obs | FIRST | LAST | MAYBE | LASTNAME | FULLNAME |
|---|---|---|---|---|---|
| 1 | Alfred | J. | Pruf | rock | Alfred J. Prufrock |
| 2 | Benjamin | Harrison | | | Benjamin Harrison |
| 3 | George | H. W. | Bush | | George H. W. Bush |
| 4 | Vincent | Van | Gogh | | Vincent Van Gogh
| 5 | A. C. | Elliott | | | A. C. Elliott |

**B.6 截断函数**

截断函数用于提取数字的某些部分，例如最小整数、最大整数、最近整数等，见表 B.8。

**B.7 财务函数**

财务函数允许你对值进行常用计算。SAS 中有 50 多个这样的函数，无法全部描述。常用的几个列在表 B.9 中。

**表 B.8 截断函数**

| Function | 说明 |
|---|---|
| CEIL (x) | 返回大于等于参数的最小整数 |
| FLOOR (x) | 返回小于等于参数的最大整数 |
| FUZZ (x) | 如果值在 x 范围内，返回最近的整数 |
| INT (x) | 返回参数的小数部分 |
| ROUND (x, roundoff) | 将值舍入到最近的单位。例如，ROUND(1.2345, .01) 返回值 1.23 |

**表 B.9 特殊函数**

| Function | 说明 |
| --- | --- |
| IRR (period, cash, ...) (amount, rate, number) | 返回内部收益率。当 PAYMENT 变量缺失时，返回此贷款还款。例如，PAYMENT(30000.,.06/12, monthly) 为 70.55 |
| NPV (rate, period, cash, ...) | 返回现值 |

# 动手示例

- 1. 打开文件 FUNC_MORT.SAS。此程序使用 MORT 函数计算贷款还款。此示例显示了不同贷款金额的还款金额。运行程序并观察表 B.10 中的结果。

```sas
DATA LOAN;
FORMAT VALUE DOLLAR12.;
INTR1-INTR3 4.
NUMBER 4;
INPUT INTR1-INTR3;
ARRAY (3) INTR1-INTR3;
DO I=1 to 3;
PAYMENT(I) = MORT(VALUE,,12);
END;
LABEL MORT="Mortage Payment"
LABEL INTR1="Int. Rate 1"
LABEL INTR2="Int. Rate 2"
LABEL INTR3="Int. Rate 3"
LABEL PAYMENT="Amount of Payment"
LABEL VALUE="Loan Amount"
LABEL NUMBER="Num. Payments";
DATALINES;
100000 .05 .04 .03 360
100000 .05 .04 .03 180
150000 .05 .04 .03 360
150000 .05 .04 .03 180;
RUN;
PROC PRINT DATA=LOAN ;
```

向数据中添加一条 200,000 的贷款，期限为 30 年和 15 年，利率分别为 0.05、0.04 和 0.03。运行程序并观察结果。

**表 B.10 MORT 示例**

| Obs | Loan Amount | Int. Rate 1 | Int. Rate 2 | Int. Rate 3 | Num. Payments | PAY1 | PAY2 | PAY3 |
|---|---|---|---|---|---|---|---|---|
| 1 | $100,000 | 0.05 | 0.04 | 0.03 | 360 | 536.82 | 477.42 | 421.60 |
| 2 | $100,000 | 0.05 | 0.04 | 0.03 | 180 | 790.79 | 739.69 | 690.58 |
| 3 | $150,000 | 0.05 | 0.04 | 0.03 | 360 | 805.23 | 716.12 | 632.41 |
| 4 | $150,000 | 0.05 | 0.04 | 0.03 | 180 | 1186.19 | 1109.53 | 1035.87 |

# **B.8 特殊用途函数**

“特殊用途函数”是一个统称，指在 SAS 中非常有用的函数。它们包括提供变量类型转换的方法、创建宏变量、创建滞值以及使用邮政编码确定距离差异的函数。这些函数列在表 B.11 中。

# 表 B.11 特殊用途函数

| 函数 | 说明 |
|---|---|
| INPUT(string,format) | INPUT 函数将字符转换为数值 |

![](img/6113440fee6085d6edba5f406f541c12_496_0.png)

> 例如，
s="1,212"
x=input(s,comma5);
返回 x=1212（数值）。
注意：INPUT(string1,char-format) 和 PUTN(string1,num-format) 与 INPUT()类似，但你可以在代码中指定格式

PUT 函数将变量从字符或数值转换为字符

![](img/6113440fee6085d6edba5f406f541c12_496_1.png)

