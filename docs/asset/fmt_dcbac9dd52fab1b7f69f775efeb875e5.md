
### 4. `beta`: II 类错误率

### 5. `alpha`: I 类错误率

### 6. `simN`: 蒙特卡洛模拟的迭代次数

## 示例代码 11.2：计算所需样本量的 SimNorm 宏

```sas
%macro simnorm(seed1, seed2, mux, muy, stdx, stdy, beta, simN=10000, alpha)
data x;
  call streaminit(&seed1);
  do i = 1 to &simN
    x=rand('normal', &mux, &stdx);
    output;
  end;
run;

data y;
  call streaminit(&seed2);
  do i = 1 to &simN
    y=rand('normal', &muy, &stdy);
    output;
  end;
run;

data one;
  merge x y;
```

```sas
if x<y then flag=1;
else flag=0;
run;
proc means noprint data=one;
var flag;
output out=pl mean=pl;
run;
data_null;
set pl;
call symput('pl', compress(pl));
run;
data_null;
syl=&seed2 +1;
call streaminit(syl);
y1=rand('normal', &muy, &stdx);
output;
call symput('yl', compress(yl));
run;
data_null;
sy2=&seed2 +2;
call streaminit(sy2);
y2=rand('normal', &mux, &stdx);
output;
call symput('y2', compress(y2)));
run;
data x;
set x;
if x<&y1 and x<&y2 then flag=1;
else flag=0;
run;
proc means noprint data=x;
var flag;
output out=p2 mean=p2;
run;
data_null;
set p2;
call symput('p2', compress(p2)));
run;
data_null;
sxl=&seed1 +1;
call streaminit(sxl);
x1=rand('normal', &mux, &stdx);
output;
call symput('x1', compress(x1)));
run;
data_null;
sx2=&seed2 +1;
call streaminit(sx2);
x2=rand('normal', &mux, &stdx);
output;
call symput('x2', compress(x2)));
run;
data y;
set y;
if y>&y1 and y>&y2 then flag=1;
else flag=0;
run;
proc means noprint data=y;
var flag;
output=p3 mean=p3;
run;
data_null;
set p3;
call symput('p3', compress(p3)));
run;
```

```sas
title 'Normal Distribution'

%MSower(&&beta, &p1, &p2, &alpha);

%end simnorm;

%simnorm(seed1=1, seed2=100, mux=5, muy=8, stdx=2, stdy=1.5, beta=0.2, simN=10000, alpha=0.05);
```

宏调用的结果如示例代码 11.2 的输出所示。这表明，如果控制组的治疗结果遵循均值为 5、标准差为 2 正态分布；如果实验组的治疗结果遵循均值为 8、标准差为 1.5 的正态分布，则通过蒙特卡洛模拟得到的 `p1`、`p2` 和 `p3` 的估计值分别为 0.8837、0.9126 和 0.9985，拒绝零假设提供 80% 效能的最小样本量为每个治疗组 12。总样本量为 24 的实际效能为 82%。

# 表 11.4 示例代码 11.2 的输出

| 样本量 | p1 | p2 | p3 | alpha | beta | power |
|---|---|---|---|---|---|---|
| 12 | 0.8837 | 0.9126 | 0.9985 | 0.05 | 0.18012 | 0.81988 |

或者，如果治疗结果遵循 Gamma 分布，`simgamma` 使用公式 (6) 计算出提供指定 `$1-\beta$` 效能以拒绝零假设的最小样本量。指定的参数如下：

1. `seed1`, `seed2`: 用于生成随机数的种子
2. `mux`, `muy`: 控制组和实验组治疗结果的平均值
3. `stdx`, `stdy`: 控制组和实验组治疗结果的标准差
4. `beta`: II 类错误率
5. `alpha`: I 类错误率
6. `simN`: 蒙特卡洛模拟的迭代次数

## 示例代码 11.3：计算所需样本量的 SimGamma 宏

```sas
%macro simgamma(seed1, seed2, mux, muy, stdx, stdy, beta, simN=10000, alpha)

data temp;

  ax=round((mux**2)/(stdx**2));

  bx=round((mux/(stdx**2)));

  ay=round((mux**2)/(stdy**2));

  by=round((muy/(stdy**2)));

  ... (注: 此处原文代码似乎存在逻辑错误，如应为rand(gamma)，但根据指令，代码块不翻译且保持原样)

output;

run;

data x;

  call streaminit(&seed1);

  do i = 1 to &simN

    x=rand('gamma', ax, by);

    output;

  end;

run;

data y;

  call streaminit(&seed2);

  do i = 1 to &simN

    y=rand('gamma', ay, by);

    output;

  end;

run;

data one;

  merge x y;

  if x<y then flag=1;

else flag=0;

run;

proc means noprint data=one;

var flag;

output out=pl mean=pl;

run;

data_null;

set pl;

call symput('pl', compress(pl)));

run;

data_null;

syl=&seed2 +1;

call streaminit(syl);

y1=rand('gamma', ay, by);

output;

call symput('y1', compress(yl)));

run;

data_null;

sy2=&seed2 +2;

call streaminit(sy2);

y2=rand('gamma', ax, by);

output;

call symput('y2', compress(y2)));

run;

data x;

set x;

if x<&y1 and x<&y2 then flag=1;

else flag=0;

run;

proc means noprint data=x;

var flag;

output out=p2 mean=p2;

run;

data_null;

set p2;

call symput('p2', compress(p2)));

run;

data_null;

sxl=&seed1 +1;

call streaminit(sxl);

x1=rand('gamma', ax, by);

output;

call symput('x1', compress(x1)));

run;

data_null;

sx2=&seed2 +1;

call streaminit(sx2);

x2=rand('gamma', ax, by);

output;

call symput('x2', compress(x2)));

run;

data y;

set y;

if y>&y1 and y>&y2 then flag=1;

else flag=0;

run;

proc means noprint data=y;

var flag;

output=p3 mean=p3;

run;

data_null;

set p3;

call symput('p3', compress(p3)));

run;
```

