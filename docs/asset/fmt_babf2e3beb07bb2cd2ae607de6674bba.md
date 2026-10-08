
LAWRENCE CALDWELL

1010 LAKE STREET

ANAHEIM CA 94122

RACHEL CHEVONT

3719 OLIVE VIEW ROAD

HARTFORD CT 06183

```
- a.
```

1------+10------+20---

SHIRT LT BLUE SOLID

SKU 128699

$38.99

SHIRT DK BLUE STRIPE

SKU 128799

$41.99

```
- b.
```

1------+10------+20---

MARCUS JONES

SR01 $26,134.00

MARY ROBERTSON

COURTNEY NEILS

TWO1 $28,342.00

```
- c.
```

1------+10------+20---

CROC MIX

10 CASES

DAFFODIL

12 CASES

HYACINTH BLUE

8 BAGS

```
- d.
```

正确答案：c

新的数据文件中每个观测值包含记录数量并不相同，该数据集的输出将显示第四行的 ID 和薪资信息为无效数据。

# 第20 章：从单条记录创建多个观测值

- 1. 关于双尾随符号 (`@@`)，哪项描述是正确的？
   a. 它允许下一个 `INPUT` 语句在 DATA 步的多次迭代中从当前记录读取数据。
   b. 它必须是 `INPUT` 语句中的最后一项。
   c. 当输入指针移过记录末尾时，它会被释放。
   d. 以上皆对

正确答案：d

双尾随符号 (`@@`) 允许下一个 `INPUT` 语句在 DATA 步的多次迭代中从当前记录读取数据。它必须是 `INPUT` 语句中指定的最后一项。被双尾随符号 (`@@`) 保持的记录在输入指针移过记录末尾或或指定了无行持有者的 `INPUT` 语句之前不会释放。

- 2. 被单尾随符号 (`@`) 保持的记录在何时自动释放？
   a. 输入指针移过记录末尾时。
   b. DATA 步的下一次迭代开始时。
   c. 执行另一个带有 `@` 的 `INPUT` 语句时。
   d. 从观测值中读取另一个值时。

正确答案：b

与双尾随符号 (`@@`) 不同，单尾随符号 (`@`) 在控制权返回 DATA 步顶部进行下一次迭代时会自动释放。`@@` 不会开启和关闭。如果执行另一个带有尾随 `@@` 的 `INPUT` 语句，保持效果仍然有效。

- 3. 哪一个 SAS 程序为每个数据块创建一个单独观测值？

```
1----+----+10+----+20+----+30+----+40+----+
1001 apple 1002 banana 1003 cherry
1004 guava 1005 kiwi 1006 papaya
1007 pineapple 1008 raspberry 1009 strawberry
```

- a. `data perm.produce;`
   `infile fruit;`
   `input Item : Variety : $10;`
   `run;`

- b. `data perm.produce;`
   `infile fruit;`
   `input Item $ Variety : $10. @;`
   `run;`

- c. `data perm.produce;`
   `infile fruit;`
   `input Item $ Variety : $10. @@;`
   `run;`

- d. `data perm.produce;`
   `infile fruit @@;`
   `input Item $ Variety : $10;`
   `run;`

正确答案：c
该文件中的每条记录都包含三个 Item 和 Variety 的重复数据值块。`INPUT` 语句读取 Item 和 Variety 的一组值，并使用双尾随符号 (`@@`) 保持当前记录。程序数据中的值被写入数据集，作为第一个观测值。在下一次迭代中，`INPUT` 语句从同一条记录中读取下一组 Item 和 Variety 的值。

- 4. 哪一个 SAS 程序读取 ID 并为每个 Quantity 值保持记录，以便为每个值创建三个观测值？

|---+10----+20-----+----30 |
| 2101 21,208 19,047 22,890 |
| 2102 18,775 20,214 22,654 |
| 2103 19,763 22,927 21,862 |

```
a. data work.sales;
infile unsold;
input ID $;
do week=1 to 3;
input Quantity : comma;
output;
run;
```

```
b. data work.sales;
infile unsold;
input ID $ @@;
do week=1 to 3;
input Quantity : comma;
output;
run;
```

```
c. data work.sales;
infile unsold;
input ID $ @;
do week=1 to 3;
input Quantity : comma;
output;
run;
```

