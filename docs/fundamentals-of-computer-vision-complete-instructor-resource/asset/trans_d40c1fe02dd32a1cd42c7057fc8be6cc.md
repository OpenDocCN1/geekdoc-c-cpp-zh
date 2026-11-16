

![](img/5f95dd954ac63cc68119f6f48ca99e18_366_0.png)

图 13.1 同一栋建筑的两张图像重叠。事实上，它们是同一相机简单旋转的结果。

between 0 and 255. A derivation that assumes nothing can be brighter than 255 can produce interesting results, as with 255 + 2 = 1. More subtle assumptions are also around, for example, a relationship may be linear if the second camera is a rotation of the first, but not if rotations and translations are combined.

介于 0 和 255 之间。假设没有任何东西比 255 更亮的推导可以产生有趣的结果，例如 255 + 2 = 1。还有更微妙的假设，例如，如果第二台相机是第一台相机的旋转，则关系可能是线性的，但如果旋转和平移结合在一起，则不是。

Also be aware that numerical methods such as inverse problems may be surprisingly sensitive to small errors. Learn the meaning of ill-conditioned. As we discussed in Chapter 6, ill-conditioned systems require special treatment.

还要注意，诸如逆问题之类的数值方法可能对小错误出奇地敏感。了解病态条件的含义。如第 6 章所讨论，病态系统需要特殊处理。

### Choose Performance Metrics

### 选择性能指标

In the next step, you will need to test your algorithm on some images. Wouldn’t you love to say, “My algorithm works better than any other on this data!” But what do you mean works better? You need to decide (possibly even before you begin the work) how you will evaluate the results. What is good performance? How can you measure it? How can you compare it?

下一步，您需要在一些图像上测试您的算法。您难道不想说：“我的算法在这组数据上优于任何其他算法！”吗？但您所说的“更好”是什么意思？您需要决定（甚至可能在开始工作之前）如何评估结果。什么是良好性能？如何衡量它？如何比较它？

### Test Your Idea on a Synthetic Image

### 在合成图像上测试您的想法

If you completed the project assignments of Chapter 5, you already simulated an ideal image. Then, you corrupted that image with blur and noise. This sort of simulation allows you to test your algorithms under the most favorable conditions. If your algorithm doesn’t work on synthetic images, it almost certainly won’t work on real images, which have unknown and unmeasured distortions.

如果您完成了第 5 章的项目作业，您已经模拟了一张理想图像。然后，您用模糊和噪声损坏了该图像。这种模拟允许您在最有利的条件下测试您的算法。如果您的算法在合成图像上不起作用，那么它几乎肯定也无法在真实图像上工作，因为真实图像具有未知且未测量的畸变。

### Test Your Idea on a Phantom

### 在幻体上测试您的想法

A phantom is a real image, but it contains features that have been very carefully measured. The lead-hole images that you may have analyzed in the homeworks of Chapter 9 are of holes drilled with high precision in a circuit board. Since you know with great precision the parameters of the object being imaged, these images represent a type of phantom, and your algorithm should return precise answers when it determines the radius of those holes.

幻体是一张真实图像，但它包含经过非常仔细测量的特征。您可能在第 9 章的作业中分析过的铅孔图像是电路板上高精度钻孔的图像。由于您对被成像物体的参数了如指掌，这些图像代表一种幻体，当您的算法确定这些孔的半径时，应返回精确的答案。

Medical physicists calibrating x-ray machines also use a type of phantom, in the form of a block of plastic or wax with very tiny wires embedded in the wax. These wires will be visible only if the x-ray machine is working optimally.

校准 X 射线机的医学物理学家也使用一种幻体，形式为嵌有极细导线的塑料或蜡块。只有当 X 射线机工作最佳时，这些导线才可见。

### Determine the Answer to “What Is Truth?”

### 确定“什么是真理”的答案

