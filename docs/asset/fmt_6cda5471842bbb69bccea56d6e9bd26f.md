
| 参数 | 最小值 | 最大值 | Theta0 参数=Theta0 | Pr > |t| |
| --- | --- | --- | --- | --- | --- |
| DIFF | -0.010824 | -0.010316 | 0 | -7.23 | <.0001 |

# 第5章 含有缺失值的倾向性评分

传递给 `PROC MIAN` 的两个数据集包含估计的治疗效应（数据集 `FOR_MI_EST`）及其相关的协方差矩阵（数据集 `FOR_MI_COV` 中的标准误差平方）。`PROC MIAN` 的输出包含总方差划分的信息，包括插补间和插补内的估计效应方差、多重插补参数、基于 t 分布的近似 95% 置信区间以及总方差。注意，对于有限次数的插补 (`M`)，Rubin 的方差估计量是不一致的，因为它具有非退化的卡方极限分布。因此，基于正态分布的 Wald 类型推断是无效的，使用的是 t 分布（Rubin, 1987）。缺失协变量对最终效应估计的影响也可以缺失信息比例（关于治疗效应）进行评估，在本例中该比例非常低（仅 2%）。

## 5.3.4 缺失模式 (MP) 分析

MP 方法通过仅包含缺失模式内的无值对每个缺失模式单独估计倾向性评分。因此，倾向性评分模型中的自变量在模式之间不同。实施 MP 的挑战通常是某些模式的样本量较小，导致模型估计不稳定。为了解决这个问题，我们开发了一种算法，根据相似性对小模式进行合并，以达到每个池指定的最小观测数（Qu and Lipkovich, 2009）。在合并相似模式后，我们使用边缘均值对每个池进行插补（以避免空洞），并使用逻辑回归模型估计倾向性评分。在本例中，我们将每个合并单元格具有至少 100 个观测值的缺失模式进行了合并。程序 5.5 提供了创建这些模式的宏。

### 116 使用 SAS 进行观察性健康数据分析

```sas
/* 创建缺失值及其缺失模式的指标 */
DATA MS;
SET &MSDATA;
ARRAY MS(&&MISSING) M1-M&MISSING;
ARRAY X(0:&&MISSING) &VARLIST;
MV = 0;
DO I = 1 TO &MISSING;
  IF X(I) = . THEN MS(I) = 1;
  ELSE MS(I) = 0;
  MV = 2*MV + MS(I);
END;
MV = MV + 1;
```

```sas
RUN;

/* 为每个缺失模式仅保留一条记录 */
PROC SORT DATA = MS OUT = PAT NODUPKEY
BY MV;
RUN;
```

```sas
/* 计算每个缺失模式中的观测数 */
PROC FREQ DATA = MS NOPRINT;
TABLE MV / OUT = M_MP (KEEP = MV COUNT);
RUN;
```

```sas
DATA PATTERN;
MERGE PATTERN M_MP;
BY MV;
RUN;

PROC SORT DATA = PATTERN;
BY DESCENDING COUNT;
RUN;
```

```sas
/* 从大到小将缺失模式分配给新索引 */
DATA PATTERN;
RETAIN MI1-M&MISSING MV COUNT MV_S;
SET PATTERN;
KEEP MI1-M&MISSING MV COUNT MV_S;
M_S = _N;
RUN;
```

```sas
PROC IML;
USE PATTERN;
READ ALL INTO A;
CLOSE PATTERN;
MS = A[, 1:&&MISSING];
MV = A[, 1*&MISSING];
N_MP = A[, 2*&MISSING];
MV_S = A[, 3*&MISSING];
```

```sas
M = ROW(MS);
M = NCL(MS);
```

```sas
/* 计算缺失模式之间的距离 */
DISTANCE = J(M, M, 0);
DO I = 1 TO M_MP;
  DO J = 0 TO M;
    DO L = 1 TO M;
      D = D + ((MS[I,L]-MS[J,L]) * (MS[I,L]-MS[J,L]));
    END;
  END;
```

## 第 5 章 带有缺失值的倾向评分 117

