

将这些元素放入名为 Numbers 的数组中。现在，我们可以拥有另一个包含 10 个元素的数组，用于显示列表 Numbers 中每个值的频率。

```
void FrequencyCount(int Freq[10], int A[100])
{
   int i;
   for(i = 0; i < 10; i++)
      Freq[i] = 0;
   for(i = 0; i < 100; i++)
      Freq[A[i]]++;
}
```

在图 2.26 中，Frequency[0] 表示 0 在数组 Numbers 中出现了一次，1 出现了 20 次，2 出现了 5 次，依此类推。

![](img/a99ec79093c067f0bed8f1086197950e_82_0.png)

图 2.26 0 到 9 范围内数字的频率统计

此概念将在第 2.11.3 节中用于快速转置。

## 2.11 稀疏矩阵

矩阵是一种非常常用的数学对象。要表示矩阵，我们需要一个二维数组，使用两个不同的索引来引用行和列。用于矩阵操作的表示应该是高效的，以便空间和时间需求尽可能少。

在许多应用中，算法设计的关键方面是空间考量。因此，如果矩阵很大，开发者必须注意矩阵的表示方式。在许多情况下，矩阵的大小非常大，但其中大部分元素都是 0（不重要或无关数据）。只有很小一部分矩阵实际上被使用。这种类型的矩阵称为稀疏矩阵，因为矩阵被数据稀疏地填充，大多数位置是空的或包含无关数据。在这种情况下，必须使用替代表示来表示和存储矩阵，以实现良好的空间利用率。这种表示避免了与 0 相关的操作（0 的加法或乘法）。因此，如果稀疏矩阵使用替代表示而非常规方式存储，则可以实现良好的时间复杂度和高效的存储。

图 2.27 说明了逻辑矩阵 LA 和 LB。

![](img/a99ec79093c067f0bed8f1086197950e_83_0.png)

图 2.27 稀疏逻辑矩阵

在图 2.27 中，矩阵 LA 相对于 1 是稀疏的，相对于 0 是稠密的，而 LB 相对于 0 是稀疏的，相对于 1 是稠密的。

对于 m 行 n 列的矩阵，如果 m = n，则该矩阵称为方阵（图 2.28）。

![](img/a99ec79093c067f0bed8f1086197950e_83_1.png)

图 2.28 稀疏方阵

图 2.28 中的矩阵 A 有许多 0 项，可以称为稀疏矩阵。没有精确的定义说明何时矩阵是稀疏的，何时不是。在这里，0 可能表示无关数据，或某些实验连续读数或连续位置没有变化。

图 2.29 和 2.30 展示了两种常见的 n 阶稀疏矩阵类型。

![](img/a99ec79093c067f0bed8f1086197950e_83_2.png)

图 2.29 稀疏三角矩阵

图 2.30 稀疏三对角矩阵

在图 2.29 的矩阵中，主对角线以上的所有项都是 0。所有非零项仅出现在主对角线上或下方的矩阵称为三角矩阵。

非零项只能出现在对角线上或对角线上方或下方紧邻元素上的矩阵称为三对角矩阵（图 2.30）。

### 2.11.1.1 稀疏矩阵表示

稀疏矩阵需要一种替代形式的表示。在处理大型稀疏矩阵时，我们需要考虑一种替代表示，仅存储非零元素以实现更好的空间利用率。

矩阵的每个元素都由其行和列位置唯一标识。因此，三元组 (i, j, value) 可以轻松表示矩阵的非零元素。

在矩阵的稀疏表示中，有三列。在第一行中，我们始终在列 1、2 和 3 中分别指定行数、列数和非零元素数（No_Of_NonZeroValues）。从第二行开始，我们按三元组 (i, j, value) 存储每个非零元素。因此，在稀疏矩阵中，有三列和 (No_Of_NonZeroValues + 1) 行。通常，为了空间可靠性，3 x (No_Of_NonZeroValues + 1) 应始终小于或等于 m x n，其中 m = 行数，n = 列数。

No_Of_NonZeroValues = 非零元素的数量

简而言之，对于替代表示，我们应有

3 x (No_Of_NonZeroValues + 1) <= m x n

考虑图 2.31(a) 中的矩阵 A。在 42 个元素中，8 个成员是非零的。对于常规表示，我们需要 42 个内存位置来存储矩阵（假设每个元素一个位置），而对于如图 2.31(b) 所示的替代表示，我们需要 (8 + 1) x 3，即 27 个内存位置。

![](img/a99ec79093c067f0bed8f1086197950e_84_0.png)

