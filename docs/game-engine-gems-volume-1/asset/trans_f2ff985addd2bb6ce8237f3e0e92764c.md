

```cpp
{
    const float err = ComputeError(cluster->first, cluster->second, freq, aw);
    if (err > worstError)
    {
        worstError = err;
        worstValue = cluster->first;    // remember
    } // so we
    return (worstValue);
}
```

## 在集群中测量误差

如果数据构成向量场，计算样本与其代表值 v 之间的量化误差可以采用几种方法。RGB 颜色和 (x,y,z) 点是空间中的向量，构成度量空间，这意味着我们可以使用简单的距离公式。你可以选择简单的线性误差或平方误差。线性误差允许限制总偏差 ε，而不考虑误差在样本各轴上的分布情况。它看起来过于宽松，但计算速度快。

$$\varepsilon = \sum_{i=1}^{n} |v - x_i| w_{x_i}$$

有趣的是，在渲染过程中，4 个分量的 RGBA 颜色并不能有效地作为向量场，因为 alpha 的线性变化可能由于混合而导致最终颜色出现不可预测的非线性变化。换句话说，alpha 与 RGB 并非线性无关。这意味着简单的欧氏距离对 alpha 分量失去了意义。我发现处理此问题的最佳方法是为每个标量分量赋予一个权重，该权重在平方误差分析中应用。

尽管如此，这种技术仍然很有用，因为它对数据拟合提供了更大的控制力。平方误差强烈限制每个轴上的偏差，因此你可以通过用因子 s_j 对每个分量的偏差加权来控制样本中每个标量的重要性。这可以用于更重地加权 Y' 亮度分量而非色度分量（CrCb），或者以牺牲 x 和 y 为代价来改善法线的 z 分量。正如你所见，平方误差的计算成本也稍高：

\(\varepsilon = \sum_{i=1}^n \left[ \sum_{j=0}^2 (v_j - x_{ij})^2 s_j^2 \right] w_{x_i}.\)

（此处，x_ij 是样本 i 的分量 j。）

### 清单 7.3：此函数计算集群代表值与其所有样本之间的平方误差，每个分量带有一个权重。

```cpp
float ComputeError(const RepValue& v, const Samples& x, const Frequency& w, const AxisWeights& s)
{
    float err = 0.0F;
    for (size_t samp = 0; samp < x.size(); samp++)
    {
        // compute the error of a single sample
        float squaredErr = 0.0F;
        for (size_t j = 0; j < 3; j++)
        {
            const float linearErr = (v[j] - x[samp][j]);
            squaredErr += linearErr * linearErr;
        }
        const int sampleFrequency = w[x[samp]];
        err += squaredErr * sampleFrequency;
    }
    return (err);
}
```

## 将集群一分为二

此时，我们已识别出拟合效果最差的集群。我们该如何尝试将其拆分？理想情况下，最终结果将是两个集群，每个新集群中包含原集群大约一半的样本。此外，我们希望沿着集群的最长轴进行拆分，这样在对半分割时，它将平分我们能穿过数据点绘制的最长直线。这应能将样本自然地分成两个彼此最远的组。

首先，我们需要一种方法来确定一组向量的主轴。主成分分析是我们感兴趣的数学工具类别。如果我们要寻找一组完全正交的轴，可以实现特征值分解或奇异值分解等方法。然而，这超出了必要范围，因为我们从不寻找超过集群主轴的内容。一组点的主轴是其协方差矩阵的最大特征向量，可以使用幂法轻松生成。基本上，这是通过不断将向量与矩阵相乘、对其归一化，并重复该过程直到其不再改变方向来完成的。结果是矩阵中数据的主轴。

### 清单 7.4：此代码计算此集群中样本的协方差矩阵。