```sas
title 'Normal Distribution'
%MSower(&&beta, &p1, &p2, &alpha);
%end simgamma;

%simgamma(seed1=1, seed2=100, mux=5, muy=8, stdx=2, stdy=1.5, beta=0.2, simN=10000, alpha=0.05);
```

宏调用的结果如示例代码 11.3 的输出所示。这表明，如果控制组的治疗结果遵循均值为 25、标准差为 2 正态分布；如果实验组的治疗结果遵循均值为 8、标准差为 1.5 的正态分布，则通过蒙特卡洛模拟得到的 `p1`、`p2` 和 `p3` 的估计值分别为 0.8837、0.9126 和 0.9985，拒绝零假设提供 80% 效能的最小样本量为每个治疗组 9。总样本量为 18 的实际效能为 81%。

# 表 11.5 示例代码 11.2 的输出

| 样本量 | p1 | p2 | p3 | alpha | beta | power |
|---|---|---|---|---|---|---|
| 12 | 0.8837 | 0.9126 | 0.9985 | 0.05 | 0.18012 | 0.81988 |

临床试验涉及随机化患者数量的要求，而检测灵敏度则在筛选患者数量方面起着至关重要的作用。最相关的检测是识别那些对新治疗比对照组更敏感的患者。当对照组活性药物时，这尤为重要。

Maitournam 和 Simon [25] 做了大量的模拟，评估了富集设计（enrichment design）与全人群设计（all-comers design）的相对效率，并得出结论：

- 当治疗效应限于标记物阳性（marker+）患者且检测特异性接近1时，富集设计在随机化人数和筛选人数方面通常比全人群设计高效得多。随着检测特异性的下降，效率也会随之降低。
- 如果标记物阴性（marker-）患者的治疗效果是阳性患者的一半，即使检测是完美的，富集设计所需的筛选人数也比未筛选的设计要多。富集设计中筛选人数的增加关键取决于检测的灵敏度。在这种情况下，除非检测的特异性接近1，否则富集设计在随机化人数方面没有实质性优势。——如果是如此，优选设计的选择将取决于其他考虑因素，如随机化的相对成本、安全耐受性特征以及更广泛标签适应的商业价值。

## 11.4 适应性富集设计

人们已经认识并记录，制药和生物技术研究投入的增加并没有反映临床开发成功率的提高。Woodcock [26] 概述了药物开发成功率下降的一些原因，即：(i) 由于改进空间缩小，证明药物获益的门槛提高；(ii) 成本和复杂性的增加可能降低许多候选药物进入临床的能力；(iii) 遗传学及相关学科尚未充分发展；(iv) 慢性病使得研究赞助者难以选择易于调查和投资的目标。美国食品药品管理局（FDA）举办了一项“关键路径计划”（Critical Path Initiative），以识别医疗产品管道潜在的关键科学挑战，并在2006年发布了*关键路径机会清单*，特别是借鉴了以往经验、正在进行的创新临床试验以及积累的数据。这种创新意味着了适应性设计方法的使用以及使用贝叶斯方法的潜力。Chow 等人 [27] 将“适应性设计”定义为一种在试验启动后允许对试验和/或试验的统计程序进行调整，且不损害试验的有效性和完整性的设计。Gallo 等人 [28] 的 PRMA 工作小组论文提到“适应性设计是一种使用累积数据来在试验持续过程中决定如何修改研究各个方面的临床试验，且不损害试验的有效性和完整性”。在过去的十年中，由于其灵活性和效率，适应性设计方法的应用变得非常流行。然而，这有时是以增加复杂性和后勤挑战为代价的。在大多数情况下，必须进行密集的规划以定义通过/不通过标准，赞助者应拥有足够的资源来实施和执行。考虑到试验的演变，一些适应性设计包括：

- (i) 分组序设计，
- (ii) 样本量估计设计，
- (iii) 剂量寻找设计，
- (iv) 退出设计，
- (v) 适应性随机化设计，
- (vi) 切换设计，
- (vii) 多重性设计，
- (viii) 生物标志物选择设计，
- (ix) 富集设计。

在这里我们将主要讨论与富集相关的设计。

### 11.4.2 频率学方法

#### 11.4.2.1 适应性签名设计

