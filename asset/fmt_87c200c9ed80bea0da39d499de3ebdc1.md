
$= max \left( 0, -N \log \left( 1 - \frac{A}{N} \right) - N \log \left( 1 - \frac{B}{N} \right) - N \left( 1 - \frac{A \cup B}{N} \right) \right)$

这两个基数结合位字符串字符，就足够相对于相应的非哈希指纹计算哈希指纹的许多相似性度量（例如 Tanimoto）。

## 4.4.2.3 圣痕算法 (Stigmata)

Sheemetulksk 等人 [46] 的 Stigmata 算法使用哈希指纹（原始工作中使用 daylight）来生成一种名为*分子指纹*的共识指纹，该指纹表示一组针对特定靶点的活性分子的共同点。分子指纹的长度与化合物集合的分子指纹相同（例如，Sheemetulsk 等人原始出版物中为 2048 位），如果某位出现在特定百分比的化合物指纹中，则被置为 TRUE。分子指纹可以用于提取有关指纹模式的信息以及新的描述符。每个分子的每个原子都可以被所谓的 *ALAB* 值标记，该值表示该原子所属的路径中也包含在分子指纹中的路径百分比。

分子层上的类似描述符是 MODP，定义为分子中也是分子指纹部分的路径百分比。分子指纹与分子指纹之间的 Tanimoto 相似性也可以作为分子描述符。在 Sheemetulsk [46] 的论文中，这种描述符被称为 MSIM。

# 分子描述符 109

## 4.4.2.4 Fingal

Brown 等人 [44] 发表的指纹算法 (FinAI) 是基于路径的哈希指纹的扩展，将几何信息整合到路径中。这是通过对路径中使用的原子类型进行调整实现的。路径上的每个原子类型都扩展了其与路径之前原子的几何距离。这些距离被分箱为 10 个距离类别，因为对于关于相同子结构（路径）数量的分子比较，两条路径的距离完全相同是不可能的。在原始出版物中，分箱的边界为 [2.35, 2.71, 3.69, 4.47, 5.25, 6.39, 7.59, 9.32, 12.44]。这使得对分子的区分能力更好，但引入了由构象引起的偏差。在原始工作中，3D 结构通过 CORINA [47] 计算。

## 4.4.3 哈希 (HASHING)

哈希是指将空间 $\chi$ 中的元素映射到一个整数（通常限制在特定范围内）。该映射使用确定性哈希函数 $h : \chi \to Z$ 进行。映射函数是单射的，这意味着当两个输入相等时，它们的哈希值才相等。尽管这是一个优良属性，但大多数哈希函数不是单射的，因为输入空间大于它映射到的整数。

许多算法在数据对象的位表示上工作。每个对象被视为位流，随后（大部分分块地）哈希到其他集合中。

## 4.4.3.1 循环冗余校验

Peterson 和 Brown [48] 发表的循环冗余校验 (CRC) 是一个将位输入序列映射到特定范围内整数（其二进制表示）的函数。其核心思想是定义一个生成多项式 $p(x) = \sum_{i=0}^k c_ix^i$，其系数 $c_i \in \{0,1\}$ 且次数为 $k$，它可以表示为具有 $k+1$ 位的位序列 $b$，使得 $b_i = c_i$。类似于，输入序列被划分为长度为 $k+1$ 的重叠块，并在必要时用零扩展。哈希值通过输入序列对生成多项式进行分块模 2 多项式除法得到。常用的生成多项式为 CRC – 32 = $x^{32} + x^{26} + x^{23} + x^{22} + x^6 + x^{12} + x^{11} + x^0 x^8 + x^7 + x^5 + x^4 + x^2 + x^1 + x^0$ 和 CRC – 16 = $x^{16} + x^{12} + x^5 + x^0$。算法的轮廓见算法 4.7。

# 算法 4.7 CRC 哈希函数的伪代码（改编自维基百科）

```
method getCRCValue(InputSet B, GeneratorBitSet G)

ShiftingRegister R := {00000....} // 初始化

while B is not finished do

```

110

化学信息学算法手册

```
b = nextBit(B)

R.shiftLeft () // 在右侧附加零

if b != leftmostBit(R) do

    R = R ⊊ G

end

return R.AsInteger()

}
```

## 4.4.3.2 InChI Key

InChI Key [49] 是分子 InChI 编码的压缩字符串表示。InChI 被分为若干块，使用 SHA-256 哈希函数 [50] 进行哈希。生成的哈希值表示为字符串并拼接，形成最终的 InChI Key。

AAAAAAAAAAAA – BBBBBBCD

第一块 A 是分子拓扑（“骨架”）到大写字母的编码。这是通过使用截断的 SHA-256 哈希函数实现的。第二块 B 表示剩余层（即质子位置、立体化学、异构体和连接层）。此外，两个字符被标记。标记 C 编码 InChI 版本号、固定层存在、立体化学和同位素信息。最后一个位置 D 是前三个块的校验和，验证 key 的完整性。