```sas
DISTANCE[I, J] = D;
DISTANCE[J, I] = D;
END;
I = 0;
M MV_POOL = 0;
MV_POOL = J(M_MP, 1, 0);

/* 根据相似性合并较小的缺失模式，
   使每个模式中达到预设的最小观测数 (&N_MP_MIN) */
DO WHILE (I < M_MP)
  I = I + 1;
  IF MV_POOL[I] = 0 THEN
    DO;
      K_MV_POOL = K_MV_POOL + 1;
      N_MP_POOL = N_MP[I];
      IF N_MP_POOL >= &N_MP_MIN THEN
        MV_POOL[I] = K_MV_POOL;
      END;
      ELSE
        IF I < M_MP THEN
          DO;
            A = DISTANCE([I+1]:MP, MP];
            B = MV([I+1]:M, MP);
            C = N_MP([I+1]:M, MP);
            D = MV([I+1]:M, MP);
            E = MV_POOL([I+1]:M, MP);
            TT = A || B || C || D || E;
            CALL SORT(TT, (1, 3));
            J = 0;
            DO WHILE (N_MP_POOL < &N_MP_MIN) AND (I+J < M_MP )
              J = J + 1;
              IF (TT[J,5] = 0) THEN
                DO;
                  N_MP_POOL = N_MP_POOL + TT[J,3];
                END;
              END;
            END;
          END;
      IF (N_MP_POOL >= &N_MP_MIN) THEN
        DO;
          MV_POOL[I] = K_MV_POOL;
          DO K = 1 TO J;
            MV_POOL[TT[K,4]] = K_MV_POOL;
          END;
        END;
      ELSE
        DO J = I TO M_MP;
          SGN_TMP = 0;
          K = 1;
          DO WHILE (SGN_TMP = 0 AND K <= M_MP)
            IF (DISTANCE[J,L] = 0 AND MV_POOL[J] = 0) THEN
              DO;
                MV_POOL[J] = MV_POOL[L];
                SGN_TMP = 1;
              END;
          END;
        END;
  END;
```

## 118 观察性健康数据分析

```sas
END;
K = K + 1;

END;
END;
MV_FINAL = MV || MV_POOL;

VARNAMES=('MV', 'MV_POOL');
CREATE MV_POOL FROM MV_FINAL(VARNAMES);
APPEND FROM_FINAL;

PROC SORT DATA = MVPOOL;
BY MV;
RUN;

PROC SORT DATA = MS;
BY MV;
RUN;

/* 变量POOL 表示合并后的缺失模式 */
DATA &OUTDATA(RENAME=(MV=MP, MV_POOL=MP));
MERGE MS MVPOOL;
BY MV;
RUN;

%MP_ASSIGN;
```

## 程序 5.6 缺失模式 (MP) 分析

```sas

****************************************************************

缺失模式 (MP) 方法;

****************************************************************

%MP_ASSIGN(MSDATA = ANALALATA, OUTDATA = ANALAL2, VARLIST = &VARLIST,

N_MP_MIN = 100);

PROC MEANS DATA = ANALALATA NOPRINT;

VARLIST;

OUTPUT OUT = MN = XM1-XM16;

BY STUDY;

DATA TEMP;

MERGE ANALALATA MN;

BY STUDY;

RUN;

DATA TEMP;

SET TEMP;

ARRAY X(16) &VARLIST;

ARRAY XM(16) XM1-XM16;

```

第 5 章 带有缺失值的倾向评分 119

