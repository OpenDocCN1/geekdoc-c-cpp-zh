
![](img/4d808358747f9096d24f831e5f9d8083_41_0.png)

**FIGURE 1.6** (a) 一个示例因子图。该图表示一个包含五个随机变量的联合概率分布的因子化：$P(a,b,c,d,e) \propto f_1(a,b,c)f_2(b,d)f_3(c,e)f_4(d,e)$。 (b) 一个用于利用线性约束节点求解经典兰伯特(Lambertian)形状从光照问题的因子图。该三维（3D）形状的表示是两倍过完备的，包括每个像素的 $p$ 和 $q$ 斜率值。黑色方块表示线性约束节点，它们强制解的可整合性（integrability）。灰色方块表示编码反射函数的因子节点。

multivariate distribution) and a set of factor nodes (one for each potential function). Each factor node is connected to each variable referenced by its corresponding potential function. (See Figure 1.6 for an example, or reference (Frey, 1998) for a review of factor graphs.) Factor graphs that satisfy certain constraints can be expressed as Bayes networks, or for other constraints, as Markov random fields (MRFs). Thus, these approaches are intimately connected and are equivalent in terms of neural plausibility.

Exact inference on factor graphs is possible only for a small subclass of problems. In most cases, approximate methods must be used. There are a variety of existing approaches to approximate the mode of the posterior distribution (MAP, or maximum *a posteriori*) or its mean (MMSE, or minimum mean-squared error), such as Markov chain Monte Carlo (MCMC) sampling, graph cuts, and belief propagation. In this section, we explore the use of the belief propagation algorithm. Belief propagation is advantageous in that it imposes fewer restrictions on the potential functions than graph cuts (Kolmogorov and Zabih, 2001) and is faster than MCMC. Belief propagation is also interesting in that it is highly neurally plausible (Lee and Mumford, 2003; Rao, 2004) and has been advanced as a possible model for statistical inference in the brain (Pearl, 1988).

Belief propagation has been applied successfully to a wide variety of computer vision problems (Freeman et al., 2000; Potetz, 2007; Sun et al., 2003; Tang et al., 2005) and has shown impressive empirical results on a number of other problems (Frey and Dueck, 2007; Kschischang and Frey, 1998). Initially, the reasons behind the success of belief propagation were only understood for those cases where the underlying graphical model did not contain loops. The many empirical successes on graphical models that did contain loops were largely unexplained. However, recent discoveries have provided a solid theoretical justification for “loopy” belief propagation by showing that when belief propagation converges, it computes a minimum of a measure used in statistical physics known as the Bethe free energy (Yedidia et al., 2000). The Bethe free energy is based on a principled approximation of the KL-divergence between a graphical model and a set of marginals and has been instrumental in studying the behaviors of large systems of interacting particles, such as spin glasses. The connection to Bethe free energy had an additional benefit in that it inspired the development of algorithms that minimize the Bethe free energy directly, resulting in variants of belief propagation that guarantee convergence (Heskes et al., 2003; Yuille, 2002), improve performance (Yedidia et al., 2000, 2003), or in some cases, guarantee that belief propagation computes the *globally* optimal MAP point of a distribution (Weiss and Freeman, 2007).

Belief propagation estimates the marginals $b_i(x_i)=\sum_{\mathbf{X}\setminus x_i}P(\mathbf{X})$ by iteratively computing *messages* along each edge of the graph according to the following equations:

$$
m_{i\to f}^{t+1}(x_i)=\prod_{g\in\mathcal{N}(i)\setminus f}m_{g\to i}^{t}(x_i) \tag{1.9}
$$

$$
m_{f\to i}^{t+1}(x_i)=\sum_{\tilde{\mathbf{x}}_{\mathcal{N}(f)\setminus i}}\phi_f(\tilde{\mathbf{x}}_{\mathcal{N}(f)})\prod_{j\in\mathcal{N}(f)\setminus i}m_{j\to f}^{t}(x_j) \tag{1.10}
$$

