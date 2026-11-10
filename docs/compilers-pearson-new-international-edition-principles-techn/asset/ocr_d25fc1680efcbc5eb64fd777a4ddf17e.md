| Source Code | Partition | Transformed Code |
|---|---|---|
| ```c
for (i=1; i<=N; i++)
    Y[i] = Z[i]; /*s1*/
for (j=1; j<=N; j++)
    X[j] = Y[j]; /*s2*/
```
依赖关系图：白色节点 `s1` 位于上方，灰色节点 `s2` 位于下方，箭头表示映射关系。 | **Fusion**  
`s1 : p = i`  
`s2 : p = j` | ```c
for (p=1; p<=N; p++){
    Y[p] = Z[p];
    X[p] = Y[p];
}
```  
依赖关系图：`s1` 与 `s2` 映射到统一的迭代空间。 |
| ```c
for (p=1; p<=N; p++){
    Y[p] = Z[p];
    X[p] = Y[p];
}
```
依赖关系图：两个语句集合在同一迭代轴上。 | **Fission**  
`s1 : i = p`  
`s2 : j = p` | ```c
for (i=1; i<=N; i++)
    Y[i] = Z[i]; /*s1*/
for (j=1; j<=N; j++)
    X[j] = Y[j]; /*s2*/
```
依赖关系图：将合并的迭代空间拆分为两个独立的迭代空间。 |
| ```c
for (i=1; i<=N; i++) {
    Y[i] = Z[i-1]; /*s1*/
    X[i] = Y[i-1]; /*s2*/
}
```
依赖关系图：`s1` 和 `s2` 的访问位置相对偏移。 | **Re-indexing**  
`s1 : p = i`  
`s2 : p = i - 1` | ```c
if (N>=1) X[1]=Y[0];
for (p=1; p<=N-1; p++){
    Y[p]=Z[p];
    X[p+1]=Y[p];
}
if (N>=1) Y[N]=Z[N];
```
依赖关系图：通过重新索引调整两个语句的迭代位置。 |
| ```c
for (i=1; i<=N; i++) {
    Y[2*i] = Z[2*i]; /*s1*/
    for (j=1; j<=N; j++)
        X[j]=Y[j]; /*s2*/
}
```
依赖关系图：`s1` 的迭代点按比例映射到 `s2` 的迭代空间。 | **Scaling**  
`s1 : p = 2 * i`  
`(s2 : p = j)` | ```c
for (p=1; p<=2*N; p++){
    if (p mod 2 == 0)
        Y[p] = Z[p];
    X[p] = Y[p];
}
```
依赖关系图：`s1` 映射到偶数迭代点，`s2` 覆盖完整迭代空间。 |

Figure 11.35: Primitive affine transforms (I)