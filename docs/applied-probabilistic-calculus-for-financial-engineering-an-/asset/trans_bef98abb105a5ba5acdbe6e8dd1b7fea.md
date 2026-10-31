
实现差分进化算法，用于对一个实值参数向量的实值函数进行全局优化。

| 字段 | 值 |
|---|---|
| 版本 | 2.2-4 |
| 依赖 | parallel |
| 建议 | foreach, iterators, colorspace, lattice |
| 发布时间 | 2016-12-19 |
| 作者 | David Ardia [aut], Katharine Mullen [aut, cre], Brian Peterson [aut], Joshua Ulrich [aut], Kris Boudt [ctb] |
| 维护者 | `Katharine Mullen <mullenkate@gmail.com>` |
| 许可证 | GPL-2 \| GPL-3 [由 GPL (≥ 2) 扩展而来] |
| 需要编译 | 是 |
| 引文 | DEoptim 引文信息 |
| 材料 | README NEWS |
| 所属视图 | 优化 |
| CRAN 检查 | DEoptim 结果 |

## 下载：

| 资源 | 详情 |
|---|---|
| 参考手册 | DEoptim.pdf |
| Vignettes | DEoptim：一个用于差分进化的 R 包<br>使用 DEoptim 进行大规模投资组合优化 |
| 包源码 | DEoptim_2.2-4.tar.gz |
| Windows 二进制文件 | r-devel: DEoptim_2.2-4.zip, r-release: DEoptim_2.2-4.zip, r-oldrel: DEoptim_2.2-4.zip |
| OS X Mavericks 二进制文件 | r-release: DEoptim_2.2-4.tgz, r-oldrel: DEoptim_2.2-4.tgz |
| 旧版源码 | DEoptim 存档 |

## 反向依赖：

| 类型 | 包 |
|---|---|
| 反向依赖 | EcoHydRology, galts, IBHM, likeLTD, micEconCES, quicksky, selectMeta |
| 反向导入 | BBEST, CEGO, covmat, DstarM, FuzzyStatProb, MSGARCH, SpaDES |
| 反向建议 | BayesianTools, MSCMT, nanop, npsp, PortfolioAnalytics, RcppDE, SACOBRA, SPOT |

## 来自 CRAN 的示例：

在 R 中使用以下两个示例，以说明上述方法在投资组合优化中的应用：

## DEoptim：差分进化优化

### 说明

通过差分进化算法执行进化式全局优化。

### 用法

```r
DEoptim(fn, lower, upper, control = DEoptim.control(), ..., fnMap=NULL)
```

### 参数

- `fn` 要优化（最小化）的函数。该函数应当将实值参数向量作为其第一个参数，并返回一个标量实数值。不允许出现 NA 和 NaN 值。
- `lower, upper` 两个向量，分别指定每个待优化参数的标量实值下界和上界，因此 `lower` 和 `upper` 的第 i 个元素适用于第 i 个参数。该实现会在 `lower` 和 `upper` 之间搜索 `fn` 的全局最优值（最小值）。
- `control` 一个控制参数列表；详见 `DEoptim.control`。
- `fnMap` 一个可选函数，在每次生成种群之后、将种群传给目标函数之前运行。这样用户就可以施加整数/基数约束。
- `...` 传递给 `fn` 的其他参数。

### 详细说明

`DEoptim` 对 `fn` 执行优化（最小化）。`control` 参数是一个列表；有关详细信息，请参见 `DEoptim.control` 的帮助文件。

`DEoptim` 的 R 实现由 David Ardia 于 2005 年首次发布在 Comprehensive R Archive Network（CRAN）上。早期版本使用纯 R 编写。自 2.0-0 版本（2009 年发布到 CRAN）起，该包通过接口调用 DE 的 C 语言实现，在大多数问题上比纯 R 实现快得多。

需要强调的是，`DEoptim` 的结果是一个随机变量，也就是说，即使使用相同设置反复运行该算法，也可能得到不同结果。因此，如果用户希望复现结果，应设置随机种子，例如在调用 `DEoptim` 之前设置 `set.seed(1234)`。