图 2.31 稀疏矩阵表示（a）稀疏矩阵 A（b）稀疏矩阵 A 的替代表示

在有限元分析、图像处理、仿真等应用中，矩阵的大小为 2048 x 2048 或更高。当 m 和 n 是大数且 No_Of_NonZeroValues 远小于它们时，替代表示可以节省大量内存和处理时间。

程序代码 2.8 表示稀疏矩阵的 ADT。

```
PROGRAM CODE 2.8
class Sparse_Matrix
{
    private:
    const int Max = 20;
    int S_Mat[Max][3];
    public:
    void Read_SparseMatrix();
    Sparse_Matrix Simple_Transpose();
    Sparse_Matrix Fast_Transpose();
    Sparse_Matrix Add_SparseMatrix(Sparse_Matrix B);
    Sparse_Matrix Mpy_SparseMatrix(Sparse_Matrix B);
};
```

### 2.11.2 稀疏矩阵加法

除了替代表示，我们还需要为常见的矩阵运算（如加法、减法、转置、逆、乘法和除法）设计合适的算法。让我们讨论其中两种——加法和转置。

设 A 和 B 为两个待加的稀疏矩阵，如图 2.32 所示。

![](img/a99ec79093c067f0bed8f1086197950e_85_0.png)

图 2.32 稀疏矩阵加法

只有当两个矩阵的大小相同时，才能相加。设 A_ROW 和 B_ROW 分别为矩阵 A 和 B 的行数。M 和 N 分别是 A 和 B 中非零元素的数量。C 是结果稀疏矩阵。算法 2.2 描述了添加两个稀疏矩阵的过程。

### 算法 2.2

```
1. Let A, B be the matrices to be added and stored in C
2. Let M and N be number of non-zero entries in A and B respectively.
3. Let i, j, and k be the three index variables used for the rows of A, B, and C respectively.
4. Let i = j = k = 1, M = A[0][2], N = B[0][2]
5. C[0][0] = A[0][0]
   C[0][1] = A[0][1]
   C[0][2] = A[0][2]
6. while (i <= M and j <= N) do
   begin
   if (A[i][0] = B[j][0]) //if1
   if (A[i][1] = B[j][1]) //if2
   then
   begin
   C[k][0] = A[i][0]
   C[k][1] = A[i][1]
   C[k][2] = A[i][2] + B[j][2]
   i = i + 1, j = j + 1, k = k + 1
   end
   else if (A[i][1] < B[j][1]) //if3 and else for if2
   then
   begin
   C[k][0] = A[i][0]
   C[k][1] = A[i][1]
   C[k][2] = A[i][2]
   k = k + 1, i = i + 1
   end
   else //else for if3
   begin
   C[k][0] = B[j][0]
   C[k][1] = B[j][1]
   C[k][2] = B[j][2]
   j = j + 1, k = k + 1
   end
   else if (A[i][0] < B[j][0]) //if4 and else for if1
   then
   begin
   C[k][0] = A[i][0]
   C[k][1] = A[i][1]
   C[k][2] = A[i][2]
   k = k + 1, i = i + 1
   end
   else
   begin
   C[k][0] = B[j][0]
   C[k][1] = B[j][1]
   C[k][2] = B[j][2]
   k = k + 1, j = j + 1
   end
end while
7. while(i <= M) do
begin
C[k][0] = A[i][0]
C[k][1] = A[i][1]
C[k][2] = A[i][2]
k = k + 1, i = i + 1
end
8. while(j <= N) do
begin
C[k][0] = B[j][0]
C[k][1] = B[j][1]
C[k][2] = B[j][2]
k = k + 1, j = j + 1
end
9. C[0][2] = k
10. stop
//else for if4
```

程序代码 2.9 包含稀疏矩阵的 ADT 以及根据算法 2.2 进行两个稀疏矩阵相加的函数。

```
PROGRAM CODE 2.9

Sparse_Matrix Sparse_Matrix :: Add_SparseMatrix
(Sparse_Matrix B)
{
Sparse_Matrix C;
int i, j, k, Row1, Row2, Col1, Col2, M1, M2;
Row1 = S_Mat[0][0];
Col1 = S_Mat[0][1];
M1 = S_Mat[0][2];
Row2 = B.S_Mat[0][0];
Col2 = B.S_Mat[0][1];
M2 = B.S_Mat[0][2];
if(Row1 == Row2 && Col1 == Col2)
// checking dimensions if1
{
i = j = k = 1;
C.S_Mat[0][0] = S_Mat[0][0];
C.S_Mat[0][1] = S_Mat[0][1];
```

