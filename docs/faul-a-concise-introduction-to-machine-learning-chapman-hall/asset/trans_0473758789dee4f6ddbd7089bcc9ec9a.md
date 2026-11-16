

特征是连续的，决策基于数值是大于还是小于某个阈值的问题。样本沿树向下遍历直到到达一个叶节点。每个叶节点关联一个类别。因此，样本被分配给其最终到达的叶节点的类别。

决策树是从训练集递归生长的。树的生长方式有很多种。在每个节点，到达该节点的训练样本集被分成两部分。这两个子集分别沿着其中一条分支传递给子节点。在每个节点，我们需要选择用于划分的特征以及阈值。为此，会考虑每个特征的所有可能划分，并选择最优划分。最优性基于不同的可能准则。

在讨论准则之前，我们需要引入一些符号。令 $t = P, L$ 或 $R$ 分别指代与父节点、左子节点或右子节点相关的量。例如，$N_P$ 是到达父节点的样本数量，而 $N_L$ 和 $N_R$ 分别是到达左子节点和右子节点的样本数量。令 $N_{tk}$ 是到达节点 $t$ 的类别 $k$ 的样本数量，其中 $k = 1, \dots, K$。我们定义 $p_{tk}$ 为节点 $t$ 中属于类别 $k$ 的样本比例。即

$$p_{tk} = \frac{N_{tk}}{N_t},$$

and we have

$$\sum_{k=1}^K p_{tk} = 1.$$

父节点的比例与子节点的比例以如下方式相关：

$$p_{Pk} = \frac{N_{Pk}}{N_P} = \frac{N_{Lk} + N_{Rk}}{N_P} = \frac{N_L p_{Lk} + N_R p_{Rk}}{N_P}.$$ (5.2)

如果一个节点只包含一个类别的样本，则称为*纯*节点。这自然成为一个叶节点。然而，并非所有叶节点都是纯节点，因为每个叶节点样本数量少的树可能会过拟合数据，并且对未见数据的泛化能力较差。因此，在包含混合类别样本的叶节点中，一些训练样本会被误分类。

我们将节点*不纯度* $i(t)$ 定义为类别比例的函数

$$i(t) = \phi(p_1, \dots, p_k).$$

我们将稍后讨论 $\phi$ 的具体选择。一个好的决策划分应优化纯度，换句话说，即最小化不纯度。由于两个子节点的大小可能不同，我们定义不纯度的变化 $\Delta i$ 为父节点的不纯度减去子节点不纯度的加权平均：

$$\Delta i = i(P) - \left( \frac{N_L}{N_P} i(L) + \frac{N_R}{N_P} i(R) \right).$$

![](img/d3c00252180686426c9e63ab889b535b_146_0.png)

Figure 5.9: 两个类别的不同节点不纯度。

最佳可能的划分最大化了所有特征的所有可能划分中的不纯度变化。如果没有可能的划分使得变化为正，则该节点不进行划分，并成为一个叶节点。

在考虑 $\phi$ 的具体选择之前，它需要满足某些属性。如果只存在一个类别，不纯度应为零。也就是说，$i(t) = 0$ 当且仅当某个 $k$ 的 $p_{tk} = 1$，而其他所有类别的比例为零。另一方面，当所有类别以相等比例混合时，即 $p_{t1} = \dots = p_{tK} = 1/K$，不纯度应为最大。此外，如果类别被重新标记，它也应是对称的。

不纯度 $i(t) = \phi(p_{t1}, \dots, p_{tK})$ 的一个常用选择是*基尼多样性指数 (gdi)*

$$i(t) = \sum_{k=1}^K p_{tk}(1 - p_{tk}) = 1 - \sum_{k=1}^K p_{tk}^2,$$

since $\sum_{k=1}^K p_{tk} = 1$。如果某个 $k$ 的 $p_{tk} = 1$，而其他所有类别的比例为零，则它消失。图 5.9 显示了两个类别的情况下，$i(t)$ 作为 $p_{t1}$ 的函数（或等价地 $p_{t2} = 1 - p_{t1}$）。

使用此选择，不纯度的变化为

$$\Delta i = \left( 1 - \sum_{k=1}^K p_{Pk}^2 \right) - \frac{N_L}{N_P} \left( 1 - \sum_{k=1}^K p_{Lk}^2 \right) - \frac{N_R}{N_P} \left( 1 - \sum_{k=1}^K p_{Rk}^2 \right)$$
$$= \sum_{k=1}^K \frac{N_R}{N_P} p_{Rk}^2 + \frac{N_L}{N_P} p_{Lk}^2 - p_{Pk}^2 ,$$

where we used \(N_L + N_R = N_P\). Inserting (5.2), gives

