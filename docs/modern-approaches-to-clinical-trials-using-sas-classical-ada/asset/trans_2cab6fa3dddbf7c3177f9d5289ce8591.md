

# 示例代码 9.3 偏倚币设计

```sas
* f(x)=1-x <- 分配到 A 组的概率 */
* g(x)=x <- 分配到 B 组的概率 */
* 其中 x <- (治疗组间人数差异)/(总人数人数) */

%macro BCDandomize(n1, n2, seed);
data Assignment;
%let numer=EVAL(&n1+&n2);
%let denom=EVAL(&n1+&n2);

* 以概率 x 分配到 B，概率 1-x 分配到 A */
%if %SYSEVAL(&n1&=0) & %SYSEVAL(&n2&=0) %then let DiffRatio = %SYSEVAL(
%let AllocProb=%SYSEVAL(1/2-&DiffRatio/2);
%let RandNum=%SYFUNC(runani(&seed)); *均匀[0,1] 随机变量;
%if %SYSEVAL(&RandNum <&AllocProb) %then let Assign-A=;
%else let Assign-B=;

* 创建受试者人数变量 _ */
%let AssignNum = %EVAL(&n1+&n2+&1);
groupA = &n1;
groupB = &n2;
allopB = &AllocProb;
newGroup = "Assign";

label group groupA = "A组人数"
groupB = "B组人数"
allop = "分配到 A 组的概率"
newGroup = "下一次分配"
run;

proc print data=Assignment label noobs;
run;
%end BCDandomize;

%BCDandomize(n1=0,n2=0,seed=123);
%BCDandomize(n1=5,n2=10,seed=123);
```

# 表 9.4 示例代码 9.3 的新试验

| A组人数 | B组人数 | 分配到 A 组的概率 | 下一次分配 |
| 0 | 0 | 0.5 | B |

在正在进行的试验中，动态偏倚币设计（BCD）可以自适应地改变分配比例。假设试验已向 A 组分配了 5 名患者，向 B 组分配了 10 名患者。我们再次像[示例代码 9.3 偏倚币设计](#)（示例代码 9.3 的进行试验）的第二次调用一样应用 BCDandomize 宏。

# 表 9.5 示例代码 9.3 的进行试验

| A组人数 | B组人数 | 分配到 A 组的概率 | 下一次分配 |
| | | | |

## 9.4 协变量自适应随机化

## 9.4.1 分层随机化

在随机化之前，会收集一些基线预后因素（协变量），例如年龄、性别和疾病严重程度，这些因素可能对治疗结果产生重要影响。因此，在这些协变量上平衡治疗分配是理想的，以便进行有效且高效的治疗比较。

在重要协变量上平衡治疗分配的最简单方法是通过分层。如图 9.1 “分层随机化的插图”所示，试验参与者首先根据其预后变量的值被分为互斥的各个层，然后在每个层内将他们随机分配到每种治疗中。

图 9.1 分层随机化的插图

![](img/f4ec2665c3484c528370923aeb5cb99f_434_0.png)

如果层数较少，分层随机化可以在协变量的各种组合之间达到平衡。然而，如果层数相对于受试者数量较大，分层可能变得毫无意义。因为层数随着分层因素数量的增加呈乘法增长，某些层可能会变得非常稀疏甚至为空。这反可能导致治疗组之间出现显著的不平衡 [5]。

```sas
可以使用 plan 来设计分层随机化程序。假设试验已入组了 24 名患者，我们需要根据两个预后因素对受试者进行分层
```

[sas]
患者进行分层：性别和血压。该因素因素两个水平——男性或女性，而血压有 3 个水平——高、正常和低。结合置乱块随机化，基于这两个因素的分层导致了六个互斥的组。如果我们取块大小为 4，示例代码 9.4 “分层随机化”的输出为此类试验产生了一个分层块随机化方案（示例代码 9.4 的输出）。

# 示例代码 9.4 分层随机化

```sas
proc plan seed=123;
    factors Block=1 random Gender=2 ordered Pressure=3 ordered Sequence=4
    ordered/noprint;
    treatments Treatment=4 randomRandomization Gender cvals=('Male' 'Female') ordered
    output=stratifiedRandomization
    Pressure cvals=('High' 'Normal' 'Low')
    Treatment cvals=('A' 'B')
run;

proc print data=stratifiedRandomization;
run;
```

# 表 9.6 示例代码 9.4 的输出

| 性别 | 压力 | 序列 | 治疗 |
|--- | --- | --- | --- |
| 男性 | 高 | 1 | A |
| 男性 | 高 | 2 | B |
| 男性 | 高 | 3 | A |
| 男性 | 高 | 4 | B |
| 男性 | 正常 | 1 | A |
| 男性 | 正常 | 2 | B |
| 男性 | 正常 | 3 | A |
| 男性 | 正常 | 4 | B |
| 男性 | 低 | 1 | A |
| 男性 | 低 | 2 | B |
| 男性 | 低 | 3 | A |
| 男性 | 低 | 4 | B |
| 女性 | 高 | 1 | A |
| 女性 | 高 | 2 | B |
| 女性 | 高 | 3 | A |
| 女性 | 高 | 4 | B |
| 女性 | 正常 | 1 | A |
| 女性 | 正常 | 2 | B |
| 女性 | 正常 | 3 | A |
| 女性 | 正常 | 4 | B |
| 女性 | 低 | 1 | A |
| 女性 | 低 | 2 | B |
| 女性 | 低 | 3 | A |
| 女性 | 低 | 4 | B |

## 9.4.2 协变量自适应随机化

当存在许多预后因素时，要在试验中实现平衡是困难的。Taves [6] 和 Simon [7] 提出了最小化方法（也称为动态分配、协变量自适应或随机化），用于顺序治疗分配。在随机化过程中，每个受试者的分配概率取决于当前的平衡情况。

详细而言，令 $l$ 表示预后因素的总数，在双臂试验中，令 $n_{1}$ 为分配到 1 组的人数，$n_{2}$ 为分配到 2 组的人数，则 $i$ 的差异由

$g_i = |n_{1} - n_{2}|, i=1, \dots$ 给出。

总不平衡通过每个因素的加权和来衡量，$G = \sum_{i=1}^l w_i g_i$，其中 $w_i$ 是描述第 $i$ 个因素的重要性。表 9.7 最小化方法的插图

| 预后因素 | 治疗 | 不平衡 | 新患者 | 潜在不平衡 |
|---|---|---|---|---|
| | A | B | | 分配到 A | 分配到 B |
| 性别 | 男性 | 9 | 7 | 2 | 1 |
| | 女性 | 10 | 13 | 4 | 4 |
| 肿瘤 | I | 7 | 6 | 1 | 2 |
| II | 10 | 3 | 3 | 3 |
| III | 2 | 2 | 0 | 总计 | 8 |