经典设计仅涉及一个生物标志物，且假设截点（cut-off）是预先的。当潜在生物标志物未知但某些证据表明靶向治疗可能有效时，使用签名设计（signature design）。签名设计通过以下步骤完成：

1. 将研究人群分为训练子样本和验证子样本。
2. 使用训练子样本建立模型，预测靶向治疗与对照组之间的治疗差异随基线变量的变化。
3. 该模型也称为获益函数（benefit function），用于验证验证样本的结果。
4. 该设计使用的获益函数是针对预设数量的生物标志物和显著性水平，治疗相互作用的最小优势值比 [29]。
5. 风险差（risk difference）是另一种使用的获益函数，它是靶向治疗与对照组之间概率随基线变量变化的差异 [20,31]。
6. 对样本中的每个受试者进行预测，并计算预测评分以将该子类分类为敏感或非敏感。
7. 使用预设的预测评分截点选择亚组。
8. 在该亚组中进行第二次假设检验，以观察靶向治疗相对于对照组的获益。该测试在得低的显著性水平下进行（例如：0.01或0.02）。

如果初始假设在较低显著性水平被拒绝，则宣布靶向治疗对于总体人群优于对照组。此时，人群测试完成。

通常，随着敏感患者比例的增加，实验组和对照组客观缓解率之间的差异也随之增加。因此，对于高于某些阈值的流行率，总体效应检验的效力将主导敏感子集的效力。适应性签名设计保留了检测总体效应的能力。然而，它与传统设计（具有广泛入选标准的总体效应测试）相比的优势有所降低。[25] 中提供了协助研究人员评估敏感子集与总体测试之间效力关系的公式。开发了基于 [25] 中公式 (1.1) 计算效力的宏程序。在计算总体测试的效力时，需要指定以下参数：

- `pe`: 接受实验治疗患者的预期反应概率
- `pc`: 接受对照治疗患者的预期反应概率
- `alpha`: 单侧显著性水平
- `N`: 总样本量。

同样，可以通过在敏感性子集中指定这些参数，使用宏来计算子集检验的效能。

例如，如果接受实验治疗的患者预期响应概率为 0.5，接受对照治疗的患者预期响应概率为 0.2，假设单侧显著性水平为 0.05且总样本量为 100，则整体检验的效能可以通过“示例代码 11.4 适应签名设计的效能”进行计算。在本例中，效能为 94.3%。

## 示例代码 11.4 适应签名设计的效能

```sas
%macro power(pe, pc, alpha, N);
data result;
pe=&pe;
pc=&pc;
alpha=&alpha;
N=N;
nb=1&alpha;
pbar=(pe+pc)/2;
za=quantile('Normal', b);
num=(pe-pc)-2*sqrt(pbar*(1-pbar)*4/N);
den=pe*(1-pe)*2/N+pc*(1-pc)*2/N;
alpha=num/den;
power=CDF('Normal', a);

run;

proc noobs;
var pe pc N alpha power;
run;
mend power;
%power(0.5, 0.2, 100);
```

这种设计的优势在于它能够降低在关键性试验中丢失更广泛人群标签的风险。根据 Freidlin 和 Simon [29] 的研究，这种设计可能是理想的，即利用二期临床试验为对靶向治疗反应较好的患者开发检测方法或签名（signatures）。该设计的缺点是，只有一半的患者被用于开发或验证。如果生物标志物敏感患者亚组的患病率较低，则这种设计将需要大量患者进行筛选。这在经济上可能是不可行的，而且在操作上具有挑战性，并会延长入组期。另一个缺点是，子组数量增加会导致高维数据，可能需要较大的样本量来确保试验具有足够的效能。

### 11.4.2.2 生物标志物自适应阈值设计

在这种设计 [32] 中，整体治疗效应的检验与对预设的生物标志物亚组（被认为对靶向治疗最敏感）的截断点（cutpoint）的开发和验证相结合。统计假设检验通过拆分整体 I 类错误率 `alpha` 来进行。首先，在 `alpha1` 处比较整体人群的治疗反应，如果不显著，则在 `alpha-1` 处进行第二次检验。例如，如果无获益的零假设（a）在所需的显著性水平（例如 0.04）下被拒绝，则停止检验；否则，对假设 (b) 进行检验至 0.01 的水平，以将整体 `alpha` 控制在 0.05 以下。使用 Altman 等人 [33] 提出的简化截断模型来开发所提的程序。整体患者人群被分为两组：基于生物标志物的（敏感）和非基于生物标志物的（非敏感）。这种分类可能会导致某些信息的丢失，但所提的检验程序对于偏离简化截断模型的情况具有稳健性。使用置换重采样法（permutation resampling）来选择最佳截断点，以避免多重性问题 [34]。

当治疗效应限制在亚人群时，临床试验样本规划的方法见 [32] 的附录 B。假设在一个具有事件时间结局的试验中，整体检验检测目标治疗效应（在显著性水平 `alpha` 下）并达到 `1-beta` 效能所需的观测事件数，可以通过“示例代码 11.5 生物标志物自适应阈值设计的事件数”中的事件宏进行计算。
