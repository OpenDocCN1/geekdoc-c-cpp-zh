

### Display 8.22 定义识字类别的指示变量

```
data toyexample;
    input literacy @@;

/* method 1-2:
    Boolean trick to assign category labels 1-4;
    If a logical comparison is TRUE (FALSE), it evaluates to 1 (0)
    e.g. if literacy=54, (53<literacy<=76)=TRUE while
        (0<literacy<=53)=(76<literacy<=90)=(90<literacy<=100)=FALSE
        And so cat_literacy1 = 1*0 + 2*1 + 3*0 + 4*0 = 2
*/

cat_literacy1 = 1*(0<literacy<=53) + 2*(53<literacy<=76)
    + 3*(76<literacy<=90) + 4*(90<literacy<=100);

cat_literacy2 = 1*(literacy<=53) + 2*(53<literacy<=76)
    + 3*(76<literacy<=90) + 4*(90<literacy<=100);

/*
    method 3:
    First check for nonmissing and valid ranges before Boolean trick
*/

if ( (literacy NE .) AND (0<=literacy<=100) ) then
    cat_literacy3 = 1*(literacy<=53) + 2*(53<literacy<=76)
        + 3*(76<literacy<=90) + 4*(90<literacy<=100);

/* method 4:
    IF-THEN-ELSE blocks to assign category labels
*/

if ( (literacy EQ .) OR (100<literacy)
        OR (literacy<0) ) then cat_literacy4=.;
else if (literacy <=53) then cat_literacy4=1;
else if (literacy <=76) then cat_literacy4=2;
else if (literacy <=90) then cat_literacy4=3;
else cat_literacy4=4;
datalines;
-99 25.55 73.7 83   99.9 107 .
;
run;
ods rtf file="C:\Users\baileraj.IT\Desktop\Display-8-22.rtf";
proc print data=toyexample;
run;
ods rtf close;
```

四个不同的指示变量显示在 Display 8.23 中。

### Display 8.23 不同指示变量的 PROC PRINT 输出

| Obs | literacy | cat_literacy1 | cat_literacy2 | cat_literacy3 | cat_literacy4 |
|---|---|---|---|---|---|
| 1 | -99.00 | 0 | 1 | . | . |
| 2 | 25.55 | 1 | 1 | 1 | 1 |
| 3 | 73.70 | 2 | 2 | 2 | 2 |
| 4 | 83.00 | 3 | 3 | 3 | 3 |
| 5 | 99.90 | 4 | 4 | 4 | 4 |
| 6 | 107.00 | 0 | 0 | . | . |
| 7 | . | 0 | 1 | . | . |

观察定义变量 `cat_literacy1` 的第一种方法。当 literacy=54 时，第一个条件 (0<literacy<=53) 为 FALSE。第二个条件 (53<literacy<=76) 为 TRUE。第三个条件 (76<literacy<=90) 为 FALSE。第四个条件 (90<literacy<=100) 为 FALSE。考虑以下表达式：

```
cat_literacy1 = 1*(0<literacy<=53) + 2*(53<literacy<=76)
              + 3*(76<literacy<=90) + 4*(90<literacy<=100);
```

如果 TRUE =1 且 FALSE =0，则该表达式求值为以下内容：

```
cat_literacy1 = 1*(0) + 2*(1) + 3*(0) + 4*(0) = 2
```

如果你希望保留 LITERACY 的缺失值，或者希望将有效范围之外的取值赋为缺失值，则此代码不会按预期行为运行。如果 LITERACY 缺失 (.)，或其取值超出所测试的范围 (-99 到 107)，则没有任何条件为 TRUE，且 `cat_literacy1=0`。

第二种方法导致了值得注意的其他行为。考虑以下表达式：

```
cat_literacy2 = 1*(literacy<=53) + 2*(53<literacy<=76)
              + 3*(76<literacy<=90) + 4*(90<literacy<=100);
```

此方法在 LITERACY 为 -99 或缺失时将 `cat_literacy2=1`。此赋值发生是因为条件 (literacy<=53) 对 -99 为 TRUE（不出所料，因为 -99≤53），且缺失观测为 TRUE（可能令人惊讶，因为你可能不知道缺失 (.)≤53）。

第三种和第四种方法的行为符合预期。首先进行非缺失值和有效范围的 IF 检查。如果该值通过此检查，则类别的分配遵循前两种方法分配类别的方式。第四种方法使用 IF–THEN–ELSE 构造。代码稍长，但可能更容易理解。关键是始终使用边界、无效和缺失案例测试你的代码，以确保你得到想要的结果。

