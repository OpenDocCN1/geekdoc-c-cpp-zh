

迭代地。每次迭代，只涉及一个或一小批数据。另一个可以自然地应用在线学习策略的场景是为流数据学习距离度量，其中数据以流式方式到来，因此距离度量需要迭代更新。接下来我们介绍两种在线距离度量学习方法的例子。

## 18.4.2.1 伪度量在线学习算法（POLA）

伪度量在线学习（POLA）[17] 属于成对约束的监督度量学习范畴。更具体地说，存在一个必须链接约束集 ℳ 和一个不能链接约束集 𝒞。POLA 为 ℳ 或 𝒞 中的每一对 (x_i, x_j) 分配一个标签 l_ij，使得如果 (x_i, x_j) ∈ ℳ，则 l_ij = 1；如果 (x_i, x_j) ∈ 𝒞，则 l_ij = −1。然后它引入一个阈值 b 并构造以下约束

∀(x_i, x_j) ∈ ℳ, l_ij = 1 ⇒ (x_i − x_j)^⊤ M (x_i − x_j) ≤ b − 1  (18.35)
∀(x_i, x_j) ∈ 𝒞, l_ij = −1 ⇒ (x_i − x_j)^⊤ M (x_i − x_j) ≥ b + 1  (18.36)

可以统一为
l_ij [b − (x_i − x_j)^⊤ M (x_i − x_j)] ≥ 1  (18.37)

注意该公式与标准 SVM 中的约束类似。然后 POLA 的目标是以下铰链损失
ℐ_ij(M, b) = max(0, l_ij[(x_i − x_j)^⊤ M (x_i − x_j) − b] + 1).  (18.38)

两个约束集定义为
𝒞_ij^1 = { (M, b) ∈ ℝ^{n²×1} : ℐ_ij(M, b) = 0 }  (18.39)
𝒞² = { (M, b) ∈ ℝ^{n²×1} : M ⪰ 0, b ≥ 1 }  (18.40)

POLA 以迭代方式运行：首先 POLA 将 M 初始化为零矩阵，然后在每一步，它从约束集（ℳ 或 𝒞）中随机挑选一对数据，然后交替地在 𝒞_ij^1 和 𝒞² 上进行投影。通过将 M 和 b 投影到 𝒞_ij^1 上，POLA 得到 M 和 b 的更新规则为

M̂ = M − l_ij α_ij u_ij u_ij^⊤  (18.41)
b̂ = b + α_ij l_ij  (18.42)

其中
u_ij = x_i − x_j  (18.43)
α_ij = ℐ_ij(M, b) / (||u_ij||₂⁴ + 1).  (18.44)

通过将 (M, b) 投影到 𝒞² 上，POLA 更新 M 为
M̂ = M − λ μ μ^⊤  (18.45)

其中 λ = min{λ̃, 0} 且 (λ̃, μ) 是 M̂ 的最小特征值-特征向量对。因此，POLA 以顺序方式并入约束集中的数据。

## 18.4.2.2 在线信息论度量学习（OITML）

我们在这里想要回顾的另一种技术是在线信息论度量学习（OITML）方法 [3]。该方法也属于监督度量学习范畴。它是我们第 18.3.5 节中介绍的 ITML 方法的在线版本。假设在时间 t + 1，我们需要从约束集中随机挑选一对数据，并最小化以下目标

M_{t+1} = arg min_M R(M, M_t) + η_t ℓ(D_t, D̂_t) (18.46)

其中 D̂_t = (x_i - x_j)^T M (x_i - x_j) 且 R(M, M_t) = d_logdet(M, M_t) 是 logdet 散度。[3] 表明 M_{t+1} 可以用以下规则更新

M_{t+1} ← M_t - [2 η_t (D_t - D̂_t) M_t (x_i - x_j)(x_i - x_j)^T M_t] / [1 + 2 η_t (D_t - D̂_t) (x_i - x_j)^T M_t (x_i - x_j)] (18.47)

其中

