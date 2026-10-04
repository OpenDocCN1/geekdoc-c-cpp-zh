

### 4.3.2 定义排序等级

上一节中的性别因子代表了最简单的一种因子变量——只有两种可能的水准且没有排序，即一个水准在直觉上不会被认为“高于”或“跟随”另一个水准。这里你将查看具有可以逻辑排序的水准的因子；例如出生月份（MOB），有 12 个水准具有自然顺序。让我们将之前观察到的 MOB 存储为字符向量。

```
R mob <- c("Apr", "Jan", "Dec", "Sep", "Nov", "Jul", "Jun")
```

该向量中的数据存在两个问题。首先，并非所有可能的类别都被表示，因为 mob 仅包含七个唯一的月份。其次，该向量没有反映月份的自然顺序。如果你比较一月和十二月哪个更大，你会得到：

```
R mob[2]
[1] "Jan"
R mob[3]
[1] "Dec"
R mob[2]<mob[3]
[1] FALSE
```

从字母顺序来看，这个结果当然是正确的——J 不出现在 D 之前。但就我们感兴趣的日历月份而言，FALSE 的结果是不正确的。

如果你从这些值创建因子对象，可以通过向 factor 函数提供额外的参数来解决这两个问题。你可以通过向 levels 参数提供所有可能值的字符向量来定义额外的水准，然后通过将 ordered 参数设为 TRUE 来指示 R 严格按照 levels 中出现的顺序对值进行排序。

```
R ms <- c("Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec")
R mob.fac <- factor(x=mob,levels=ms,ordered=TRUE)
R mob.fac
[1] Apr Jan Dec Sep Nov Jul
Levels: Jan < Feb < Mar < Apr < May < Jun < Jul < Aug < Sep < Oct < Nov < Dec
```

这里，mob.fac 包含与之前 mob 向量相同的个体条目，且位于相同的索引位置。请注意，该变量有 12 个水准，即使你没有对 “Feb”、“Mar”、“Oct” 等水准进行任何观察。注意，如果你的控制台窗口太窄而无法打印所有水准到屏幕上，你可能会看到一个 ...，表示输出已被隐藏。只需拓宽窗口并重新打印对象即可查看隐藏的水准。此外，这些水准的严格顺序通过对象输出中的 < 符号显示。使用这个新的因子对象，你可以执行之前的关联比较并得到你可能期望的结果。

```
R mob.fac[2]
[1] Jan
Levels: Jan < Feb < Mar < Apr < May < Jun < Jul < Aug < Sep < Oct < Nov < Dec
R> mob.fac[3]
[1] Dec
Levels: Jan < Feb < Mar < Apr < May < Jun < Jul < Aug < Sep < Oct < Nov < Dec
R> mob.fac[2]<mob.fac[3]
[1] TRUE
```

这些改进远不止是外观上的。例如，某些类别中零观测的数据集与从开始就定义为更少类别的相同数据集之间存在很大差异。是否指示 R 正式对因子进行排序的选择，也可能在回归和其他类型的建模等各种统计方法实现中产生重要后果。

### 4.3.3 合并与切割

正如你所见，通常使用 c 函数很容易合并同种类的多个向量（无论是数值、逻辑还是字符）。这里有一个例子：

```
R foo <- c(5.1,3.3,3.1,4)
R bar <- c(4.5,1.2)
R c <- c(foo,bar)
[1] 5.1 3.3 4.0 4.5 1.2
```

这与因子值向量以相同的方式合并。然而，c 函数并不适用。让我们看看当你对表 4-4 中的数据和第 4.3.2 节中的 MOB 因子 mob.fac 使用它时会发生什么。假设你现在观察到另外三个个体，其 MOB 值为 “Oct”、“Feb” 和 “Feb”，存储为因子对象，如下所示。

```
R new_values <- factor(c("Oct"
```

```
[1] Oct Feb Feb
Levels: Jan < Feb < Mar < Apr < May < Jun < Jul < Aug < Sep < Oct < Nov < Dec
```

现在你有 mob.fac 中的原始观察值和 new.values 中的另外三个。两者都是因子对象，以相同的有序水准定义。你可能会期望你可以直接使用 c 将两者合并如下。

```
R> c(mob.fac,new.values)
[1] 4 1 12 9 11 7 7 10 2 2
```

