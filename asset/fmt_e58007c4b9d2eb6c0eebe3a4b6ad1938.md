
```c
public RMatrix ReplaceRow(RVector vec, int m)
{
    if (m < 0 || m > nRows)
    {
        throw new Exception("*m-th row is out of range!");
    }
    if (vec.GetVectorSize() != nCols)
    {
        throw new Exception("*Vector ndim is out of range!");
    }
    for (int i = 0; i < nCols; i++)
    {
        matrix[m, i] = vec[i];
    }
    return new RMatrix(matrix);
}
```

```c
public RMatrix ReplaceCol(RVector vec, int n)
{
    if (n < 0 || n > nCols)
    {
        throw new Exception("*n-th col is out of range!");
    }
    if (vec.GetVectorSize() != nRows)
    {
        throw new Exception("*Vector ndim is out of range!");
    }
    for (int i = 0; i < nRows; i++)
    {
      matrix[i, n] = vec[i];
    }
    return new RMatrix(matrix);
}
```

```c
public RMatrix SwapMatrixRow(int m, int n)
{
  double temp = 0.0;
  for (int i = 0; i < nCols; i++) {
    temp = matrix[m, i];
    matrix[m, i] = matrix[n, i];
    matrix[n, i] = temp;
  }
  return new RMatrix(matrix);
}

public RMatrix SwapMatrixColumn(int m, int n)
{
  double temp = 0.0;
  for (int i = 0; i < nRows; i++) {
    temp = matrix[i, m];
    matrix[i, m] = matrix[i, n];
    matrix[i, n] = temp;
  }
  return new RMatrix(matrix);
}
```

在线性代数中，线性变换可以用矩阵表示。如果 `$T$` 是一个从 `$\mathbb{R}^n$` 映射到 `$\mathbb{R}^m$` 的线性变换，且 `$\vec{x}$` 是一个具有 `$n$` 个元素的列向量，那么

> `$T(\vec{x}) = A\vec{x}$`

对于 `$m \times n$` 矩阵 `$A$`，称为 `$T$` 的变换矩阵。矩阵允许将任意变换表示为适用于计算的形式。例如，如果有一个函数形式的线性变换 `$T(x)$`，通过对标准基的每个向量应用 `$T$` 变换并将结果插入矩阵 `$A$` 的列，就可以很容易确定变换矩阵。换言之，

> `$A = [T(\vec{e}_1) \ T(\vec{e}_2) \ \dots \ T(\vec{e}_n)]$`

大多数固定原点的几何变换都是线性的，包括旋转、缩放、切切正交投影。如果仿变换不是平移，它会固定某个点，可以将该点选择为原点以变为线性变换。例如，考虑在二维欧几平面内绕原点逆时针旋转角度 `$\theta$`。函数形式为 `$x' = x \cos \theta - y \sin \theta$` 和 `$y' = x \sin \theta + y \cos \theta$`。用矩阵形式表示这些方程变为：

```
$$\begin{bmatrix} \cos\theta & -\sin\theta \\ \sin\theta & \cos\theta \end{bmatrix}$$
```

# 向量与矩阵

以下代码演示了如何在 C# 中计算变换矩阵

```csharp
public static RVector Transform(RMatrix mat, RVector vec)
{
    RVector result = new RVector(vec.GetVectorSize);
    if (!mat.IsSquared())
    {
        throw new Exception("The matrix must be squared!");
    }
    if (mat.GetNCols != vec.GetVectorSize)
    {
        throw new Exception("The dim of the vector must be equal"
        + " to the number of cols of the matrix!");
    }
    for (int i = 0; i < mat.GetNRows(); i++)
    {
        result[i] = 0.0;
        for (int j = 0; j < mat.GetNCols; j++)
        {
            result[i] += mat[i, j] * vec[j];
        }
    }
    return result;
}
```

```csharp
public static RVector Transform(RVector vec, RMatrix mat)
{
    RVector result = new RVector(vec.GetVectorSize);
    if (!mat.IsSquared())
    {
        throw new Exception("The matrix must be squared!");
    }
    if (mat.GetNRows != vec.GetVectorSize)
    {
        throw new Exception("The ndim of the vector must be equal"
        + " to the number of rows of the matrix!");
    }
    for (int i = 0; i < mat.GetNRows; i++)
    {
        result[i] = 0.0;
        for (int j = 0; j < mat.GetNCols; j++)
        {
            result[i] += vec[j] * mat[j, i];
        }
    }
    return result;
}
```