```
d. data work.sales;
infile ID $ @;
input ID $ @;
do week=1 to 3;
input Quantity : comma, @;
output;
run;
```
正确答案：d
此文件包含一个 ID 字段以及重复字段。第一个 `INPUT` 语句读取 ID 并使用 `@` 指定符保持下一个记录记录。第二个 `INPUT` 语句读取 Quantity 值。当读取所有重复字段后，控制权返回 DATA 步顶部，记录被释放。

- 5. 当索引名为 `count` 的值从 1 到 50 步增 5 时，哪个 SAS 语句重复执行？

- a. `do count=1 to 50 by 5;`
- b. `do count=1 to 50 by 5;`
- c. `do while (count=1 to 50 + 5);`
- d. `do while (count=1 to 50 * 5);`

正确答案：a
迭代 `DO` 语句根据变量 `count` 的值从 1 到 50 步增 5。

- 6. 在 DATA 步中使用，以下哪一个选项在每次读取 Activity 值后将观测值写入数据集？

- a. `do choice=1 to 3;`
   `input Activity : $10. @;`
   `output;`
   `run;`
- b. `do choice=1 to 3;`
   `input Activity : $10. @;`
   `output;`
   `run;`
- c. `do choice=1 to 3;`
   `input Activity : $10. @;`
   `output;`
   `run;`
- d. a 和 b

正确答案：a
`OUTPUT` 语句必须放在循环中，这样每次读取 Activity 值时都会立即写入数据集。

- 7. 当 `Cholesterol` 值大于 200 时，哪个 SAS 语句重复执行？

- a. `do cholesterol > 200;`
- b. `do cholesterol gt > 200;`
- c. `do while (cholesterol) > 200;`
- d. `do while cholesterol > 200;`

正确答案：c
`DO WHILE` 语句检查 `Cholesterol` 大于 200 的条件。表达式必须放在括号内。表达式在循环执行前的顶部进行评估。如果条件为真，则执行循环。如果第一次评估为假，循环不执行。

- 8. 以下哪一个选项是 `sum` 语句的示例？
a. `totalpay=1;`
b. `totalpay*1;`
c. `totalpay by 1;`

正确答案：b
`sum` 语句将表达式的结果累加到一个变量。`by` 是 `sum` 语句的重要部分。在这里，`TotalPay` 的值增加了 1。

- 9. 哪一个程序从所示的原始数据文件创建 `Perm.Topstore` 数据集？

```
1----+----------+----+20-------------+
1001 77163.19 76804.75 74384.27
1002 76612.93 81456.34 82063.97
1003 82185.16 79742.33
```

| Store | Sales | Month |
|---|---|---|
| 1001 | 77163.19 | 1 |
| 1001 | 76804.75 | 2 |
| 1001 | 74384.27 | 3 |
| 1002 | 76612.93 | 1 |
| 1002 | 81456.34 | 2 |
| 1002 | 82063.97 | 3 |
| 1003 | 82185.16 | 1 |
| 1003 | 79742.33 | 2 |

- a. `data perm.topstores;`
   `infile sales98 misover;`
   `input Store Sales : comma. @;`
   `while sales ne .;`
   `month = month + 1;`
   `output;`
   `input sales : comma. @`
   `end;`
   `run;`

- b. `data perm.topstores`
   `infile sales98 missover`
   `input Store Sales : comma. @`
   `do while (sales ne).`
   `Month=0;`
   `month + 1;`
   `output;`
   `input sales : comma. @`
   `end;`

- c. `data perm.topstores`
   `infile sales98 missover`
   `input Store Sales : comma.`
   `Month @`
   `do while (sales ne).`
   `month + 1;`
   `input sales : comma. @`
   `end;`

- d. `data perm.topstores`
   `infile sales98 missover`
   `input Store Sales : comma. @`
   `Month=0;`
   `do while (sales ne).`
   `month + 1;`
   `output;`
   `input sales : comma. @`
   `end;`
   `run;`

正确答案：d
第一个 `INPUT` 语句读取 STORE 并使用 `@` 保持记录。`Month` 初始化为 0。`DO` 循环在 SALES 不缺失时执行。在循环内部，`month` 递增，`output`，读取下一个 SALES 值并保持记录。循环返回 DATA 步顶部，保持记录被释放，控制语句读取下一个记录。

10. 读取此外部文件的 DATA 步产生了多少个观测值？

| 11----+10----+20----+30----+40 |
| 01 CHOCOLATE VANILLA RASPBERRY |
| 02 VANILLA PEACH |
| 03 CHOCOLATE |
| 04 RASPBERRY PEACH CHOCOLATE |
| 05 STRAWBERRY VANILLA CHOCOLATE |