```sas

DO I = 1 TO 16;

  IF X(I) = . THEN X(I) = XM(I);

END;

DROP I;

RUN;

PROC SORT DATA = TEMP;

BY MP;

RUN;

PROC LOGISTIC DATA = TEMP NOPRINT;

CLASS BISMORE = &VARLIST;

OUTPUT OUT=PRED PREDICTED=P;

BY MP;

RUN;

DATA PRED;

SET PRED;

IF BISMORE = 0 THEN PROB = P;

IF BISMORE = 1 THEN PROB = 1-P;

W = 1/PROB;

RUN;

PROC SORT DATA=PRED;

BY BISMORE;

RUN;

TITLE '缺失模式 (MP) 方法分析';

PROC MIXED DATA = PRED;

CLASS BISMORE;

MODEL P = BISMORE;

WEIGHT W;

LSMEANS BISMORE/DIFF;

FORMAT BISMORE BINARY.;

RUN;

程序 5.6 输出

缺失模式 (MP) 方法分析

混合过程 (Mixed Procedure)

最小二乘均值 (Least Squares Means)

| 效应 (Effect) | 估计值 (Estimate) | 误差 (Error) | DF | t 值 | Pr >t |
|---|---|---|---|---|---|
| MORE 第 4 年使用双膦酸盐 (BISMORE) | -0.00222 | 0.001021 | 1641 | -2.18 | 0.0295 |
| 使用双膦酸盐 (BISMORE) | 0.007187 | 0.000987 | 1641 | 7.28 | <.0001 |

最小二乘均值的差异 (Differences of Least Squares Means)

| 效应 (Effect) | 估计值 (Estimate) | 误差 (Error) | DF | t 值 | Pr >t |
|---|---|---|---|---|---|
| MORE 第 4 年使用双膦酸盐 (BISMORE) | -0.00941 | 0.001420 | 1641 | -6.63 | <.0001 |

## 5.3.5 多重插补缺失模式 (MIMP) 分析

MIMP 方法本质上是 MI 和 MP 方法的。首先，对缺失值进行多重插补。对于每个插补数据集，使用基线变量和缺失模式分类变量估计倾向评分。与 MP 方法类似，我们合并较小的缺失模式以使每个单元至少包含 100 个观测值。我们创建带有合并模式指标的数据集（见节 5.3.4），只需对该数据集应用 `PROC MI`（见节 5.3.3）。程序 5.7 显示了执行 MIMP 分析的 SAS 代码，程序 5.7 输出结果。

#### 5.7 插补缺失模式 (MIMP) 分析

```sas
****************************************************************
多重插补缺失模式 (MIMP) 方法;
****************************************************************
```

## 135 第 5 章 带有缺失值的倾向评分

## 程序 5.6 输出

均值过程 (MEANS Procedure)

分析变量 (Analysis Variable)：估计值 (Estimate)

分组 (BY Group)

| N | 均值 (Mean) | 标准差 (Std Dev) | 最小值 (Minimum) | 最大值 (Maximum) |
|---|---|---|---|---|
| MORE 第 4 年使用双膦酸盐 (BISMORE) | -0.0021775 | 0.00011208 | -0.002187 | -0.0021596 |
| 使用双膦酸盐 (BISMORE) | 0.0083296 | 0.000190528 | 0.0081254 | 0.008643 |

均值过程 (MEANS Procedure)

分析变量 (Analysis Variable)：估计值 (Estimate)

| N | 均值 (Mean) | 标准差 (Std Dev) | 最小值 (Minimum) | 最大值 (Maximum) |
|---|---|---|---|---|
| 5 | -0.0105070 | 0.000187855 | -0.0108178 | -0.01030396 |

可以使用 `PROC MIANALYZE` 获取治疗差异的点估计值。然而，来自 `PROC MIANALYZE` 的方差估计是无效。这种方法在程序 5.8 中显示，程序 5.8 输出了结果。

## 程序 5.8 使用 PROC MIANALYZE 汇总 MIMP 方法的估计值

```sas
TITLE2 '使用 PROC MIANALYZE 估计治疗差异';
DATA MIMP_EST (KEEP = _IMPUTATION EFFECT RENAME=(EFFECT=PARAMETER));
SET DIFFS;
EFFECT = 'DIFF';
RUN;
```

```sas
DATA FOR_MIMP_COV (KEEP = _IMPUTATION ROWNAME BISMORE DIFF);
SET DIFFS;
DIFF = STDERR**2;
ROWAME = "DIFF"
RUN;
```

```sas
PROC MIANALYZE PARMS=FOR_MIMP_EST COVB=MIMP_COV;
MODEFFECTS DIFF;
ODS OUTPUT PARAMETERIMATES=MI_EST
VARIANCEINFO=MI_VAR
RUN;
```

# 122 使用 SAS 对观察性健康数据进行分析

# 程序 5.8 的输出

使用多重插补缺失模式 (MIMP) 方法的分析结果

使用 PROC MIANALYZE 估计治疗差异

MIANALYZE 过程

```
PARMS Data Set               WORK.FOR_MIMP_EST
COVB Data Set               WORK.FOR_MIMP_COV
Number of Imputations        5
```

多重插补方差信息

| | --方差-- | | | DF |
|---|---|---|---|---|
| 参数 | 组间 | 组内 | 总计 | |
| DIFF | 3.289507E-8 | 0.000020272 | 0.000002115 | 9972.9 |

多重插补参数估计

| | | | | |
|---|---|---|---|---|
| 参数 | 方差相对增加 | 缺失信息比例 | 相对效率 |
| DIFF | in Variance | 0.020436 | 0.020224 | 0.995972 |

多重插补参数估计

| | | | | | |
|---|---|---|---|---|---|
| 参数 | 估计值 | 标准误 | 95% 置信限 | | |
| DIFF | -0.010507 | 0.001454 | -0.01336 | -0.00766 | 9972.9 |
| | | | | | | | |

|---|---|---|---|---|---|---|

| 参数 | 最小值 | 最大值 | Theta0 | 参数=Theta0 | Pr > |t| |
| DIFF | -0.010818 | -0.010310 | 0 | -7.23 | <.0001 |

### 5.3.6 获取 Bootstrap 置信区间