You probably can’t find the definitive answer to this ancient question, but you can and must test your algorithm on real examples. To do that, you must determine some definition for how well your algorithm is performing, and that requires a definition of what correct performance is. For example, in medical imaging, you might decide that if three expert radiologists agree, their collective judgement is correct by definition. You get to choose the definition, but to publish your results, you have to defend your decision.

您可能无法找到这个古老问题的最终答案，但您可以而且必须在真实示例上测试您的算法。为此，您必须确定算法表现良好的某个定义，而这需要定义什么是正确性能。例如，在医学影像中，您可能会决定，如果三位专家放射科医生意见一致，那么他们的集体判断按定义就是正确的。您可以选择定义，但要发表结果，您必须为您的决定辩护。

### Thoroughly Test Your Algorithm

### 彻底测试您的算法

You will need to run many tests. Evaluate your algorithm as a function of multiple image distortions, such as the amount of additive noise, the diversity of test examples, etc. When it fails, learn what makes it fail.

您需要运行许多测试。作为多种图像畸变（例如加性噪声的量、测试示例的多样性等）的函数来评估您的算法。当它失败时，了解导致其失败的原因。

The list of topics above isn't complete. We didn't include techniques on how to avoid letting frustration get you down.

上面的主题列表并不完整。我们没有包括如何避免沮丧打垮您的技巧。

In this book, we have introduced a few very important principles. When you encounter a real problem, you can use the principles you have mastered here to help you grasp the nature of the problem and how hard it might be to solve. Then, you can move on to more detailed literature that will provide more, but narrower direction. For example, the “bible” of multi-camera image analysis is a 400-page book [13.1], which covers in great detail the topics to which we provide an introduction in sections 12.2–12.3.

在本书中，我们介绍了几条非常重要的原则。当您遇到实际问题时，可以使用在此掌握的原则来帮助您把握问题的本质以及解决问题可能有多困难。然后，您可以转向更详细的文献，这些文献将提供更多但更狭窄的方向。例如，多相机图像分析的“圣经”是一本 400 页的书 [13.1]，它详细涵盖了我们在第 12.2–12.3 节中介绍的主题。

We hope that the introduction given in this book makes your life a bit easier as you move into this exciting field!
W.E.S. and H.Q.

我们希望本书提供的介绍能让您进入这个激动人心的领域时生活轻松一些！
W.E.S. 和 H.Q.

## Bibliography

## 参考文献

- [13.1] R. Hartley and A. Zisserman. *Multiple view geometry in computer vision*, volume 2. Cambridge University Press, 2000.

- [13.1] R. Hartley 和 A. Zisserman. *计算机视觉中的多视图几何*, 第 2 卷. 剑桥大学出版社, 2000.

- [13.2] Sir Isaac Newton. *Mathematical Principles of Natural Philosophy*. The Royal Society, 1687.

- [13.2] 艾萨克·牛顿爵士. *自然哲学的数学原理*. 皇家学会, 1687.

- [13.3] M. A. Sutton, J. J. Orteu, and H. Schreier. *Image Correlation for Shape, Motion and Deformation Measurements*. Springer, 2009.

- [13.3] M. A. Sutton, J. J. Orteu, 和 H. Schreier. *用于形状、运动和变形测量的图像相关*. Springer, 2009.

## Appendix A Support Vector Machines

## 附录 A 支持向量机

In Chapter 1 of this book, we distinguished between *Pattern Recognition* and *Computer Vision*. Computer Vision systems make measurements on images, and Pattern Recognition systems accept measurements as inputs and make decisions.

在本书第 1 章中，我们区分了*模式识别*和*计算机视觉*。计算机视觉系统对图像进行测量，而模式识别系统接受测量作为输入并做出决策。

There is a problem with these definitions. At the time of publication of this book, many Computer Vision experts are working on the problem of *Object Recognition*, assigning a label to an object (e.g., bicycle or car) in a scene that is cluttered with other objects and background. Making such a decision is clearly a pattern recognition problem, but most research in this area is published in the Computer Vision literature.

