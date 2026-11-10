
### 实用函数

| | |
|---|---|
| `calcgx` | 将权重和偏置的性能梯度计算为单个向量 |
| `calcjejj` | 计算雅可比性能向量 |
| `calcjx` | 将权重和偏置的性能雅可比计算为单个矩阵 |
| `calcpd` | 计算延迟的网络输入 |
| `calcperf` | 计算网络输出、信号和性能 |
| `getx` | 将所有网络权重和偏置值作为单个向量获取 |
| `setx` | 使用单个向量设置所有网络权重和偏置值 |

### 向量函数

| | |
|---|---|
| `combvec` | 创建向量的所有组合 |
| `con2seq` | 将并发向量转换为顺序向量 |
| `concur` | 创建并发偏置向量 |
| `ind2vec` | 将索引转换为向量 |
| `minmax` | 矩阵行的范围 |
| `normc` | 归一化矩阵的列 |
| `normr` | 归一化矩阵的行 |
| `pnormc` | 伪归一化矩阵的列 |
| `quant` | 将值离散化为数量的倍数 |
| `seq2con` | 将顺序向量转换为并发向量 |
| `vec2ind` | 将向量转换为索引 |

### 权重和偏置初始化函数

| | |
|---|---|
| `initcon` | conscience 偏置初始化函数 |
| `initsompc` | 使用主成分初始化 SOM 权重 |
| `initzero` | 零权重和偏置初始化函数 |
| `midpoint` | 中点权重初始化函数 |
| `randnc` | 归一化列权重初始化函数 |
| `randnr` | 归一化行权重初始化函数 |
| `rands` | 对称随机权重/偏置初始化函数 |
| `revert` | 将网络权重和偏置更改为先前的初始化值 |

## C.5 GPLAB——MATLAB 的遗传编程工具箱

GPLAB 是用于 MATLAB 的遗传编程工具箱。其大多数函数都作为“即插即用”设备使用，因此只要用户具备最少的 MATLAB 编程环境知识，它就是一个通用且易于扩展的工具。

GPLAB 的一些特性包括：

- 3 种树初始化模式（Full、Grow、Ramped Half-and-Half）+ 这些模式的 3 种变体
- 若干用于构建树的预置函数和终端
- 对树深度或大小的动态限制（可选）
- 资源受限的 GP（可变规模种群）（可选）
- 动态种群（可变规模种群）（可选）
- 4 种遗传算子（交叉、变异、交换变异、收缩变异）
- 可配置的算子概率自动适应（可选）
- 稳态 + 世代 + 批处理模式，且它们之间具有模糊边界
- 5 种采样方法（轮盘赌、SUS、锦标赛、字典序简约压力锦标赛、双重锦标赛）
- 3 种计算预期后代数量的模式（绝对值 + 2 种排名方法）
- 2 种读取输入文件和计算适应度的方法（符号回归和奇偶校验问题 + 人工蚂蚁问题）
- 对运行中最佳个体进行运行时交叉验证（可选）
- 通过任一个体进行离线交叉验证或结果预测（可选）
- 4 级精英保留
- 可配置的停止条件
- 将结果保存到文件（5 种频率模式，可选）
- 3 种运行时文本输出模式
- 运行时图形输出（4 种图，可选）
- 离线图形输出（5 个函数，可选）
- 运行时种群多样性测量（2 种度量，可选）
- 运行时测量平均树层级、节点数、内含子数和树填充率（可选）
- 4 个演示函数（符号回归、奇偶校验、人工蚂蚁、多路复用器）

无论这个列表有多长，GPLAB 最大的特点始终是“即插即用”理念。用户构建的任何替代（或集合）函数都会被该工具箱直接接受，只要它符合与所涉模块相关的规则。此外，函数与参数之间不存在不兼容性，这意味着用户可以使用它们的任意组合，即使用户使用的是自己的函数也是如此。

GPLAB 未实现：

- 多个子种群
- 自动定义函数

### 遗传编程工具箱的函数

GPLAB 工具箱提供的超过一百个函数可分为若干不同的功能组。以下是每个组中包含的函数列表。同一个函数可能列在多个组中。

### 演示函数

| | |
|---|---|
| `demo` | DEMO 运行一个符号回归问题 |
| `demoparity` | DEMO 运行一个奇偶校验-3 问题 |
| `demoant` | DEMO 运行一个蚂蚁 |

### 运行算法与测试结果

| | |
|---|---|
| `gplab` | 运行 GPLAB 遗传编程算法 |
| `testind` | 在不同的数据集上评估一个 GPLAB 个体 |

### 参数和状态设置

| | |
|---|---|
| `setparams` | 设置 GPLAB 算法的参数变量 |
| `resetparams` | 重置 GPLAB 算法的参数变量 |
| `resetstate` | 重置 GPLAB 算法的状态变量 |
| `setoperators` | 将算子信息存储为 GPLAB 算法的参数 |
| `addoperators` | 将附加算子信息存储为 GPLAB 的参数 |
| `setfunctions` | 将函数信息存储为 GPLAB 算法的参数 |
| `addfunctions` | 将附加函数信息存储为 GPLAB 的参数 |
| `setterminals` | 将终端信息存储为 GPLAB 算法的参数 |
| `addterminals` | 将附加终端信息存储为 GPLAB 的参数 |