## 8.4 任务执行的顺序

在开始为问题实现编程解决方案之前，你需要知道计算执行的顺序（所谓的运算顺序或运算优先级）。让我们快速看一下初学者程序员常见的头痛来源。（如果你已经知道这些内容，则跳过。）计算机做你所说的，而不是你所想的。因此，你应仔细编写程序，尤其是方程。当编码方程时，请记住计算机以特定顺序执行方程的各部分。如果没有括号，则先进行指数运算。然后，第二步进行乘法和除法（同等优先级）。最后进行加法和减法（同等优先级）。括号内的表达式先于其他表达式处理。处理方程时从左到右求值。AND 运算符在 OR 运算符之前执行，这在复杂的表达式中如果程序未包含括号时可能会产生差异。

让我们从抽象转向具体。下一个示例说明了粗心编码的一些危险。在示例中，请特别注意计算对：

```
x1a=3×2² versus x1b=(3×2)²
x2a=3−2/2 versus x2b=(3−2)/2
x3a=−2² versus x3b=(−2)²
```

你可能期望由于括号的分组，这对会产生不同的值。然而，当你查看代码时，这并不完全清晰。例如，如果你天真地认为代码不考虑运算顺序而从左到右处理，那么你可能会期望 `x2a=3−2/2` 和 `x2b=(3−2)/2` 产生相同的答案。Display 8.24 包含测试代码，证明情况并非如此。

### Display 8.24 运算顺序的测试代码

```
data preced_test;
  x1a = 3*2**2;
  x1b = (3*2)**2;
  x2a = 3-2/2;
  x2b = (3-2)/2;
  x3a = -2**2;
  x3b = (-2)**2;
  put '--------------------------------';
  put ' | Order of operations |';
  put ' | illustrated |';
  put '--------------------------------';
  put '  3*2**2 = ' x1a;
  put ' (3*2)**2 = ' x1b;
  put '  3-2/2 = ' x2a;
  put ' (3-2)/2 = ' x2b;
  put '  -2**2 = ' x3a;
  put ' (-2)**2 = ' x3b;
run;
```

Display 8.24 中编码的每个运算的结果显示在 Display 8.25 中。

### Display 8.25 运算顺序测试代码的输出

```
--------------------------------
| Order of operations |
| illustrated |
--------------------------------
  3*2**2 = 12
 (3*2)**2 = 36
  3-2/2 = 2
 (3-2)/2 = 0.5
  -2**2 = -4
 (-2)**2 = 4
```

这个编程故事有一个简单的寓意——如果你希望运算按特定顺序进行，请使用括号。

## 8.5 数据集中保留什么、丢弃什么

你已使用 DATA 步将数据读入变量并操纵数据，例如定义新变量。完成这些任务后，你可能希望通过去掉多余变量来简化数据集。选项 DROP 和 KEEP 指定要从 SAS 数据集中删除或保留的变量。除了消除变量之外，你可能还希望保留满足某些条件的观测。语句 WHERE 和 IF 使你能够指定要在 SAS 数据集中保留的变量的值。例如，以下语句仅包含数值变量 LITERACY 缺失值的观测：

```
if literacy EQ .;
```

IF 语句可用于一系列 IF-THEN-ELSE 表达式。WHERE 语句可以执行与 IF 语句类似的工作，但它具有特定的运算符，BETWEEN-AND、CONTAINS、IS NULL、IS MISSING、LIKE 和 SAME-AND，这些在 SAS Help 中有详细记录。

DATA 步中的编程语句即使在常规分析中也经常需要。在第 2 章中，SET 语句将多个数据集的内容放入新创建的数据集中。OUTPUT 语句将变量集合的当前规范写入数据集。OUTPUT 语句可用于扩展数据集，以便为当前数据集中的每个观测在新数据集中创建多行。这在 Display 8.26 中有所演示，该示例说明了变量和记录的操纵。代码首先将 nitrofen 数据读入名为 nitro 的 SAS 数据集。然后 nitro 的内容被设置为新的 SAS 数据集 `nitrofenA`。每个动物的单条记录被扩展为每个窝的单独行。通过施加 WHERE 限制来打印前四个动物的数据。非正式挑战：你能想到另一种纳入此打印限制的方法吗？这种数据结构通常用于 SAS 中的特定模型，例如线性混合效应模型，可使用 PROC MIXED 分析。