```
data perm.choices;
infile icecream missover;
input Day $ Flavor : $10. @;
```

```
do while (flavor ne ' ');
  output;
  input flavor : $10.;
;
```

- a. 3
b. 5
c. 12
d. 15

正确答案：c

此 DATA 步为每个重复的字段产生一个观测值。INFILE 语句中的 MISSOVER 选项防止 SAS 在记录记录末尾出现缺失值时读取下一条记录。每个观测值包含一个 `Flavor` 值，与相应的 `ID` 值配对。因为 `Flavor` 有 12 个值，所以数据集中有 12 个观测值。

# 第 21 章：读取分层文件

- 1. 当你编写一个 DATA 步来为每个详细记录创建一个观测值时，你需要：
   a. 区分头部记录和详细记录。
   b. 将头部数据作为每个观测值的一部分，直到遇到下一个头部记录。
   c. 保留当前记录，以便读取记录中的其他值。
   d. 以上所有

正确答案：d

为了为每个详细记录创建一个观测值，必须区分头部记录和详细记录。使用 RETAIN 语句将头部数据作为每个观测值的一部分，直到遇到下一个头部记录。你还需要使用 @line-hold 修饰符保留当前记录，以便读取记录中的其他值。

- 2. 哪个 SAS 语句读取 `code`（第一个字段）的值，并保持记录，直到 INPUT 语句在 DATA 步的同一次迭代中读取同一记录的剩余值？

| ID | Description |
| :--- | :--- |
| 01 | Office Supplies |
| 02 | Paper Clips |
| 02 | Tape |
| 01 | Art Supplies |
| 02 | Crayons |
| 02 | Finger Paint |
| 02 | Construction Paper |

- a. `input code $2. @;`
- b. `input code $2. @@@;`
c. `retain code;`
d. 以上都不是

正确答案：a
使用 INPUT 语句来读取 `code` 的值。INPUT 语句末尾的单个 @ 符号保留当前记录，供 DATA 步的同一次迭代中的后续 INPUT 语句使用。

- 3. 哪个 SAS 语句检查“记录等于 C”的条件，并执行单个语句读取 `Amount` 的值？
a. `if record='C' then input @3 Amount comma7;`
b. `if record='C' then input @3 Amount comma7;`
c. `if record='C' then do input @3 Amount comma7;`

正确答案：b
IF 语句定义了“记录等于 C”的条件，并在条件真同时执行 INPUT 语句来读取 `Amount` 的值。C 必须放在引号内，并且必须按照所示精确指定，因为它是一个字符值。

- 4. 在第六次迭代中读取 `code` 的值后，哪一个程序向量（program vector）插图是正确的？

```
1-----+----10+----+20----+----+30
H Lettuce
P Green Leaf Quality Growers
P Iceberg Pleasant Farm
P Romaine Quality Growers
H Squash
P Yellow Tasty Acres
P Zucchini Pleasant Farm
```

```sas
data_perm.produce (drop=code);
infile orders;
retaining Vegetable;
input code $2. @;
if code='H' then input @3 vegetable $6;
if code='P';
input @3 Variety : $10. $15;
run;
proc print data_perm;
run;
```

| _N | Vegetable | Variety | Supplier |
| :--- | :--- | :--- | :--- |
| 6 | | P | |

- b.
| _N | Vegetable | Variety | Supplier |
| :--- | :--- | :--- | :--- |
| 6 | | P | |

- c.
| _N | Vegetable | Variety | Supplier |
| :--- | :--- | :--- | :--- |
| 6 | | H | |

- d.
| _N | Vegetable | Variety | Supplier |
| :--- | :--- | :--- | :--- |
| 6 | | H | |

正确答案：b
`Vegetable` 的值在 DATA 步的多次迭代中被保留。作为第六次迭代，INPUT 语句读取 `code` 的值并保持记录，以便可以使用额外的 INPUT 语句读取 `Variety` 和 `Supplier` 的值。

- 5. 当 DATA 步的第四次迭代完成后，会发生什么？

| | | Total || :--- | :--- | :--- |
| F Apples | | $50 |
| V Gala | | $50 |
| V Golden Delicious | | $99 |
| V Rome | | $35 |
| F Oranges | | $79 |
| V Navel | | $99 |
| V Temple | | $99 |

```sas
data.perm.orders (drop=type);
infile produce;
retain Fruit;
input type $1 @;
if type='F' then input @3 fruit $7;
if type='V';
input @3 Variety :$16 @20 Price,
```
