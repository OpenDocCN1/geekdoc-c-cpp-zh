


## 第18章

\((iii)\quad \begin{pmatrix}\frac12&\frac12&-\frac12&-\frac12\\[2pt]\frac{1}{3\sqrt2}&\frac23&\frac23&\frac{1}{3\sqrt2}\\[2pt]\frac12&-\frac12&\frac12&-\frac12\\[2pt]\frac23&-\frac{1}{3\sqrt2}&-\frac{1}{3\sqrt2}&\frac23\end{pmatrix}\begin{pmatrix}2&0&0&0\\0&1&0&0\\0&0&1&0\\0&0&0&2\end{pmatrix}\begin{pmatrix}\frac12&\frac{1}{3\sqrt2}&\frac12&\frac23\\[2pt]\frac12&\frac23&-\frac12&-\frac{1}{3\sqrt2}\\[2pt]-\frac12&\frac23&\frac12&-\frac{1}{3\sqrt2}\\[2pt]-\frac12&\frac{1}{3\sqrt2}&-\frac12&\frac23\end{pmatrix}.\)

\(18.2.\) (ii) \(\begin{pmatrix}\frac{1}{\sqrt2}&\frac12&-\frac{1}{\sqrt6}&-\frac{1}{2\sqrt3}\\[2pt]\frac{1}{\sqrt2}&-\frac12&\frac{1}{\sqrt6}&\frac{1}{2\sqrt3}\\[2pt]0&\frac12&\frac{2}{\sqrt6}&-\frac{1}{2\sqrt3}\\[2pt]0&\frac12&0&\frac{3}{2\sqrt3}\end{pmatrix}\begin{pmatrix}4&0&0&0\\0&4&0&0\\0&0&8&0\\0&0&0&8\end{pmatrix}\begin{pmatrix}\frac{1}{\sqrt2}&\frac{1}{\sqrt2}&0&0\\[2pt]\frac12&-\frac12&\frac12&\frac12\\[2pt]-\frac{1}{\sqrt6}&\frac{1}{\sqrt6}&\frac{2}{\sqrt6}&0\\[2pt]-\frac{1}{2\sqrt3}&\frac{1}{2\sqrt3}&-\frac{1}{2\sqrt3}&\frac{3}{2\sqrt3}\end{pmatrix}.\)

**18.5. (i)** \(\begin{pmatrix}0&\sqrt{\frac23}&\frac{1}{\sqrt3}\\[2pt]\frac{1}{\sqrt2}&-\frac12\sqrt{\frac23}&\frac{1}{\sqrt3}\\[2pt]\frac{1}{\sqrt2}&\frac12\sqrt{\frac23}&-\frac{1}{\sqrt3}\end{pmatrix}\begin{pmatrix}\frac{2}{\sqrt2}&\frac{1}{\sqrt2}&\frac{1}{\sqrt2}\\[2pt]0&\sqrt{\frac32}&\frac12\sqrt{\frac23}\\[2pt]0&0&\frac{2}{\sqrt3}\end{pmatrix}.\)

\((ii)\quad \begin{pmatrix}\frac12&\frac{1}{2\sqrt{51}}\\[2pt]\frac12&\frac{9}{2\sqrt{51}}\\[2pt]\frac12&\frac{1}{2\sqrt{51}}\\[2pt]-\frac12&\frac{11}{2\sqrt{51}}\end{pmatrix}\begin{pmatrix}2&-\frac12\\[2pt]0&\frac{51}{2\sqrt{51}}\end{pmatrix}.\)

\((iii)\quad \simeq\begin{pmatrix}0.500&0.070&-0.530\\0.500&0.630&-0.175\\0.500&0.070&0.822\\-0.500&0.770&0.117\end{pmatrix}\begin{pmatrix}2.000&-0.500&0.000\\0.000&3.571&-0.560\\0.000&0.000&3.699\end{pmatrix}.\)

## 第19章

# 奇异值分解

在本章中，我们将发展另一种分解类型，它是第18章讨论的对角化过程的推广。这种分解适用于任意实 $m \times n$ 矩阵 $A$，在文献中被称为*奇异值分解（SVD）*。除了求解线性方程组外，SVD 在数据压缩、降噪、存储、估计矩阵的秩以及数字化信息传输等众多领域都有广泛的应用。在陈述本章的主要结果之前，让我们回顾以下步骤：