`DEoptim` 依靠反复评估目标函数来推动种群逼近全局最小值。希望让 `DEoptim` 尽可能快速运行的用户，应考虑以并行模式使用该包（从而利用所有可用 CPU），并确保目标函数的求值尽可能高效（例如在纯 R 代码中使用向量化，或用 C 或 Fortran 等更底层的语言编写目标函数的一部分）。

有关 R 包 `DEoptim` 的更多细节和示例，可参见 Mullen et al. (2011) 以及 Ardia et al. (2011a, 2011b)，也可以通过输入 `vignette("DEoptim")` 查看包的 vignette。此外，一个针对高维非线性投资组合优化问题的包使用示例，可通过输入 `vignette("DEoptimPortfolioOptimization")` 查看。

在出版物中请引用该包。使用 `citation("DEoptim")`。

### 返回值

函数 `DEoptim` 的输出是 S3 类 `DEoptim` 的一个实例。更准确地说，它是一个长度为 2 的列表，包含以下元素：

- `optim`，一个包含以下元素的列表：
  - `bestmem`：找到的最佳参数集合。
  - `bestval`：与 `bestmem` 对应的 `fn` 值。
  - `nfeval`：函数评估次数。
  - `iter`：过程迭代次数。
- `member`，一个包含以下元素的列表：
  - `lower`：下边界。
  - `upper`：上边界。
  - `bestvalit`：每次迭代中 `fn` 的最优值。
  - `bestmemit`：每次迭代中的最佳成员。
  - `pop`：最后一次迭代生成的种群。
  - `storepop`：包含中间种群的列表。

`DEoptim` 类的成员具有一个接受 `plot.type` 参数的 `plot` 方法。`plot.type = "bestmemit"` 会绘制每一代中使目标函数值最低的参数值。`plot.type = "bestvalit"` 会绘制每一代中目标函数的最优值。最后，`plot.type = "storepop"` 会绘制已保存的种群（只有在通过适当设置 `DEoptim()` 的 `control` 参数保存这些种群时才可用）。保存中间种群可以让我们详细检查优化的进展。此外，还提供了一个 `summary` 方法，返回最佳参数向量、目标函数的最优值、优化运行的代数以及目标函数被评估的次数。

### 注意

DE 是由 Storn 和 Price（1997）提出的搜索启发式算法。它作为连续数值最小化问题上的全局优化算法，其卓越性能已被广泛研究。DE 属于遗传算法一类，这类算法利用受生物学启发的交叉、变异和选择操作作用于种群，从而在连续多代中最小化目标函数。与其他进化算法一样，DE 通过变异和选择算子演化候选解种群来求解优化问题。DE 对种群成员采用浮点数编码而不是位串编码，并在变异中使用算术运算而不是逻辑运算。DE 特别适合寻找实值参数的实值函数的全局最优值，并且不要求该函数连续或可微。

设 NP 表示种群中参数向量（成员）x ∈ R^k 的数量。为了创建初始代，需要对参数向量的最优值进行 NP 次猜测，猜测值既可以取自 lower 和 upper 边界（由用户定义）之间的随机值，也可以使用用户提供的值。每一代都需要从当前种群成员中创建一个新种群。这一过程通过种群成员的差分变异完成。首先随机选择种群中的三个成员 x_{r0}、x_{r1} 和 x_{r2}，从而创建初始变异参数向量 v_i。然后按如下方式生成 v_i：

v_i = x_{r0} + F(x_{r1} - x_{r2})

其中 F 是差分权重因子，其有效值通常介于 0 和 1 之间。在首次变异操作之后，变异会继续进行，直到完成 d 次变异，并伴随一个交叉概率 CR ∈ [0, 1]。交叉概率 CR 控制从变异向量复制过来的参数值比例。如果在变异和交叉之后，试验参数向量的某个元素违反边界，则将其重置，以确保满足边界（具体方式因实现而异）。然后计算与子代相关的目标函数值。如果试验向量的目标函数值不高于前一个向量（相等或更低），则它会替换种群中的前一个向量。
