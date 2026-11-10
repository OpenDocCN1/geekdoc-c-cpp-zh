

```python
(0.785398167726482..., 9.04272522456719...e-07)
sage: N(pi/4)
0.785398163397448
sage: N(QuadNC(lambda x: sqrt(1-x^2), 0, 1, 20))
0.784586419900198
```

我们注意到，结果的精度取决于所使用的点数：

```python
sage: [N(QuadNC(lambda x: x * log(1+x), 0, 1, n) - 1)
....:  for n in [2, 8, 16]]
[0.0965735902799726, 1.17408932933522e-7, 2.1344905010566e-13]
sage: [N(QuadNC(lambda x: sqrt(1-x^2), 0, 1, n) - pi/4)
....:  for n in [2, 8, 16]]
[-0.285398163397448, -0.0052456673640445, -0.00125482109302663]
```

要在 Sage 中的不同数值积分方法与我们的方法 QuadNC 之间进行更有趣的比较，需要将其变成自适应方法。自适应方法会自动细分积分区间，就像 numerical_integral 所做的那样。

## A.15 枚举与组合数学

### 练习 50 第 330 页。（抽到四条的概率）

让我们构建四条牌型的集合：

```python
sage: Suits = FiniteEnumeratedSet(
....:     ["Hearts", "Diamonds", "Spades", "Clubs"])
sage: Values = FiniteEnumeratedSet([2, 3, 4, 5, 6, 7, 8, 9, 10,
....:     "Jack", "Queen", "King", "Ace"])
sage: FourOfAKind = cartesian_product((Arrangements(Values,2), Suits))
```

我们使用了 FiniteEnumeratedSet 而不是 Set，以便指定花色和点数的顺序，从而指定四条牌型的顺序：

```python
sage: FourOfAKind.list()
[((2, 3), 'Hearts'),
 ((2, 3), 'Diamonds'),
 ...
 (('Ace', 'King'), 'Clubs')]
```

上面的列表以“2 的四条配红桃 3”开始，以“A 的四条配梅花 K”结束。总共有 624 手四条：

```python
sage: FourOfAKind.cardinality()
624
```

相对于手牌总数，随机抽取一手牌时，抽到四条的概率为 1/4165：

```python
sage: Cards = cartesian_product([Values, Suits])
sage: Hands = Subsets(Cards, 5)
sage: FourOfAKind.cardinality() / Hands.cardinality()
1/4165
```

### 练习 51 第 330 页。（*抽到同花和同花顺的概率*）

要选择一手同花顺，我们必须选择其最小的牌（介于 1 和 10 之间）及其花色。因此共有 40 手同花顺。

```python
sage: StraightFlush = cartesian_product([range(1, 11), Suits])
sage: StraightFlush.cardinality()
40
```

因此还剩 5108 手（非顺子）同花：

```python
sage: AllFlush = cartesian_product([Subsets(Values,5),Suits])
sage: AllFlush.cardinality() - StraightFlush.cardinality()
5108
```

最后，随机抽取一手牌得到同花的概率约为 2/1000：

```python
sage: _ / Hands.cardinality()
1277/649740
sage: float(_)
0.001965401545233478
```

如果能在集合上执行上述计算——而不是处理基数——通过显式地把同花集合构建为 AllFlush 与 StraightFlush 的差集，那会更好。然而，没有高效的通用算法来计算两个集合的差集 `A \setminus B`：在没有任何额外信息的情况下，我们能做的最好的事情就是扫描 A 的所有元素，并检查它们是否在 B 中。在上面的计算中，我们利用了 B 包含于 A 这一事实，而 Sage 无法*先验地*猜到这一点。另一个困难虽然更容易处理，即 A 和 B 的元素应当以相同方式表示。

### 练习 52 第 330 页。

这里我们只处理葫芦（full hand）的情形，即由三条和一个对子组成。我们先写一个检查是否为葫芦（full hand）的函数。为了写得更简短，我们使用下面的方法，它允许我们统计一个单词中字母的重复次数：

```python
sage: Word(['a','b','b','a','a','b','a']).evaluation_dict()
{'a': 4, 'b': 3}
```

```python
sage: def is_full_hand(hand):
....:     suits = Word([value for (value, suit) in hand])
....:     repetitions = sorted(suits.evaluation_dict().values())
....:     return repetitions == [2,3]
sage: is_full_hand((('5', 'Diamonds'), ('6', 'Diamonds'), ('6', 'Hearts'),
....:                ('5', 'Spades'), ('1', 'Spades')))
False
```

```python
sage: is_full_hand({(3, 'Clubs'), (3, 'Spades'), (3, 'Hearts'),
....:              (2, 'Clubs'), (2, 'Spades')})
True
```

现在，我们通过实验估计葫芦（full hand）的比例。更一般地，下面的函数估计有限集合 $S$ 中满足谓词 predicate 的元素比例。它假定该集合具有均匀分布的 `random_element` 方法。

```python
sage: def estimate_proportion(S, predicate, n):
....:     count = 0
....:     for i in range(n):
....:         if predicate(S.random_element()):
....:             count += 1
....:     return count/n
```

```python
sage: float(estimate_proportion(Hands, is_full_hand, 10000))
0.0014
```

现在让我们符号化地进行计算。要确定一手葫芦（full hand），我们必须选择一对不同的点数，其中一个用于三条，一个用于对子，并为三条选择一个由三个花色组成的集合，为对子选择两个花色组成的集合：

```python
sage: FullHands = cartesian_product([Arrangements(Values, 2),
....:     Subsets(Suits, 3), Subsets(Suits, 2)])
```

例如，下面是一手葫芦（full hand），其中三条是 2，对子是 3：

