

## 4.2 控制记录的加载时机

# 4-33

### 执行情况：第一次尝试

```sas
data salesQL;
infile "&path\sales.dat";
input SaleID $4. @6 Location $3;
if Location='USA' then
    input @10 Date mmddy10.
    @20 Amount 7;
else if Location='EUR' then
    input @10 Date date9.
    @20 Amount commax7.
run;
```

SAS 日志中写入无效数据消息

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
30|34   EUR   30|JAN2011   1|876,6|30

PDV
| SaleID | Location | | | Amount |
| :--- | :--- | :--- | :--- | :--- |
| $4 | $3 | N8 | N8 |
| 101 | USA | | | |

### 执行情况：第一次尝试

```sas
data salesQL;
infile "&path\sales.dat";
input SaleID $4. @6 Location $3;
if Location='USA' then
    input @10 Date mmddy10.
    @20 Amount 7;
else if Location='EUR' then
    input @10 Date date9.
    @20 Amount commax7.
run;
```

隐式 OUTPUT：
隐式 RETURN；

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
30|34   EUR   30|JAN2011   1|876,6|30

PDV
| SaleID | Location | | | Amount |
| :--- | :--- | :--- | :--- | :--- |
| $4 | $3 | N8 | N8 |
| 101 | USA | | | |

### 执行情况：第一次尝试

```sas
data salesQL;
infile "&path\sales.dat";
input SaleID $4 @6 Location $3; if Location='USA' then
input @10 SaleDate mmddyy10.
@20 Amount 7.; then
else if Location='EUR' then
input @10 SaleDate date9.
@20 Amount commax7;
```

```
持续到 EOF
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0
30 3 0 4 E U R 3 0 J A N 2 0 1 1 1 8 7 6, 30 0
```

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | N8 | N8 |

### 第一次尝试：意外输出

部分 SAS 日志

```sas
NOTE: Invalid data for SaleDate in line 2 10-19.
NOTE: Invalid data for Amount in line 2 20-26.
RULE: ------+1---------+2-------+3---------+4-------+5----
3034 EUR 30JAN2011 1876,30
SaleID=101 Location=USA SaleDate, Amount= _ERROR=1 _N=1
```

NOTE: 从 infile 'sales.dat' 中读取了 6 条记录。
最小记录长度为 26。
最大记录长度为 27。
NOTE: 数据集 WORK.SAL1 有 3 个观测值和 4 个变量。

### 第一次尝试：意外输出

```sas
proc print data=salesQ1 noobs;
run;
```

| Sale ID | Location | Date | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | 18663 | 2908.74 |
| 101 | USA | | 27891.00 |
| 1345 | EUR | | |

为了为了获得正确的结果，SAS 需要某种方法来防止第二个 INPUT 语句移动到原始数据的下一行。

### 混合记录类型：正确的程序

末尾的单个 @ 会在输入缓冲区中保留一条原始数据记录，直到 SAS 执行以下操作之一：

- 执行一个不带末尾 @ 的 INPUT 语句
- 开始 DATA step 的下一次迭代

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @;
if Location='USA' then
 input @10 Date mmmddy10.
 @20 Amount 7.;
else if Location='EUR' then
 input @10 Date date9.
 @20 Amount commax7.;
run;
```

通常情况下，DATA step 中的每个 INPUT 语句都会将一条新数据记录读取到输入缓冲区。当你使用末尾 @ 时，会发生以下情况：

- 指针位置不改变。
- 没有新记录被读取到输入缓冲区。
- DATA step 同次迭代的下一个 INPUT 语句将继续读取同一记录，而不是新记录。

### 执行情况：正确的程序

```sas
data salesQL;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
 Location='USA' then
    input @10 SaleDate mmddyy10
    @20 Amount $7;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| $4 | $3 | N | | N |

### 执行情况：正确的程序

```sas
data salesQL;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10
    @20 Amount $7;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入

1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3.
if Location='USA' then
    input @100DateDateddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 Date date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV | SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV | SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV | SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV | SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV | SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV | SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

> 未读取 INPUT 语句

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV | SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

2.50

| SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

| 101 | USA | | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

输入缓冲区
1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6
3 0 1 | U S A | 1 2 - 0 | 2 0 1 | 3 2 9 5 0

PDV | SaleID | Location | SaleDate | Amount |
| :--- | :--- | :--- | :--- |
| 101 | USA | | | | | | |

### 执行情况：正确的程序

```sas
data salesQ1;
infile "&path\sales.dat";
input SaleID $4. @ Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount $7.;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
run;
```

### 4.05 短答调查

这个子集 IF 语句的最佳位置在哪里？

```sas
data EuropeQ1;
infile "path\sales.dat";
input SaleID $4. @6 Location $3. @
if Location='USA' then
    input @10 SaleDate mmddyy10.
    @20 Amount 7;
else if Location='EUR' then
    input @10 SaleDate date9.
    @20 Amount commax7;
if Location = 'EUR';
run;
```