显然，这没有达到你想要的效果。合并两个因子对象导致了一个数值向量。这是因为该函数将因子解释为整数。将此与定义的水准进行比较，你可以看到这些数字指的是每个月份在有序水准内的索引。

```
R> levels(mob.fac)
[1] "Jan" "Feb" "Mar" "Apr" "May" "Jun" "Jul" "Aug" "Sep" "Oct" "Nov" "Dec"
```

这意味着你可以使用这些整数与 levels 来检索完整观察数据的字符向量——原始的八个加上另外三个。

```
R> levels(mob.fac)[c(mob.fac,new.values)]
[1] "Apr" "Dec" "Sep" "Nov" "Jul" "Jun" "Oct" "Feb" "Feb"
```

现在你已将所有观察值存储在向量中，但它们当前存储为字符串，而不是值。最后一步是将此向量转换为因子对象。

```
R> mob.new <- levels(mob.fac)[c(mob.fac,new.values)]
R> mob.new.fac <- factor(x=mob.new,levels=levels(mob.fac),ordered=TRUE)
R> mob.new.fac
[1] Jan < Feb < Mar < Apr < May < Jun < Jul < Aug < Sep < Oct < Nov < Dec
```

正如这个例子所示，因子化需要两个对象来分解每个条目相对于因子水准的数值位置，然后再将它们重新组合在一起。这确保了水准的一致性以及最终产品中的观察值有效性。

因子也从最初在连续体上测量的数据创建，例如一组成人的体重或给予患者的药物剂量。有时你需要将这些类型的观察值分组（或分箱）到类别中，如 Small/Medium/Large 或 Low/High。在 R 中，你可以使用 cut 函数将这种数据映射到离散因子类别。考虑以下 10 个的数值向量：

```
R> Y <- c(0.53,5.4,1.5,3.3,33.0,0.45,0.1,2.4,1.9,1.0)
```

假设你想按如下方式对数据进行分箱：Small 指区间 [0,2) 中的观察值，Medium 指 [2,4)，Large 指 [4,6]。方括号指的是*包含*其最近的值，而括号表示*排除*，因此一个观察值 $y$ 将落在 Small 区间如果 $0 \le y < 2$，落在 Medium 如果 $2 \le y < 4$，或落在 Large 如果 $4 \le y \le 6$。为此你使用 cut 并向 breaks 参数提供你期望的断点：

```
R br <- c(0,2,4,6)
R cut(x=Y,breaks=br)
[0,2] [4,6] [2,4] [0,2] [0,2] [2,4] [4,6] [0,2]
Levels: (0,2] (2,4] (4,6)
```

这给了你一个因子，每个观察值现在被分配一个区间。然而，请注意你的边界区间是倒置的——你希望边界水准在左侧像 [0,2]，而不是像默认出现的那样在右侧，(0,2]。你可以通过将逻辑参数设为 FALSE 来修复它。

```
R cut(x=Y,breaks=br,right=F)
[0,2] [4,6] [2,4] [0,2] [0,2] [2,4] [4,6] [0,2]
Levels: (0,2] (2,4] (4,6]
```

现在你已交换了包含和排除的边界。这很重要，因为它改变了哪些类别会落入其中。请注意，第七个观察值已更改类别。但仍有一个问题：最终区间*排除*了 6，而你希望此最大值*包含*在最高等级中。你可以用另一个逻辑参数来修复它：include.lowest。即使它被称为“include.lowest”，此参数也可以用于在 right 为 FALSE 时包含*最高*值，如帮助文件 ?cut 中所述。

```
R cut(x=Y,breaks=br,right=F,include.lowest=T)
[0,2] [4,6] [2,4] [0,2] [0,2] [2,4] [4,6] [0,2]
Levels: (0,2] (2,4] (4,6]
```

区间现在定义为你想要的方式。最后，你希望为类别添加更好的标签，而不是使用 R 默认提供的水准，将字符字符串向量传递给 labels 参数。标签的顺序必须与因子对象中水准的顺序相匹配。

```
R lab <- c("Small","Medium","Large")
R cut(x=Y,breaks=br,right=F,include.lowest=T,labels=lab)
[1] Small Large Small Medium Small Small Large Small Small
Levels: Small Medium Large
```