```python
sage: FullHands.first()
([2, 3], {'Hearts', 'Spades', 'Diamonds'}, {'Hearts', 'Diamonds'})
```

抽到葫芦（full hand）的概率为：

```python
sage: float(FullHands.cardinality() / Hands.cardinality())
0.0014405762304921968
```

### 练习 53 第 330 页。（*手工计数完全二叉树*）

有一棵含一个叶子的完全二叉树，以及一棵含两个叶子的完全二叉树。对于 $n = 3, 4$ 和 $5$ 个叶子，我们分别得到 $2$、$5$ 和 $14$ 棵树（对于 $n = 4$，见图 15.1）。

### 练习 54 第 340 页。

$n$ 的 $k$ 部分 composition 与 $\{1, \ldots, n - 1\}$ 的大小为 $k - 1$ 的子集一一对应：对于集合 $\{i_1, i_2, \ldots, i_{k-1}\}$，其中 $0 < i_1 < i_2 < \cdots < i_{k-1} < n$，我们关联 composition $(i_1, i_2 - i_1, \ldots, i_{k-1} - i_{k-2}, n - i_{k-1})$，反之亦然。由此得到枚举公式：$n$ 有 $2^{n-1}$ 个 composition，其中具有 $k$ 个部分的 composition 有 $\binom{n-1}{k-1}$ 个。

```python
sage: n=6
sage: Compositions(n).cardinality(); 2^(n-1)
32
32
sage: n=6; k=3
sage: Compositions(n, length=k).cardinality(); binomial(n-1, k-1)
10
10
```

为了回头确认是否使用了这些公式，我们可以查看 cardinality 命令的代码：

```python
sage: C = Compositions(n)
sage: C.cardinality??
```

在下面的第二种情形中，内部使用的方法名，即 `_cardinality_from_iterator`，给出了答案：基数是通过遍历所有 composition 来计算的——而且效率不高。

```python
sage: C = Compositions(5,length=3)
sage: C.cardinality
<bound method IntegerListsLex...._cardinality_from_iterator ...>
```

### 练习 55 第 343 页。

一些例子：

```python
sage: IntegerVectors(5,3).list()
[[5, 0, 0], [4, 1, 0], [4, 0, 1], [3, 2, 0], [3, 1, 1], [3, 0, 2],
...
[0, 4, 1], [0, 3, 2], [0, 2, 3], [0, 1, 4], [0, 0, 5]]
```

```python
sage: OrderedSetPartitions(3).cardinality()
13
sage: OrderedSetPartitions(3).list()
[[{1}, {2}, {3}], [{1}, {3}, {2}], [{2}, {1}, {3}], [{3}, {1}, {2}],
...
[{1, 2}, {3}], [{1, 3}, {2}], [{2, 3}, {1}], [{1, 2, 3}]]
sage: OrderedSetPartitions(3,2).random_element()
[{1, 3}, {2}]
```

```python
sage: StandardTableaux([3,2]).cardinality()
5
sage: StandardTableaux([3,2]).an_element()
[[1, 3, 5], [2, 4]]
```

### 练习 56 第 343 页。

对于较小的尺寸，我们得到置换矩阵：

```python
sage: list(AlternatingSignMatrices(1))
[[1]]
sage: list(AlternatingSignMatrices(2))
[
[1 0]  [0 1]
[0 1], [1 0]
]
```

第一个负号出现在 $n = 3$ 时：

```python
sage: list(AlternatingSignMatrices(3))
[
[1 0 0] [0 1 0] [1 0 0] [ 0 1 0] [0 0 1] [0 1 0] [0 0 1]
[0 1 0] [1 0 0] [0 0 1] [ 1 -1 1] [1 0 0] [0 0 1] [0 1 0]
[0 0 1], [0 0 1], [0 1 0], [ 0 1 0], [0 1 0], [1 0 0], [1 0 0]
]
```

通过观察更大 n 的例子，我们可以看出，该集合由所有系数在 {−1, 0, 1} 中的矩阵组成，使得在每一行和每一列上，非零系数在 1 和 −1 之间交替，并以 1 开始和结束。

### 练习 57 第 343 页。

在 (Z/2Z)^5 中有 2^5 个向量：

```python
sage: GF(2)^5
Vector space of dimension 5 over Finite Field of size 2
sage: _.cardinality()
32
```

要构造一个系数在 Z/2Z 中的可逆 3 × 3 矩阵，只需选择一个非零行向量（2^3 − 1 种选择），然后选择一个与第一个向量线性无关的第二个向量（2^3 − 2 种选择），再选择一个与前两个向量都线性无关的第三个向量（2^3 − 2^2 种选择）。这给出：

```python
sage: (2^3-2^0)*(2^3-2^1)*(2^3-2^2)
168
```

确实：

```python
sage: GL(3,2)
General Linear Group of degree 3 over Finite Field of size 2
sage: _.cardinality()
168
```

同样的推理给出一般公式，它自然用 q-阶乘表示：

$$\prod_{k=0}^{n-1}(q^n-q^k)=q^{n(n-1)/2}(q-1)^n[n]_q!$$

因此：

```python
sage: from sage.combinat.q_analogues import q_factorial
sage: q = 2; n = 3
sage: q^(n*(n-1)/2) * (q-1)^n * q_factorial(n,q)
168
sage: q = 3; n = 5
sage: GL(n, q).cardinality()
475566474240
sage: q^(n*(n-1)/2) * (q-1)^n * q_factorial(n,q)
475566474240
```

### 练习 58 第 346 页。

在第一种情形中，Python 先构建所有结果的列表，然后将其传给 all 函数。在第二种情形中，迭代器