$$
b_i(x_i)\propto\prod_{g\in\mathcal{N}(i)}m_{g\to i}^{t}(x_i) \tag{1.11}
$$

where $f$ and $g$ are factor nodes, $i$ and $j$ are variable nodes, and $\mathcal{N}(i)$ is the set of neighbors of node $i$ (Heskes, 2004). Here, $b_i(x_i)$ is the estimated marginal of variable $i$. Note that the expected value of $\bar{X}$ or equivalently, the minimum mean-squared error (MMSE) point estimate, can be computed by finding the mean of each marginal. If the most likely value of $\bar{X}$ is desired, also known as the maximum *a posteriori* (MAP) point estimate, then the integrals of Equation (1.10) are replaced by suprema. This is known as *max-product belief propagation*.

to a straightforward computation of Equation (1.13), which is \(O(M^4)\). In (Potetz and Lee, 2008), we show how this approach can be used to compute messages in time \(O(M^2)\) for all potential functions of the form

$$
\phi(\vec{x}) = g\left(\sum_i g_i(x_i)\right) \tag{1.17}
$$

This reduces a problem from exponential time to linear time with respect to the number of variables connected to a factor node. Potentials of this form are common in graphical models, in part because they offer advantages in training graphical models from real data (Friedman et al., 1984; Hinton, 1999; Roth and Black, 2005; Zhu et al., 1998).

This approach reduces a problem from exponential time to linear time with respect to the number of variables connected to a factor node. With this efficient algorithm, we were able to apply belief propagation to the classical computer vision problem of shape from shading, using the factor graph shown in Figure 1.6 (see Potetz, 2007 for details). Previously, the general problem of shape from shading was solved using gradient descent-based techniques. In complex, highly nonlinear problems like shape from shading, these approaches often become stuck inside local, suboptimal minima. Belief propagation helps to avoid difficulties with local minima in part because it operates over whole probability distributions. Gradient descent approaches maintain only a single 3D shape at a time, iteratively refining that shape over time. Belief propagation seeks to optimize the single-variate marginals \( b_i(x_i) \) for each variable in the factor graph.

Solving shape from shading using belief propagation performs significantly better than previous state-of-the-art techniques (see Figure 1.7). Note that without the efficient techniques described here, belief propagation would be intractable for this problem, requiring over 100,000 times longer to compute each iteration. In addition to improved performance, solving shape from shading using belief propagation allows us to relax many of the restrictions typically assumed by shape-from-shading algorithms in order to make the problem tractable. The classical definition of the shape-from-shading problem specifies that lighting must originate from a single point source, that surfaces should be entirely matte, or Lambertian in reflectance, and that no markings or colorations can be present on any surface. The flexibility of the belief propagation approach allows us to start relaxing these constraints, making shape from shading viable in more realistic scenarios.

![](img/4d808358747f9096d24f831e5f9d8083_45_0.png)

**FIGURE 1.7**  我们使用循环信念传播（行 b）推断光照下的形状与光照的结果与以往方法（行 c 和 d）的对比。每行包含一个三维（3D）线框图（右侧）和在光源位置 (1,0,1) 处渲染（左侧）的表面。 (a) 原始表面。该列的渲染作为后续三列 SFS（形状与光照）算法的输入。 (b) 使用我们线性约束节点方法恢复的表面。 (c) 使用 Lee 和 Kuo (1993) 所述方法恢复的表面。该算法在张等人 (1999) 综述的六种 SFS 算法中表现最佳。 (d) 使用 Zheng 和 Chellappa (1991) 所述方法恢复的表面。我们的方法（行 b）在显著改善了以往领先方法。特别重要的是，恢复的表面渲染与原始输入图像非常相似。这意味着每个像素的 Lambertian 约束得到了满足，而原始与恢复表面之间的任何错误主要归因于这里使用的自然三维形状的简化先验概率模型。