+   S1  对于 $m \times n$ 矩阵 $A$，$m \times m$ 矩阵 $AA^t$ 和 $n \times n$ 矩阵 $A^tA$ 是对称的。
+   
+   S2  根据[问题 17.8]，$A^tA$ 的特征值是实数且非负。我们假设特征值 $\lambda_1,\cdots,\lambda_r$ 非零，并按递减顺序排列，即 $\lambda_1 \geq \lambda_2 \geq \cdots \geq \lambda_r > 0$。
+   
+   S3  根据[定理 18.2]，矩阵 $A^tA$ 有 $n$ 个标准正交特征向量 $v^1,\cdots,v^n$。设 $v^1,\cdots,v^r$ 是对应于 $A^tA$ 的特征值 $\lambda_1,\cdots,\lambda_r$ 的那些特征向量。显然，[问题 11.3] 的直接推广意味着 $r$ 是 $A^tA$ 的秩，这与 $A$ 的秩相同。
+   
+   S4  由于 $AA^tAv^i=A(\lambda_i v^i)=\lambda_iAv^i$，因此 $v^i$ 是 $A^tA$ 的特征向量，这意味着 $Av^i$ 是 $AA^t$ 的特征向量，且具有相同的特征值 $\lambda_i$。
+   
+   S5  由[问题 17.8]可得 $\|Av^i\|_2=\sigma_i\|v^i\|_2$，其中 $\sigma_i=\sqrt{\lambda_i}$，$i=1,\cdots,r$。这些 $\sigma_i$ 被称为 $A$ 的*奇异值*。显然，$\sigma_1\geq\sigma_2\geq\cdots\geq\sigma_r>0$。
+   
+   S6. 定义 $u^i=Av^i/\sigma_i$，$i=1,\cdots,r$。那么显然

$$(u^i,u^i)=\frac{1}{\lambda_i}(Av^i,Av^i)=\frac{\lambda_i}{\lambda_i}(v^i,v^i)=1,$$

即向量 $u^i$（$i=1,\cdots,r$）也是标准化的。进一步，我们有

$$(u^i)^tAv^j=(Av^i/\sigma_i)^tAv^j=\frac{1}{\sigma_i}(v^i)^tA^tAv^j=\frac{1}{\sigma_i}(v^i)^t\lambda_jv^j=\frac{\lambda_j}{\sigma_i}(v^i)^tv^j,$$

这意味着对所有 $1\leq i,j\leq r$，当 $i\neq j$ 时 $(u^i)^tAv^j=0$，当 $i=j$ 时为 $\sigma_i$。这意味着集合 $\{u^1,\cdots,u^r\}$ 是列空间 $A$ 的一组标准正交基。

S7. 矩阵 \(V=(v^1,\cdots,v^r|v^{r+1},\cdots,v^n)\) 正交对角化
\(A^tA\)；我们利用注 14.2 将集合 \(\{u^1,\cdots,u^r\}\) 扩展为 \(\{u^1,\cdots,u^r|u^{r+1},\cdots,u^m\}\)，它构成 \(R^m\) 的一组标准正交基，并构造矩阵
\(U=(u^1,\cdots,u^r|u^{r+1},\cdots,u^m)\)；我们如下定义矩阵 \(\Sigma\)：

\(\Sigma=\left(\begin{array}{ c c c }
D_{rr} & \vdots & 0_{r,n-r} \\
\cdots\cdots\cdots & \vdots & \cdots\cdots\cdots \\
0_{m-r,r} & \vdots & 0_{m-r,n-r}
\end{array}\right);\)

这里，\(D_{rr}\) 是对角矩阵

\(D_{rr}=\left(\begin{array}{ c c c c }
\sigma_1 & 0 & \cdots & 0 \\
0 & \sigma_2 & \cdots & 0 \\
\vdots & \vdots & \ddots & \cdots \\
0 & 0 & \cdots & \sigma_r
\end{array}\right)\)

且 \(0_{k\ell}\) 是 \(k\times\ell\) 零矩阵。

S8. 我们断言 \(U\Sigma=AV\)。事实上，我们有

\(U\Sigma=(\sigma_1u^1,\cdots,\sigma_ru^r|0,\cdots,0)\)
\(=(Av^1,\cdots,Av^r|Av^{r+1},\cdots,Av^n)=AV.\)

S9. 利用 \(V\) 的正交性，可得

\(A=U\Sigma V^t.\) (19.1)

