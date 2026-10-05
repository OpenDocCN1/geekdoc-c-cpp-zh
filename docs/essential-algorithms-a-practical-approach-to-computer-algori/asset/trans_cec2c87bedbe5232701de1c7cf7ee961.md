

# 492 附录 B — 练习题解答

要送五本书，你只需要选取五个名字放入数组的前五个位置，然后停止。这只需要五个步骤，所以速度非常快。数组中有多少个名字并不重要，只要至少有五个即可。

- 6. 简单地创建一个包含所有 52 张牌的数组，将其随机化，然后像往常一样发牌——轮流给每个玩家一张，直到每个人都拿到为止。

无论轮流给每个玩家发一张牌，还是一次性发完所有牌都没有关系。只要牌组是随机洗过的，每个玩家都会得到五张随机牌。

- 7. 图 B-2 显示了用 C# 编写的程序，该程序可以在书籍网站下载。每个值的数字是产生该值的掷百分比、实际的预期百分比以及百分比差异。

![](img/fefa42765c0b410af6705110aea7c0cb_515_0.png)

图 B-2：较少的试验次数有时会导致观测频率与预期掷频率之间出现显著差异。在试验次数足够大之前，实际结果与预期结果不匹配。对于约 10,000 次试验，程序产生的某些值误差超过了 5%。

- 8. 如果 $A_1 < B_1$，则 $Mod B_1 = A_1$，因此 $A_2 = B_2$ 且 $B_2 = A_1$。换句话说，在第一次循环期间，A 和 B 的值交换了。

- 9. $LCM(A, B) = A \times B / GCD(A, B)$。假设 $g = GCD(A, B)$，则对于某些整数 $m$ 和 $n$，$A = g \times m$ 且 $B = g \times n$。那么 $A \times B / GCD(A, B) = m \times n$$m$ 和 $n$ 没有公共因子，所以这就是最小公倍数（LCM）。

- 10. 下面的伪代码显示了 FastExponentiation 示例程序使用的算法，该程序可以在书籍网站下载。（**粗体行**用于练习 11。）

```
// 执行幂运算。
Integer: Exponentiate(Integer: value, Integer: exponent)
```

```
// 创建幂列表以及对应幂的值的列表。
List Of Integer: powers
List Of Integer: value_to_powers

// 从幂 1 和 value^1 开始
Integer: last_power = 1
Integer: last_value = value
powers.Add(last_power)
value_to_powers.Add(last_value)

// 计算其他幂，直到得到一个比 exponent 大的幂。
While (last_power < exponent)
    last_power = last_power * 2
    last_value = last_value * last_value
    powers.Add(last_power)
    value_to_powers.Add(last_value)
End While

// 组合值所需的幂。
Integer: result = 1

// 获取小于 exponent 的最大幂的索引。
For power_index = powers.Count - 1 Step -1
    // 检查该幂是否在 exponent 范围内。
    If (powers[power_index] <= exponent)
        // 使用这个幂。
        exponent = exponent - powers[power_index]
        result = result * value_to_powers[power_index]
Next power_index

// 返回结果。
Return result
End Exponentiate
```

- 11. 你需要修改前面代码中的粗体行。如果模数为 $m$，你需要将此行：

```
last_value = last_value * last_value
```

改为：

```
last_value = (last_value * last_value) Mod m
```

你还需要修改这一行：

```
result = (result * value_to_powers[power_index])
```

改为：

```
result = (result * value_to_powers[power_index]) Mod m
```

在书籍网站上可以下载的 ExponentMod 示例程序演示了这种算法。

# 494 附录 B — 练习题解答

图 B-3 显示了 GcdTimes 示例程序，该程序可以在书籍网站下载。灰色线条显示了步骤数与值的图表。顶部的深色曲线显示了值的对数。从图中很难步骤数是否真的遵循对数规律，但它显然增长得很缓慢。

![](img/fefa42765c0b410af6705110aea7c0cb_517_0.png)

- 13. 你已经知道 next\_prime $\times 2$ 已经被划除了，因为它是 2 的倍数。如果是 next\_prime $\times 3$，你知道 next\_prime $\times 3$ 已经被划除了，因为 3 已经考虑过了。对于每一个满足 $p < next\_prime$ 的质数 $p$，$p$ 已经考虑过了，所以 next\_prime $\times p$ 已经被划除了。第一个不小于 next\_prime 的质数是 next\_prime，第一个未考虑过的 next\_prime 的倍数是 next\_prime $\times next\_prime$。这意味着你可以将循环改为：

```
// 划掉该质数的倍数。
For i = next_prime * next_prime To max_number
iscomposite[i] = true
```

- 14. 下面的伪代码显示了一个显示卡米壶数（Carmichael numbers）及其质因数的算法：

```
// 生成卡米壶数。
GenerateCarmichaelNumbers(Integer: max_number)
Boolean: iscomposite[] = sieve of Eratosthenes for numbers 2 through max_number

// 检查卡米壶数。
For i = 2 To max_number
// 只检查非质数。
If {iscomposite[i]} Then
```

```
// 检查 i 是否是卡米壶数。
If (IsCarmichael(i)) Then
    <输出 i 和它的质因数>
End If
Next i

// 如果数字是卡米壶数则返回真。
Boolean: IsCarmichael(Integer: number)
```

- 15. 假设你使用中间值的高度。那么，如果函数是递增的，矩形的左部分太短，右部分太长，会相互抵消。同样，如果函数是递减的，矩形的左部分太长，右部分太短，会相互抵消。如果曲线在中间有局部最小值或极大值，这种方法将没有帮助（甚至可能有害）。

图 4 显示了 MidpointRectangle 示例程序，该程序可以在书籍网站下载，当你将结果与图 2-2 中的结果进行比较时，你会发现中间点法将误差从 6.5% 降低到了 0.2%，大约缩小了 30 倍，而没有改变矩形的数量。

- 16. 是的。这类似于使用随机点而不是网格的自适应网格积分。如果处理得当，它将比普通的蒙特卡洛积分更有效，因为它会选择更多感兴趣的点，减少位于形状内部或外部的大区域。

- 17. 下面的伪代码显示了在三维执行蒙特卡洛积分的高级算法：

```
Float: EstimateVolume(Boolean: PointIsInShape(..), Integer: num_trials,
Float: xmin, Float: xmax, Float: ymin, Float: ymax,
Float: zmin, Float: zmax)
Integer: num_hits = 0
For I = 1 To num_trials
Float: x = <xmin 到 xmax 之间的随机数>
Float: y = <ymin 到 ymax 之间的随机数>
Float: z = <zmin 到 zmax 之间的随机数>
If (PointIsInShape(x, y, z)) Then num_hits = num_hits + 1
Next I
```

```
Float: total_volume = (xmax - xmin) * (ymax - ymin) * (zmax - zmin)
Float: hit_fraction = num_hits / num_trials
Return total_volume * hit_fraction
End EstimateVolume
```