### 自动变量检查

| | |
|---|---|
| `checkvarsparams` | 初始化 GPLAB 算法参数变量 |
| `checkvarsstate` | 初始化 GPLAB 算法状态变量 |
| `checkvarsdata` | 为 GPLAB 算法填充数据集变量 |

### 参数和状态变量的描述

| | |
|---|---|
| `availableparams` | 描述 GPLAB 算法参数变量 |
| `availablestate` | 描述 GPLAB 算法状态变量 |

### 创建新一代

| | |
|---|---|
| `genpop` | 为 GPLAB 算法创建初始代 |
| `generation` | 为 GPLAB 算法创建新一代 |
| `pickoperator` | 抽取一个要在 GPLAB 算法中应用的遗传算子 |
| `applyoperator` | 应用遗传算子以创建新的 GPLAB 个体 |
| `pickparents` | 从池中为 GPLAB 遗传算子挑选父代 |
| `applysurvival` | 为 GPLAB 算法选择新一代个体 |
| `updatestate` | 更新 GPLAB 算法状态变量 |
| `stopcondition` | 检查 GPLAB 算法满足哪个停止条件 |

### 创建新个体

| | |
|---|---|
| `initpop` | 为 GPLAB 算法创建新种群 |
| `fullinit` | 使用 full 方法创建新的 GPLAB 种群 |
| `growinit` | 使用 grow 方法创建新的 GPLAB 种群 |
| `rampedinit` | 使用 ramped half-and-half 方法创建新的 GPLAB 种群 |
| `newind` | 为 GPLAB 算法创建新个体 |
| `maketree` | 为 GPLAB 算法创建表示树 |

### 过滤新个体

| | |
|---|---|
| `validateinds` | 对新 GPLAB 个体应用验证过程 |
| `strictdepth` | 对新 GPLAB 个体应用严格深度过滤器 |
| `strictnodes` | 对新 GPLAB 个体应用严格大小过滤器 |
| `dyndepth` | 对新 GPLAB 个体应用动态深度过滤器 |
| `dynnodes` | 对新 GPLAB 个体应用动态大小过滤器 |
| `heavydyndepth` | 对新 GPLAB 个体应用重度动态深度过滤器 |
| `heavydynnodes` | 对新 GPLAB 个体应用重度动态大小过滤器 |

### 受保护函数与逻辑函数

| | |
|---|---|
| `mydivid` | MYDIVIDE(X1,X2) 如果 X2==0 则返回 X1，否则返回 X1/X2 |
| `mylog` | MYLOG(X) 如果 X=0 则返回零，否则返回 LOG(ABS(X)) |
| `mylog2` | MYLOG2(X) 如果 X=0 则返回零，否则返回 LOG2(ABS(X)) |
| `mylog10` | MYLOG10(X) 如果 X=0 则返回零，否则返回 LOG10(ABS(X)) |
| `mysqrt` | MYSQRT(X) 如果 X=0 则返回零，否则返回 SQRT(X) |
| `mypower` | MYPOWER(X1,X2) 如果 X1^X2 为 Inf，或具有虚部，则返回 0，否则返回 X1^X2 |
| `myif` | 计算 IF-THEN-ELSE 语句的结果 |
| `kozadivide` | KOZADIVIDE(X1,X2) 如果 X2==0 则返回 1，否则返回 X1/X2 |
| `kozasqrt` | KOZASQRT(X) 返回 SQRT(ABS(X)) |
| `nand` | NAND(X1,X2) 返回 NOT(AND(X1,X2)) |
| `nor` | NOR(X1,X2) 返回 NOT(OR(X1,X2)) |

### 人工蚂蚁函数

| | |
|---|---|
| `demoant` | GPLAB 工具箱的演示函数 |
| `antmove` | 将 GPLAB 人工蚂蚁向前移动一步 |
| `antleft` | 将 GPLAB 人工蚂蚁向左转 |
| `antright` | 将 GPLAB 人工蚂蚁向右转 |
| `antprogn2` | 执行 GPLAB 人工蚂蚁的两个动作 |
| `antprogn3` | 执行 GPLAB 人工蚂蚁的三个动作 |
| `antif` | 执行 GPLAB 人工蚂蚁的其中一个动作 |
| `antfoodahead` | 测试 GPLAB 人工蚂蚁前方是否有食物 |
| `antnewpos` | 计算 GPLAB 人工蚂蚁的新位置 |
| `anteval` | 评估 GPLAB 人工蚂蚁的树 |
| `antfitness` | 测量 GPLAB 人工蚂蚁的适应度 |
| `antfitness_lib` | 测量 GPLAB 人工蚂蚁的适应度，值越低越好 |
| `antrail` | 将矩阵解释为 GPLAB 人工蚂蚁的食物轨迹 |
| `antsim` | 模拟最佳 GPLAB 人工蚂蚁的行为 |
| `antpath` | 存储 GPLAB 人工蚂蚁所走的路径 |