η_t = { η0, D_t - D̂_t ≤ 0; min { η0, 1/[2(D_t - D̂_t)] ( 1 / [(x_i - x_j)^T (I + (M_t^{-1} - I)^{-1}) (x_i - x_j)] ) }, otherwise. (18.48)

POLA 和 OITML 只是在线距离度量学习的两个例子。

## 18.5 结论与讨论

到目前为止，我们已经介绍了近年来最先进的监督距离度量学习算法。上面列出的所有监督度量学习方法都需要一些预先指定的自由参数，并且它们都涉及一些昂贵的计算过程，例如特征值分解或半定规划。ITML 方法是一个例外，因为它采用了 Bregman 投影策略，可能使解相对高效。然而，ITML 对 M0 的初始选择很敏感，这使得在我们没有足够先验知识的情况下难以应用。在实践中，根据提供的监督信息类型，我们可以选择能够处理该监督信息的适当的监督度量学习方法。然而，在许多现实世界应用中，获取该监督信息可能代价高昂且耗时。接下来我们将调查半监督方法，这些方法可以利用标记和未标记信息。对于距离度量学习研究的未来，我们认为以下方向是有前景的。

- 大规模距离度量学习。大多数现有的距离度量学习方法涉及计算昂贵的过程。我们如何使距离度量学习在大规模数据上高效且实用？有前景的解决方案包括在线学习或分布式学习。我们已在第 4.1 节中介绍了在线距离度量学习的最新工作。对于并行/分布式距离度量算法，由于涉及的主要计算技术是特征值分解和二次规划，我们可以采用并行矩阵计算/优化算法 [1,15] 来使距离度量学习更具可扩展性和效率。

- 经验评估。虽然已经提出了许多距离度量学习算法，但对于许多距离度量学习算法在现实世界应用中的效用，仍然缺乏系统的比较和证明点。这种经验讨论有助于展示距离度量学习算法的实际价值。一些最近的工作已经开始开发和应用距离度量学习于医疗保健，用于衡量患者之间的相似性 [19, 23, 24]。

- 一般公式。如本综述所示，大多数现有的距离度量学习算法假设学习到的距离度量在投影空间中是欧几里得的。这种假设可能不足以满足现实世界的应用，因为没有保证欧几里得距离最适合描述成对数据的关系。已经有一些初步的努力朝这个方向发展 [5, 13]，并且这个方向绝对值得探索。

## 参考文献

[1] Yair Censor. *Parallel Optimization: Theory, algorithms, and applications.* Oxford University Press, 1997.

[2] Koby Crammer and Yoram Singer. On the algorithmic implementation of multiclass kernel-based vector machines. *Journal of Machine Learning Research*, 2:265–292, 2001.

[3] Jason V. Davis, Brian Kulis, Prateek Jain, Suvrit Sra, and Inderjit S. Dhillon. Information-theoretic metric learning. In *Proceedings of International Conference on Machine Learning*, pages 209–216, 2007.

[4] Richard O. Duda, Peter E. Hart, and David G. Stork. *Pattern Classification (2nd Edition).* Wiley-Interscience, 2nd edition, 2001.

[5] Charles Elkan. Bilinear models of affinity. Personal note, 2011.

[6] Keinosuke Fukunaga. *Introduction to Statistical Pattern Recognition, Second Edition (Computer Science and Scientific Computing Series).* Academic Press, 1990.

[7] Jacob Goldberger, Sam Roweis, Geoff Hinton, and Ruslan Salakhutdinov. Neighborhood component analysis. In *Advances in Neural Information Processing Systems*, 17:513–520, 2004.

[8] Y. Guo, S. Li, J. Yang, T. Shu, and L. Wu. A generalized foley-sammon transform based on generalized fisher discriminant criterion and its application to face recognition. *Pattern Recognition Letters*, 24(1-3):147–158, 2003.

[9] Steven C. H. Hoi, Wei Liu, and Shih-Fu Chang. Semi-supervised distance metric learning for collaborative image retrieval. In *Proceedings of IEEE Computer Society Conference on Computer Vision and Pattern Recognition*, pages 1–7, 2008.

[10] Yangqing Jia, Feiping Nie, and Changshui Zhang. Trace ratio problem revisited. *IEEE Transactions on Neural Networks*, 20(4):729–735, 2009.

[11] András Kocsor, Kornél Kovács, and Csaba Szepesvári. Margin maximizing discriminant analysis. In *Proceedings of European Conference on Machine Learning*, volume 3201 of *Lecture Notes in Computer Science*, pages 227–238. Springer, 2004.

[12] Brian Kulis. Metric learning. Tutorial at International Conference on Machine Learning, 2010.