$$\Delta i = \sum_{k=1}^K \frac{N_R}{N_P} p_{Rk}^2 + \frac{N_L}{N_P} p_{Lk}^2 - \frac{(N_L p_{Lk} + N_R p_{Rk})^2}{N_P^2}$$
$$= \frac{1}{N_P^2} \sum_{k=1}^K N_R N_L (N_L + N_R) p_{Rk}^2 + N_L (N_L + N_R) p_{Lk}^2 - N_L^2 p_{Lk}^2 - 2 N_L N_R p_{Lk} p_{Rk} - N_R^2 p_{Rk}^2$$
$$= \frac{N_R}{N_P} \frac{N_L}{N_P} \sum_{k=1}^K (p_{Lk} - p_{Rk})^2 .$$

我们可以看到，如果子节点中的比例彼此相似，那么不纯度的变化将很小。然而，如果比例相当不同，那么 \(\Delta i\) 将会很大。

类似地，另一种称为*双分 (twoing)* 的可能性选择最大化以下内容的划分

$$\Delta i = \frac{N_L N_R}{N_P N_P} \left( \sum_{k=1}^K |p_{Lk} - p_{Rk}| \right)^2 .$$

当类别较多时，即 \(K\) 较大时，它常被使用。

\(i(t)\) 的另一种选择是*偏差*，也称为*交叉熵*

$$i(t) = - \sum_{k=1}^K p_{tk} \log p_{tk} .$$

它也在图 5.9 中绘制。在这种情况下，我们有

$$\Delta i = - \sum_{k=1}^K p_{Lk} \log p_{Lk} + \frac{N_L}{N_P} \sum_{k=1}^K p_{Lk} \log p_{Lk} + \frac{N_R}{N_P} \sum_{k=1}^K p_{Rk} \log p_{Rk} .$$

使用 \(p_{tk} = N_{tk} / N_t\) 和 \(N_{Pk} = N_{Lk} + N_{Rk}\)，这可以重写为

$$\Delta i = \frac{1}{N_P} \sum_{k=1}^K N_{Lk} \log \frac{p_{Lk}}{p_{Pk}} + N_{Rk} \log \frac{p_{Rk}}{p_{Pk}} .$$

如果子节点中的比例与父节点中的比例保持相似，那么不纯度的变化将很小，因为分数接近于一，且对数在那里取值为零。然而，如果比例与父节点中的比例不相似，尤其是当它们接近零或一时，那么 \(\Delta i\) 会更大。

有人可能会将节点误差作为 \(i(t)\) 的一种可能性。如果一个节点被分配给在该节点上训练样本比例最大的类别，则节点误差是误分类样本的比例：
\(i(t) = 1 - \max_k p_{tk}.\)

图 5.9 以图形方式说明了这一点。比较 \(gdi\)、\(deviance\) 和 \(node\) \(error\) 的图表，在类别具有相似平衡性的节点中，在 \(gdi\) 和 \(deviance\) 下被认为比在 \(node\) \(error\) 下更不纯。这导致 \(node\) \(error\) 不倾向于创建更纯的子节点。要看清这一点，请考虑
\(\Delta i = (1 - \max_k p_{Pk}) - \frac{N_L}{N_P}(1 - \max_k p_{Lk}) - \frac{N_R}{N_P}(1 - \max_k p_{Rk})\)
\(= 1 - \max_k \frac{N_{Pk}}{N_P} - \frac{N_L}{N_P} + \frac{N_L}{N_P} \max_k \frac{N_{Lk}}{N_L} - \frac{N_R}{N_P} + \frac{N_R}{N_P} \max_k \frac{N_{Rk}}{N_R}\)
\(= \frac{1}{N_P} \left( \max_k N_{Lk} + \max_k N_{Rk} - \max_k N_{Pk} \right),\)

where we used \(N_L + N_R = N_P\). Thus, the change in impurity is solely dependent on the sum of the numbers of largest classes in the child nodes. This number can be kept constant for different splits, while the purity of the child nodes is very different. [5] gives a numerical example: Suppose there are only two classes and at the parent node they have equal parity, \(N_{P1} = N_{P2} = 400\). One possible split is \(N_{L1} = 100, N_{L2} = 300, N_{R1} = 300, N_{R2} = 100\), while another one is \(N_{L1} = 200, N_{L2} = 400, N_{R1} = 200, N_{R2} = 0\). Both result in \(\Delta i = (600 - 400)/800 = 1/4\). However, the second split is preferable, since there the right node is pure, and thus a leaf. For the first split, both child nodes are impure and need to grow branches.

图 5.10a 显示了我们之前的示例，这次区域是由决策树分类的。图 5.10b 显示了相应的决策树。每个节点对应于某个区域的划分。第一个节点沿着 2.45 处的垂直线划分整个区域。这条线右侧的区域随后沿着 1.75 处的水平线进行划分。最后一个节点沿着 4.95 处的垂直线划分位于这条线下方且位于第一条线右侧的区域。可以看出，这个决策树可以通过让水平划分稍微低一些（例如 1.65）来改进。这将导致唯一一个被误分类的 virginica 样本被正确分类。

决策树的深度由三个参数控制：允许的分支节点划分的最大数量，需要在要划分的节点中的最小样本数，以及每个叶节点的最小样本数。在图 5.10 的示例中，叶节点中的最小样本数