```csharp
public static RMatrix Transform(RVector v1, RVector v2)
{
    for (int j = 0; j < v1.GetVectorSize; j++)
    {
        result[j, i] = v1[i] * v2[j];
    }
    return result;
}
```

行列式是一种代数运算，它将方阵 `A` 按照特定的程序转换为标量，该程序在下文中进行了详细描述。行列式仅定义于方阵，可以表示为：

`$\det A = \begin{vmatrix} a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\ a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\ \vdots & \vdots & \ddots & \vdots \\ a_{n,1} & a_{n,2} & \cdots & a_{n,n} \end{vmatrix}$`

矩阵 `A` 的子式是某个较小方阵的行列式，该矩阵是通过删除 `A` 的行或多行及多列得到的。`$n \times n$` 方阵 `A` 的 `$M_{ij}$` 子式定义为：从 `A` 中删除第 `$i$` 行和第 `$j$` 列后形成的 `$(n-1) \times (n-1)$` 矩阵的行列式。仅从方阵 `A` 中删除一行和一列形成的子式 `$M_{ij}$` 称为一阶子式。当删除两行和两列时，方阵的 `$C_{ij}$` 称为二阶子式，依此类推。方阵 `A` 的 `$(i, j)$` 代数式是 `(-1)^{i+j}` 乘以对应的子式 `$M_{ij}$`。

`$C_{ij} = (-1)^{i+j}M_{ij}$`

`A` 的代数式或代数式矩阵通常记为 `$C$`，定义为 `$n \times n$` 矩阵，其 `$(i, j)$` 元素是 `A` 的 `$(i, j)$` 代数式。`$C$` 的转置称为 `A` 的伴随矩阵。因此，伴随矩阵是代数式矩阵的转置，如下所示：

`$A^{-1} = \frac{1}{|A|} (C_{ij})^T = \frac{1}{|A|} (C_{ji})$`

`$\begin{pmatrix} C_{11} & C_{21} & \cdots & C_{n1} \\ C_{12} & C_{22} & \cdots & C_{n2} \\ \vdots & \vdots & \ddots & \vdots \\ C_{1n} & C_{2n} & \cdots & C_{nn} \end{pmatrix}$`

`$|A|$` 是 `A` 的行列式，`$C_{ij}$` 是矩阵代数式，`$A^T$` 表示矩阵转置。

伴随矩阵用于计算方阵的逆。如果存在一个 `$n \times n$` 矩阵 `B` 使得：

`$AB = BA = I_n$`

则 `$n \times n$` 方阵 `A` 是可逆或非奇异的，其中 `$I_n$` 表示 `$n \times n$` 单位矩阵，所使用的乘法是普通的矩阵乘法。如果是如此，则矩阵 `B` 是唯一确定的，并称为 `A` 的逆，记作 `$A^{-1}$`。此时矩阵 `A` 的行列式可以用矩阵 `A` 的代数式 `$C_{ij}$` 非常简洁地表示为：

`$|A| = \sum_{i=1}^{k} a_{ij}C_{ij}$`

其中对 `$j$` 没有隐含的求和，`$C_{ij}$` 是 `$a_{ij}$` 的代数式。这一过程称为按子式展开法。

设 `A` 为 `$n \times n$` 矩阵。`$Adj(A) = \det(A)I$`，其中 `$Adj(A)$` 表示 `A` 的伴随矩阵，`$\det(A)$` 是行列式，`$I$` 是单位矩阵。如果 `$\det(A)$` 可可的，则 `A` 的逆为：

`$A^{-1} = \frac{1}{\det(A)}Adj(A)$`

作为一个简单的例子，通用 `$2 \times 2$` 矩阵的逆的计算公式如下：

`$A^{-1} = \begin{bmatrix} a & b \\ c & d \end{bmatrix}^{-1} = \frac{1}{ad-bc}\begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$`

对矩阵执行所有操作的代码列如下。