这些定义存在一个问题。在本书出版时，许多计算机视觉专家正在研究*对象识别*问题，即在杂乱的其他物体和背景的场景中为物体（例如，自行车或汽车）分配标签。做出这样的决定显然是一个模式识别问题，但该领域的大多数研究都发表在计算机视觉文献中。

Support Vector Machines (SVMs) are systems that accept a set of measurements from two classes, $I_1 = \{x_1 \ x_{12} \ ...\}$ and $I_2 = \{x_1 \ x_{22} \ ...\}$. Having gained information from those two sets, then given an unknown x, the SVM can decide whether x belongs to class 1 or class 2. Such a machine is clearly a pattern classifier, and their operation is also taught in pattern recognition books.

支持向量机 (SVM) 是接受来自两个类的一组测量值的系统，$I_1 = \{x_1 \ x_{12} \ ...\}$ 和 $I_2 = \{x_1 \ x_{22} \ ...\}$。从这两组中获得信息后，给定未知 x，SVM 可以决定 x 属于类 1 还是类 2。这样的机器显然是一个模式分类器，其操作也在模式识别书籍中教授。

Nevertheless, the SVM is often used in solving computer vision problems like object recognition, and the inputs are usually measurements from image feature measurement systems like HoG's (see section 11.6). You, the student reading this book, are likely to meet people who are working on state-of-the-art systems (or at least reading about them). Since you should know at least a bit about these systems, we will introduce you to the basic concepts.

尽管如此，SVM 常用于解决对象识别等计算机视觉问题，输入通常来自图像特征测量系统（如 HoG）（参见第 11.6 节）。阅读本书的您，学生，很可能会遇到正在从事最先进系统（或至少阅读相关内容）的人。既然您应该至少了解一些这些系统，我们将向您介绍基本概念。

Support Vector Machines are pattern classifiers based on the concept of minimizing structural risk, which were first introduced by Vapnik [A.7]. They provide performance superior to most other pattern classification methods when the classification problem is to distinguish between two classes.

支持向量机是基于最小化结构风险概念的模式分类器，最初由 Vapnik [A.7] 引入。当分类问题是区分两个类时，它们提供优于大多数其他模式分类方法的性能。

### A.1 Derivation of the Support Vector Machine

### A.1 支持向量机的推导

Assume the problem may be described by asking to which of two classes an unknown vector belongs, and suppose two training sets are provided, each consisting of examples from one of the classes. Further assume the two classes are separable by a linear hypersurface.

假设问题可以描述为询问未知向量属于两个类中的哪一个，并假设提供了两个训练集，每个由一个类的示例组成。进一步假设两个类可以由线性超平面分离。

The feature space is to be divided by a hyperplane into two regions, in which the examples of the training sets are separated. Define the distance from the closest point in class 1 to the hyperplane as $d_1$. Similarly let $d_2$ be the distance from the closest point in class 2 to the hyperplane. The *margin* is defined as $d_1 + d_2$. Instead of accepting any hyperplane that divides the region space, we seek the hyperplane that maximizes the margin.

特征空间将由一个超平面分为两个区域，训练集的示例在这两个区域中被分开。定义类 1 中最近点到超平面的距离为 $d_1$。同样，令 $d_2$ 为类 2 中最近点到超平面的距离。*间隔*定义为 $d_1 + d_2$。我们不接受任何划分区域空间的超平面，而是寻求最大化间隔的超平面。

Given an unknown feature vector x, project this sample onto some unit vector $\phi$, and make a decision using the following rule:

给定未知特征向量 x，将此样本投影到某个单位向量 $\phi$ 上，并使用以下规则做出决策：

```
decide class 1 if $\phi^T x - q > 0$ otherwise decide class 2, (A.1)
```

where $q$ is a scalar constant. Let $x_1$ and $x_2$ denote points in class 1 and class 2 respectively. Since we are seeking the points closest to the decision hyperplane, we seek $x_1$ and $x_2$ such that their projections onto $\phi$ are as close together as possible, while still being on the correct side. That is, we seek points $x_1$ and $x_2$ such that with minimal positive $\rho$,