## 4.5 药效团场、高阶特征 (3D, 4D, 形状)

## 4.5.1 分子形状 (MOLECULAR SHAPE)

在计算机模拟比较和 QSAR 建模中考虑分子几何结构的基本方法之一是返回结构的形状。分子指纹可以用于提取指纹模式的信息以及新的描述符。每个分子的每个原子都可以被所谓的 *ALAB* 值标记，该值表示该原子所属的路径中也包含在分子指纹中的路径百分比。

分子层上的类似描述符是 MODP，定义为分子中也是分子指纹部分的路径百分比。分子指纹与分子指纹之间的 Tanimoto 相似性也可以作为分子描述符。在 Sheemetulsk [46] 的论文中，这种描述符被称为 MSIM。

## 4.5.1.1 分子形状

两个分子的重叠体积 (MSA) 可以以下公式估计：

```
$A_* \cup B_* \approx min \left[ -N \left( 1 - \frac{A \cup B}{N} \right), -N \log \left( 1 - \frac{A}{N} \right) \left( 1 - \frac{B}{N} \right) \right]$
```

```
$A_* \cap B_* \approx max[0, A_* + B_* - A_* \cup B_*]$,
```

```
$= max \left( 0, -N \log \left( 1 - \frac{A}{N} \right) - N \log \left( 1 - \frac{B}{N} \right) - N \left( 1 - \frac{A \cup B}{N} \right) \right)$
```

## 4.5.1.2 ROCS——化学结构的快速叠层 (Rapid Overlay of Chemical Structures)

ROCS [52] 最初不是作为分子描述符开发的，而是用于虚拟筛选的结构相似性测量。然而，MSA 中使用共同参考分子的技术也适用于 ROCS 相似性。ROCS 方法在利用重叠体积作为相似性的定量测量方面与 MSA 相似，可以被视为后者想法的扩展。

# 化学信息学算法手册

在 ROCS 方法中，特征体积通过一个定义的 3D 高斯形状来近似：

$$\chi(\mathbf{r}) = 1 - \prod_{i=1}^{N} (1 - p_i e^{-\gamma r^2})$$

其中，原子的实际范德华半径 $R$ 可以通过关系 $\gamma = \pi(3p/4\pi R^3)^{2/3}$ 引入。其优点是分子之间的相交部分可以表示为它们特征体积函数的乘积。因此，它将重叠体积的计算简化为对 3D 网格进行积分（即累加）。因此，两个分子 $A$ 和 $B$ 的重叠体积可以表示为：

$$O_{AB} = \int \int \chi_A(\mathbf{r})\chi_B(\mathbf{r})d\mathbf{r}$$

该量可以被视为两组特征的交集，因此可以结合 Tanimoto 系数等其他相似性度量中。在离散特征体积函数的情况下，它可以被视为一种特殊的指纹，其中每个位对应网格集中的一点，如果点在分子内部则置为 1，否则置为 0。这允许将重叠体积定义为位向量的交集，或者定义为点积。

## 4.5.1.3 形状片段 (Shapelets)

MSA [51] 和 ROCS [52] 方法通过分子体积描述分子形状。另一种表示方法是 Shapelet [54] 概念，它使用表面模式编码分子形状。第一步是使用如 ROCS 方法中的分子结构高斯建模来计算位阻空间等值面。分子通过一个 3D 函数编码：

$$M(\mathbf{x}) = \sum_{i=1}^{N} e^{-2(\mathbf{x}-\mathbf{c}_i)^2/r_i^2}$$

这可以看作是高斯函数的叠加，对于每个位于位置 $\mathbf{c} \in \mathbb{R}^3$、半径为 $r$ 的原子 $i$。与 ROCS一样，该函数为空间网格中的每个点 $\mathbf{x}$ 分配一个值，当点在分子内部时，该值为正。$M(\mathbf{x})$ 对应于 ROCS 中使用的特征体积函数 $\chi$，尽管它使用了不同的数学表达式。该结构的等值面可以使用快速立方体算法 [55] 构建。该方法生成一组表面点，这组点通过使用顶点法 [56] 进行简化。

表面模式，即*形状片段 (shapelets)*，通过使用双曲抛面对表面曲率进行局部近似来提取。分子形状被结构化为表面斑丁，这些斑丁由其中心点 $p_i$ 和半径 $r_i$（默认 $r_i=2.5$ $\AA$）定义。然后，一个斑丁被视为中心点 $\mathbf{P}_i$ 周围半径 $r_i$ 内的表面点集 $P_i$。表面的局部形状随后通过沿切平面内两个垂直向量 $\mathbf{e}_u, \mathbf{e}_v \in \mathbb{R}^3$ 沿的曲率来描述。这两个曲率加上 $P_r$ 中的法向量对应于一个抛物面，该抛物面可以被视为局部表面模式。

