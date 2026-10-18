![](bbox=[0.309, 0.067, 0.661, 0.226])

**FIGURE 7.1:** Infinitely many classifiers could separate the positive and negative instances.

decomposition methods are introduced in Section 7.6. Further, we discuss the multiclass strategies in Section 7.7 and make a summary in Section 7.8.

This chapter is not the only existing introduction of SVM. A number of surveys and books may be found in [6, 12, 33]. While this chapter does not discuss applications of SVMs, the reader is referred to [16] for a guide to such applications.

# 7.2  The Maximum Margin Perspective

Given the training data in the form of label-feature pairs,

$$S=\{(y_i,x_i)\mid y_i\in\{+1,-1\},\ x_i\in\mathbb{R}^n,\ \forall i=1\ldots l\}.$$

the goal of binary classification is to find a decision function $f(\mathbf{x})$ that could correctly predict the label $y$ of an input feature $\mathbf{x}$. The problem could be transformed to the determination of a function $h(\mathbf{x})$, such that

$$f(\mathbf{x})=\begin{cases}+1 & \text{when }h(\mathbf{x})>0,\\-1 & \text{when }h(\mathbf{x})<0.\end{cases}$$

The separating surface, which represents the boundary between positive and negative regions, is defined as follows:

$$\mathcal{H}=\{\mathbf{x}\mid h(\mathbf{x})=0\}.$$

Now consider a linearly separable scenario, where some linear functions

$$h(\mathbf{x})\equiv\mathbf{w}^{\mathsf{T}}\mathbf{x}+b$$

could separate the two regions. As shown in Figure 7.1, there may be infinitely many hyperplanes that separate the positive and negative instances correctly. A reasonable choice is the one with the largest gap between both classes. This setting, called the **Maximum Margin Classifier**, may be more resistant to any perturbation of the training data. Since the margin could be measured in different ways, we formally define the distances of a feature $\mathbf{x}$ to the set $\mathcal{H}$.

$$\operatorname{Distance}(\mathbf{x},\mathcal{H})\equiv\min_{\mathbf{p}\in\mathcal{H}}\|\mathbf{x}-\mathbf{p}\|.$$

Note that we may use different norms in the definition of distance. By [24, Theorem 2.2], there is a closed-form solution when $\mathcal{H}$ is a hyperplane:

$$\operatorname{Distance}(\mathbf{x},\mathcal{H})=\frac{|\mathbf{w}^{\mathsf{T}}\mathbf{x}+b|}{\|\mathbf{w}\|_*},$$