其中 $q$ 是标量常数。令 $x_1$ 和 $x_2$ 分别表示类 1 和类 2 中的点。由于我们寻找最接近决策超平面的点，我们寻找 $x_1$ 和 $x_2$，使它们在 $\phi$ 上的投影尽可能接近，同时仍在正确的一侧。也就是说，我们寻找点 $x_1$ 和 $x_2$，使得在最小正 $\rho$ 下，

```
$\phi^T x_1 = q + \rho$
$\phi^T x_2 = q - \rho$. (A.2)
```

Define $I_i$ to be the set of training examples from class $i$. For any point $x$ in $I_i$, $\phi^T x - q > \rho$, and for any such point in $I_2$, $\phi^T x - q < -\rho$. We need to find two things: (1) a pair of points, one in each class, which are as close together as possible. We will call these points *support vectors*; and (2) a vector onto which to project the support vectors so that their projections are maximally far apart. We solve this problem as follows:

定义 $I_i$ 为来自类 $i$ 的训练示例集合。对于 $I_i$ 中的任何点 $x$，$\phi^T x - q > \rho$，对于 $I_2$ 中的任何这样的点，$\phi^T x - q < -\rho$。我们需要找到两件事：(1) 一对点，每个类一个，它们尽可能接近。我们将这些点称为*支持向量*；以及 (2) 一个向量，用于投影支持向量，使它们的投影尽可能远离。我们按以下方式解决这个问题：

Recall that $\phi$ was a unit vector. It is thus equal to some other vector in the same direction divided by its magnitude, $\phi = \frac{w}{||w||}$. We will find one such vector, with certain properties that will be introduced shortly. For now, let $x_1$ denote any point in $I_1$, not necessarily a support vector, and similarly for $x_2$. Then

回想一下，$\phi$ 是一个单位向量。因此，它等于同一方向的某个其他向量除以其模长，$\phi = \frac{w}{||w||}$。我们将找到这样一个向量，不久将介绍其某些属性。目前，令 $x_1$ 表示 $I_1$ 中的任何点，不一定是支持向量，$x_2$ 亦然。那么

```
$\frac{w}{||w||} x_1 - q \ge \rho$
$\frac{w}{||w||} x_2 - q \le \rho$ (A.3)
```

which leads to

这导致

```
$w^T x_1 - q ||w|| \ge \rho ||w||$
$w^T x_2 - q ||w|| \le \rho ||w||$. (A.4)
```

Define $b = -q ||w||$, and constrain $w$ by requiring that its magnitude satisfy:

定义 $b = -q ||w||$，并通过要求 $w$ 的模长满足以下条件来约束 $w$：

```
$||w|| = \frac{1}{\rho}$. (A.5)
```

Now we have two equations that describe behavior for any points in class 1 or class 2:

现在我们有两个方程，描述类 1 或类 2 中任何点的行为：

```
$w^T x_1 + b \ge 1$
$w^T x_2 + b \le 1$. (A.6)
```

We seek the line that maximizes the margin, $\rho$, as illustrated in Figures A.1. Eq. A.5 shows that this is the same as finding the projection vector $w$ whose magnitude is minimal. That is, we seek the $w$ that minimizes $w^T w$. We have seen the derivative of a quadratic form before, and we know that the null vector would minimize this, providing a trivial and useless solution. Some constraints are needed.

我们寻求最大化间隔 $\rho$ 的直线，如图 A.1 所示。等式 A.5 表明，这等同于寻找模长最小的投影向量 $w$。也就是说，我们寻求最小化 $w^T w$ 的 $w$。我们以前见过二次型的导数，并且知道零向量将最小化它，提供一个平凡且无用的解。需要一些约束。

Define a label $y_i$ for the point $x_i$ as,

为点 $x_i$ 定义标签 $y_i$ 如下，

```
$y_i = \begin{cases} 1 & \text{if } x_i \in I_1 \\ -1 & \text{if } x_i \in I_2. \end{cases} (A.7)$
```