表面的形状可以使用 Hessian 矩阵 **H** 参数化为 $p(u, v, \mathbf{H}) = (u_{11} + v_{21})u + (u_{12} + v_{22})v$，其中 $u, v \in \mathbb{R}$ 是在 $e_u, e_v$ 坐标系中的坐标。Hessian 的系数 $h_{ij}$ 通过最小化均方根误差 $E(\mathbf{H}) = \sum|n_i - p(u, v, \mathbf{H})|^2$ 得到，这些是 3D 空间中点的坐标 $n_i, u, v$。所得 Hessian 特征值对应两个局部表面曲率 $k_1$ 和 $k_2$。

这些被用于定义每个表面斑丁中心 $P_r$ 的*形状索引* $SI(P_r) = \arctan(k_1 + k_2/k_1 - k_2)$。该过程对于不属于任何斑丁（即已被另一个形状片段近似）的每个表面点重复进行。算法的概述见算法 4。

# 算法 4.8 形状片段提取伪代码

```
method getShapeletForMolecule(Molecule T) {

  surface = getSurfaceMolecule(T)

  for all points in surface do

    S = getShapeletAt(point)

    e = getRMSEOf(S)

    set = sortedPointsAccordingToRMSE(e)

    point = getBest(set)

    shapelets = null

    while set has points do

      shapelets.add(ShapeletOf(point))

      set.remove(point)

    // 每个表面点最多属于一个形状片段的一部分

    set.removeAllPointsInPatch(point)

    point = getBest(set)

  od

  return shapelets

}

method getShapeletAt(p_r) {

  e_n = normalVectorFor(p_r)

  p = getPointInSurfacePatchOf(p_r)

  e_u = \frac{p - p_r}{\|p - p_r\|}

  e_v = \mathbf{e}_n \times \mathbf{e}_u

  points = getLocal2DGridFor(e_u, e_v)

  H = minimizeRMSEOnGrid(points)

  k_1 = getFirstEigenvalue(H)

  k_2 = getSecondEigenvalue(H)

  SI = getShapeIndex($k_1,k_2$)

  return new Shapelet($P_r,k_1,k_2,SI)

}
```

在某些方面，形状片段可以被视为一种特殊的子结构，然而，如果将其用于 QSAR 建模或虚拟筛选，它会面临相似的缺点。每个形状片段都有复杂的数值参数化，因此两个形状片段不太可能以相同的方式参数化。因此，两个分子子结构集的交集具有相似性度量的共同基础，无法直接计算。在原始工作 [54] 中，这个问题通过定义一种算法得到了解决，该算法使用两个形状片段之间的相似性度量，并结合了用于大分子模式检测的团检测方法。这种基于两个分子形状片段最优叠加的刚性结构最小二乘对齐是基于形状片段的 [57]。因此简化了两个分子 $A$ 和 $B$ 的重叠体积。

## 4.5.2. 基于 MIF 的特征

基于场的特征通过对受体进行建模来描述配体。MIF 场通过在分子周围的网格点计算相互作用。$E_{steric}$ 位于空间网格点上考虑了分子的相互作用势。$E_{electro}$ 同样在网格点上计算。在 MIF 中，探针被放置在网格点。分子的相互作用势由空间斥和静电部分组成。然而，也可以包含熵项 [58]。

介电常数 $\xi$ 和 $\varepsilon$ 被视为常数并由边界分开。基于 $s_p$ 和 $s_q$ 描述分子的电荷。电荷通过标准库仑展开得到 [60,61]：

$$E_{cd}(d,p,q) = \left( \frac{pq}{\xi \cdot d} + \frac{(\xi - \varepsilon)}{\xi+\varepsilon}\right)$$

氢键贡献通过改进的 6,4-范华势计算：

$$E_{bb}(d,\theta) = \left( \frac{C}{d^6} - \frac{D}{d^3} \right) \cos^m\theta$$

以包含受体原子提供氢键受体的角度 $\theta$。如果探针是供体，则余弦被设置为零，因为预计探针是经过旋转的。余弦通常被取次方，但 $m$ 也有其他可能的值。算法 4.9 概述了单个网格点的相互作用势的计算，因此一个基于 MIF 的描述符。

# 算法 4.9 单个网格相互作用点的伪代码

```
method getEmpiricalEnergy(Molecule T, Probe P) {

  $E_{steric} = 0$

  for all atoms in T do

    if distance(atom, P) < s then //

      s := steric_distance_threshold e.g. $8\{\AA\}$

      $E_{steric} += E_{lj}$ (distance(atom, P))

    fi

  od

  $E_{electro} = 0$

  for all atoms in T do

    $E_{electro} += E_{cd}$ (distance(atom, P), charge (P), charge (atom))

  od

  $E_{h-bond} = 0$

  for all atoms in T do

    theta = getAngle(P, atom)

    $E_{h-bond} += E_{bb}(d,theta)

  od

  return $E_{steric} + E_{electro} + E_{h-bond}$

}
```

# 化学信息学算法手册

```python
if theta < 90

    continue

fi

if P is a H-bond donor then

    theta = 0

fi

H-bond += Ehb (distance(atom,P),theta)

od

    return Esteric + EElectro + Eh-bond

}
```
