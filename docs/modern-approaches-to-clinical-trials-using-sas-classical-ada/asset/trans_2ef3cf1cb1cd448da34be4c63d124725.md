

概率 p = 0.75（示例代码 9.5 基于最小化的协变量自适应分配）。

## 示例代码 9.5 基于最小化的协变量自适应分配

```sas
data FactorWeight;
input w;
datalines;
1
1
;
run;

%macro MinimizationRandomize(TreatedPatients,NewPatient,FactorWeight,p,seed);
proc ilm;
use &TreatedPatients;
read all into X;
use &TreatedPatients;
read all var (group);
use &NewPatient;
read all into Y;
use &FactorWeight;
read all;
call randseed(&seed);
X=X//Y;

imA=0;
groupA=group//'A';
do i=1 to ncol(X);
  do j=1 to max(X[i,j]);
    imA=imA+w[i]*abs(sum(groupA[loc(X,[i,j])='A'])-sum(groupA[loc(X,[i,j])='B']));
  end;
end;
nimB=0;
groupB=group//'B';
do i=1 to ncol(X);
  do j=1 to max(X[i,j]);
    imB=imB+w[i]*abs(sum(groupB[loc(X,[i,j])='A'])-sum(groupB[loc(X,[i,j])='B']));
  end;
end;
print imA imB;

nu=1;
call randgen(u, "Uniform");

if (imA<imB & u<=p) then
call symput('newgroup', 'A');
if (imA>=imB & u<=p) then
call symput('newgroup', 'B');
if (imA<imB & u>p) then
call symput('newgroup', 'B');
if (imA>imB & u>p) then
call symput('newgroup', 'A');

NextGroup=sumget('newgroup');
print NextGroup;
quit;
```

```sas
data &NewPatient;
  length group $;
  group=symget("newgroup");
  set &NewPatient;
run;
```

```sas
proc data=\&TreatedPatients;
run;

data &TreatedPatients;
  set &TreatedPatients. &Newpatient;
run;
```

```sas
proc data=\&TreatedPatients;
run;
%mend MinimizationRandomize;
```

- * 第1个受试者：男性，肿瘤 I
  data NewPatient;
  input gender tumororage;
  datalines;
  1 1

```sas
%MinimizationRandomize(TreatedPatients,NewPatient,FactorWeight,p=0.75,seed=6)
```

- * 第2个受试者：男性，肿瘤 II
  data NewPatient;
  input gender tumororage;
  datalines;
  1 2

```sas
%MinimizationRandomize(TreatedPatients,NewPatient,FactorWeight,p=0.75,seed=6)
```

- * 第3个受试者：女性，肿瘤 II
  data NewPatient;
  input gender tumororage;
  datalines;
  2 2

```sas
%MinimizationRandomize(TreatedPatients,NewPatient,FactorWeight,p=0.75,seed=6)
```

该宏产生了一组输出。首先，它提供了当新患者被分配到组 A 和 B 时的总不平衡量；其次，宏根据最小化方法为新受试者建议一个分组；最后，通过包含新患者的数据来更新 TreatedPatients 数据集。上述示例的完整输出在此省略，我们将在“示例代码 9.5 的输出”中总结随机化的结果。

### 表格 9.8 示例代码 9.5 的输出

| 受试者编号 (Sub) | 治疗组 | 性别 | 不平衡（分配到 A） | 不平衡（分配到 B） |
|---|---|---|---|---|
| 1 | B | 男性 | 12 | 8 |
| 2 | A | 男性 | 8 | 8 |
| 3 | A | 女性 | 6 | 10 |

因此，为了最小化总不平衡量，第一个受试者应被分配到治疗 B。对于第二个受试者，无论该参与者被分配到治疗 A 还是 B，总不平衡量都是相同的。因此，我们可以完全随机地选择治疗。显然，第三个受试者将接受治疗 A，以最小化总不平衡量。

## 9.4.3 基于模型的优化协变量自适应随机化

为了实施最小化方法，需要对连续协变量进行分类。然而，确定分类的数量和相应的截止值通常是任意的。作为替代，可以开发一种优化随机化程序，使得在存在协变量的情况下估计治疗效应方差最小。具体而言，令 $Y_j$ 为第 $j$ 个患者的结果，$X_j$ 为 $p$ 维协变量（包括截距），$Z_j$ 为治疗指示，如果第 $j$ 个患者被分配到治疗组则值为 1，如果分配到控制组则值为 -1。对于连续结果 $Y_j$，我们假设一个线性模型：

$$$$Y_j = X_j^T \beta + Z_j \epsilon_j.$$

其中 $\epsilon_j$ 是从均值为 0、方差为 $\sigma^2$ 的正态分布的随机误差，$\beta$ 和 $\zeta$ 是待估计的参数，其中 $\zeta$ 表示治疗效应。估计治疗效应的方差为：

$$$$Var(\hat{\zeta}) = \frac{\sigma^2}{n-Z^TX(X^TX)^{-1}X^TZ}.$$

其中 $X$ 表示协变量的 $n \times p$ 矩阵，$Z$ 是 $Z_j, j=1..n$ 的 $n \times 1$ 向量。因此，可以通过最小化损失函数来实现最小 $Var(\hat{\zeta})$：

$$$$\mathcal{L}_n = Z^TX(X^TX)^{-1}X^TZ.$$

这可以解释为由于治疗分配效率低下而导致的单位损失。

假设 $n$ 个患者已经分配到两个治疗组，并且收集了 $(n+1)$ 个患者的协变量 $X_{n+1}$。为了构建一个顺序程序，选择第 $(n+1)$ 个患者的治疗分配以以高概率最小化损失 $\mathcal{L}_{n+1}$。例如，$(n+1)$ 个患者被分配到治疗组的概率可以指定为

$$Pr(Z_{n+1}=1|R_{n+1}) = \frac{X_{n+1}^T(X^TX)^{-1}X^TZ}{1 + \gamma X_{n+1}^T(X^TX)^{-1}X^TZ}$$

其中 $\gamma \ge 0$ 是预设的调节参数，用于控制随机程度。显然，如果 $\gamma = 0$，该程序简化为等比例随机化；通常建议 $\gamma = 5$ 以平衡治疗组和损失。假设 $n$ 个患者已经分配到两个治疗组，并且收集了 $(n+1)$ 个患者的协变量 $X_{n+1}$。为了阐明基于模型的 CAR，我们根据其预后因素分配患者。一旦入组 $n$ 个患者，基于模型的 CAR 将通过包含新患者的数据更新 TreatedPatients 数据集。示例代码 9.6 的输出显示：

```sas
proc data=\&TreatedPatients;
run;
```
