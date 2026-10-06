
消耗一些搜索能量，遗传算法（GA）试图解决的问题始终是 NP 完全问题，即你感兴趣的只是找到一个解决方案，而无论该解决方案是否为最优。

列表 8-16 中的 GA 伪代码展示了简单遗传算法（SGA）是如何运作的。它初始化了一个染色体种群。种群中的每个染色体都是目标函数的潜在解，该函数也是适应度函数。适应度函数返回一个代表解（染色体）质量的值。然后使用选择来过滤掉较差的染色体。被选中的染色体执行交叉和变异操作。在这些这些转换操作后，染色体被放入一个新的种群中并重复该过程。该过程重复若干次，或者直到种群中的最佳染色体接近最优解。适应度函数用于确定染色体距离最优解有多远。

## 列表 8-16 GA 伪代码

```
初始化群体
根据适应度函数计算染色体的适应度值

根据以下规则进化种群 X 次：

步骤1：从种群中选择一个染色体并命名为 c0
步骤2：从种群中选择一个染色体并命名为 c1
步骤3：让 c0 和 c1 进行再生并生成新染色体 c0' 和 c1'
步骤4：将 c0 和 c1 放入新种群
步骤5：从适应度函数计算适应度值

重复步骤1直到新种群大小 = 当前种群大小

当前种群 = 新种群
```

染色体通常表示为整数或浮点数的数组或列表。列表 8-17 中的实现引入了一个额外的层，使得染色体具有基因型类型层和表型类型层。基因型层是实际数据所在的地方。如果你将单个基因型类型数据项作为函数的输入，该函数的结果将表型类型层中的一个数据项。你可以使用函数将基因型类型数据转换为表型，这可以允许你对染色体使用更复杂的编码。初始化每个构建块时需要传入一个用户函数，这被称为*位点*（loci）。变异操作将在后的“交叉与变异”章节中介绍。整个种群的初始化在列表 8-18 中。

## 列表 8-17 染色体定义

```
// 表示参与 GA 的个体的染色体类型
type ChromosomeType(f, size, tconverters)
let initialF = f
let mutable genes = [for in 1..size to yield f()]
let mutable genoPhenConverters = converters
```

```f
/// 制作此染色体的复制副本
member.this.Clone() =
let newValue =
    match converters with
    Some(converters) -> new ChromosomeType(initialF, size, converters)
    | None -> new ChromosomeType(initialF, size)
newValue.Genos <- this.Genos
newValue
```

```f
/// 使用给定的适应度函数获取适应度值
member.this.Fitness(fitnessFunction) = this.Pheno | fitnessFunction
```

```f
/// 获取和设置 Genos 值
member.this.Genos
    with get() = genos
    and set(value) = genos <- value
```

```f
/// 获取和设置 Pheno 值
member.this.Pheno
    with get() =
        match genoPhenoConverters with
        | Some(genoPhenoConverters) -> List.zip genoPhenoConverters genos | List.map
```

```f
(fun
    f,value) -> f value
    | None -> this.Genos
```

```f
/// 使用给定的变异函数变异染色体
member.this.Mutate(?mutationF) =
let location = random.Next(Seq.length this.Genos)
let F =
```

```f
    match mutationF with
    | Some(mutationF) -> mutationF
    | None -> f
let transform i with
    match i with
    | when i = location -> F()
    | -> v
```

```f
this.Genos <- List.map transform this.Genos
```

## 列表 8-18 种群初始化

```f
/// 为 GA 生成种群
let Random populationPhenopopulationSize chromosomeSize =
[for i in 1..populationSize do yield (new
ChromosomeType(f = randomF, size = chromosomeSize))]
```

## 选择

首先，请记住，选择可以挑选次优个体以保持种群的多样性，这是完全没问题的。有两种两种常用的选择技术：

-   **轮盘赌法**（Roulette wheel selection）：想象一个容纳种群中所有个体的轮盘。每个个体根据其适应度值占据空间。适应度越高，个体占据的空间越大。空间越大，个体被选中的概率越大。
-   **排序选择法**（Rank selection）：轮盘赌选择使用适应度值来重新分配空间，而排序选择使用排序列表中的排名来这样做。最差的个体分配到第一个空间，次差的分配到第二个空间，以此此类推。

排序选择法赋予了较差个体更大的权重，并可以加速收敛过程。它将作为示例代码中的默认选择方法，如列表 8-19所示。

列表 8-19 排序选择法

```f
/// 排序选择方法
let RankSelection(population:ChromosomeType list) fitnessFunction=
  let populationSize = Seq.Length
  let r = random() % populationSize
  let randomSelection() =
    let c0 = population[r]
    let c1 = population[r]
    let result = if (c0.Fitness(fitnessFunction) > c1.Fitness(fitnessFunction)) then
    c0

  result.Clone()
Seq.init(populationSize, _ -> randomSelection())
```

## 交叉与变异

有两种典型的组合操作：交叉和变异。这些操作总是作用在个体上的。交叉率和变异率控制它们的执行。交叉需要两个个体，它们交换构建块。表 8-2 显示了简单的交叉。交叉操作定义在列表 8-20 中。

## 表 8-2 交叉操作

| 染色体 | |
| --- | --- |
| 染色体 1 | 0000 0000 0000 0000 |
| 染色体 2 | 1111 1111 1111 1111 |
| 后代 1 | 0000 0000 1111 1111 |
| 后代 2 | 1111 1111 0000 0000 |

```f
// 洗牌交叉
let Shufflerossover(c0:ChromosomeType) (c1:ChromosomeType) =
  let crossover c0 = c1 =
    let isEven = n%2 == 0
    let randomSwitch(x, y) = ifEven (randomF()) then (x, y) else (y, x)
    List.zip(c0 | List.map randomSwitch | List.unzip)
    let (first, second) = crossover (c0.Gens, c1.Gens)
    c0.Gens <- first
    c1.Gens <- second
```

变异只涉及一个个体。变变异是随机改变染色体上的一个块为另一个。表 8-3 显示了单位置变异。

## 表 8-3 变异操作

| 染色体 | |
| --- | --- |
| 染色体 | 0000 0000 0000 0000 |
| 变异后的染色体 | 1000 0000 0000 0000 |

交叉被认为没有引入多样性，这意味着交叉没有引入新的数字。个体中的构建块只是从一个个体移动到另一个个体。相反，变异被认为是向种群中引入多样性的方法。根据进化策略设置，交叉率通常设置为较高的值，例如 90%，而变异率低至 2%。这与现实世界的数字一致。

## 精优保留

大自然并不总是青睐优秀的个体。组合操作在大多数情况下通过破坏父母来产生新个体。即使每次都选择最好的个体，它仍然可能被破坏，导致下一代质量下降。大多数遗传算法实现都加入了精优保留的概念，以保留最佳个体并允许它们在不受组合操作干扰的情况下进入代。本节默认使用精优保留。完整的 GA 代码在列表 8-21 中，列表 8-22 显示了如何使用 GA 寻找公式 $f(x_1, x_2...x_{10})=\sum_{i=1}^{10}x_i$ 的最大值，其中 $x_i\in[0,9]$。