```cpp
void SplitCluster(const RepValue& v, const Samples& x, const Frequency& w, const AxisWeights& s, Cluster& cluster)
{
    // compute cluster center based on the samples and weights
    RepValue center = ComputeCentroid(x, w);

    // count how many pixels this cluster represents
    uint numSamplesRepresented = 0;
    for (size_t i = 0; i < x.size(); i++)
        numSamplesRepresented += w[x[i]];

    // compute covariance matrix of samples
    float covMatrix[3][3] = {{0,0,0}, {0,0,0}, {0,0,0}};
    for (size_t outer = 0; outer < 3; outer++) // rows
    {
        for (size_t inner = 0; inner < 3; inner++) // columns
        {
            // only compute the upper part and diagonal
            // and copy to the bottom part since the covariance
            if (inner >= outer)
            {
                // compute the covariance of each channel
                // with each other, across all samples.
                float deltaSum = 0.0F;
                for (size_t loop = 0; loop < x.size(); loop++)
                {
                    // weight by number of pixels this sample represents
                    deltaSum += (x[loop][inner] - center[inner]) *
                                (x[loop][outer] - center[outer]);
                }

                const float covariance = deltaSum / numSamplesRepresented;
                covMatrix[inner][outer] = covariance;
                covMatrix[outer][inner] = covariance;
            }
        }
    }
}
```

上述代码计算协方差矩阵，这是执行幂法以生成数据集第一个特征向量所必需的。幂法在某些情况下不会收敛——最具体地是当初始特征向量猜测与真实主轴正交时。在实践中，这似乎不是一个非常常见的问题，如果这让你困扰，可以将其更改为更好的方法。使用幂法的吸引力在于其实现和理解简单，并且效果相当好 [3]。

### 清单 7.5：此代码使用最多 10 次迭代的幂法来确定集群的主轴。

```cpp
// Power Method for producing the first eigenVector
float eigenVector[3] = { 1.0F, 1.0F, 1.0F};
float tempVector[3];
float lastScalar = 0.0F;

// generally converges in ~3 iterations
for (size_t iteration = 0; iteration < 10; iteration++)
{
    // vector-matrix multiply the eigenVector into tempVector
    for (size_t multiI = 0; multiI < 3; multiI++)
    {
        // store this into the temp vector until the multiplication is complete
        tempVector[multiI] = 0;
        for (size_t multiJ = 0; multiJ < 3; multiJ++)
            tempVector[multiI] +=
                eigenVector[multiJ] * covMatrix[multiI][multiJ];
    }

    // normalize the eigenvector (which is not the same as
    // normalization - a normal eigenvector has a max component of 1)
    float maxComponent = 0.0F;

    // find the maximum component in the new eigenVector
    for (size_t i = 0; i < 3; i++)
        if (fabsf(tempVector[i]) > maxComponent)
            maxComponent = fabsf(tempVector[i]);

    // perform the normalization and store into eigenVector
    for (size_t i = 0; i < 3; i++)
        eigenVector[i] = tempVector[i] / maxComponent;

    // figure out if we've converged or not
    const float absoluteRelativeError =
        fabsf((lastScalar - 1.0F / maxComponent) * maxComponent);
    if (absoluteRelativeError < 0.001F)
        break; // if our direction has not changed, stop

    // move on to another iteration, and remember what
    // eigenvalue was last iteration
    lastScalar = 1.0F / maxComponent;
}
```

一旦确定了主轴，就将所有样本投影到该轴上，并将集合拆分为位于主轴垂直平面两侧的样本。换句话说，根据每个样本沿主轴中点落在哪一侧来分配所有样本。我想我们可以尝试使用更复杂的分箱方法，但这假设每个集群中都有一个值得用来衡量误差的现实代表值。我们没有，并且选择这样的样本是 NP-hard 的——为一组样本选择代表值的问题本质上就是调色板量化！此时，重要的是集群大小大致相等，并沿主轴拆分。这些新条目是占位符——样本将很快被全局重新定位，并计算新的代表值。

### 清单 7.6：此代码沿主轴中部拆分集群，将一半样本分箱到每个新集群中。