# 定理 19.1. 每个秩为 \(r\) 的 \(m\times n\) 矩阵 \(A\) 都有奇异值分解，即 (19.1) 成立。

# 证明. 步骤 S1–S9 给出了 (19.1) 的构造性证明。 \(\blacksquare\)

显然，对于对称矩阵，只要特征值按递减顺序排列，奇异值分解与正交对角化是相同的。

# 例 19.1. 我们将求矩阵

\(A=\left(\begin{array}{ c c c c }
2 & 2 & 1 & 0 \\
1 & -1 & 0 & 1
\end{array}\right).\)

的奇异值分解。

为此，我们注意到

\(A^tA=\left(\begin{array}{ c c c c }
5 & 3 & 2 & 1 \\
3 & 5 & 2 & -1 \\
2 & 2 & 1 & 0 \\
1 & -1 & 0 & 1
\end{array}\right).\)

对于矩阵 $A^tA$，特征值和相应的特征向量分别为 $\lambda_1=9,\lambda_2=3,\lambda_3=0,\lambda_4=0$ 和 $(2,2,1,0)^t,(1,-1,0,1)^t,(-1-1,4,0)^t,(-1,1,0,2)^t$。因此，$\sigma_1=3,\sigma_2=\sqrt{3}$，

$$\Sigma=\begin{pmatrix}3&0&0&0\\0&\sqrt{3}&0&0\end{pmatrix}\quad\text{and}\quad V=\begin{pmatrix}\frac23&\frac1{\sqrt3}&\frac1{3\sqrt2}&\frac1{\sqrt6}\\\frac23&-\frac1{\sqrt3}&-\frac1{3\sqrt2}&\frac1{\sqrt6}\\\frac13&0&\frac4{3\sqrt2}&0\\0&\frac1{\sqrt3}&0&\frac2{\sqrt6}\end{pmatrix}.$$

我们还要计算

$$u^1=Av^1/\sigma_1=\begin{pmatrix}1\\0\end{pmatrix}\quad\text{and}\quad u^2=Av^2/\sigma_2=\begin{pmatrix}0\\1\end{pmatrix},$$

因此

$$U=\begin{pmatrix}1&0\\0&1\end{pmatrix}.$$

由 (19.1) 现在可得

$$\begin{pmatrix}2&2&1&0\\1&-1&0&1\end{pmatrix}=\begin{pmatrix}1&0\\0&1\end{pmatrix}\begin{pmatrix}3&0&0&0\\0&\sqrt3&0&0\end{pmatrix}\begin{pmatrix}\frac23&\frac23&\frac13&0\\\frac1{\sqrt3}&-\frac1{\sqrt3}&0&\frac1{\sqrt3}\\-\frac1{3\sqrt2}&-\frac1{3\sqrt2}&\frac4{3\sqrt2}&0\\-\frac1{\sqrt6}&\frac1{\sqrt6}&0&\frac2{\sqrt6}\end{pmatrix}.$$

**注 19.1.** 由 (19.1) 可直接得到 $A^t=V\Sigma^tU^t$。因此，根据*例 19.1*，我们有如下分解：

$$\begin{pmatrix}2&1\\2&-1\\1&0\\0&1\end{pmatrix}=\begin{pmatrix}\frac23&\frac1{\sqrt3}&-\frac1{3\sqrt2}&-\frac1{\sqrt6}\\\frac23&-\frac1{\sqrt3}&-\frac1{3\sqrt2}&\frac1{\sqrt6}\\\frac13&0&\frac4{3\sqrt2}&0\\0&\frac1{\sqrt3}&0&\frac2{\sqrt6}\end{pmatrix}\begin{pmatrix}3&0\\0&\sqrt3\\0&0\\0&0\end{pmatrix}\begin{pmatrix}1&0\\0&1\end{pmatrix}.$$

同样的分解也可以直接按照上述步骤 S1=S9 得到。

奇异值分解以自然的方式将 $A$ 的四个基本子空间联系起来。我们在下面的定理中陈述并证明这一结果。

# **定理 19.2.**

设 $m\times n$ 矩阵 $A$ 的秩为 $r$，并且设 $U\Sigma V^t$ 是它的奇异值分解；则以下结论成立：

+   (i) 集合 $\{u^1,\cdots,u^r\}$ 是 $C(A)$ 的一组标准正交基
+   
+   (ii) 集合 $\{u^{r+1},\cdots,u^m\}$ 是 $C(A)^\perp=\mathcal{N}(A^t)$ 的一组标准正交基

