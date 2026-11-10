| Source Code | Partition | Transformed Code |
|---|---|---|
| `for (i=1; i<=N; i++)`<br>`  Y[i] = Z[i]; /*s1*/`<br>`for (j=1; j<=N; j++)`<br>`  X[j] = Y[j]; /*s2*/`<br><br>[依赖关系示意图：s₁ 与 s₂ 的迭代点及箭头] | Fusion<br>`s₁: p = i`<br>`s₂: p = j` | `for (p=1; p<=N; p++){`<br>`  Y[p] = Z[p];`<br>`  X[p] = Y[p];`<br>`}` |
| `for (p=1; p<=N; p++){`<br>`  Y[p] = Z[p];`<br>`  X[p] = Y[p];`<br>`}`<br><br>[依赖关系示意图：s₁ 与 s₂ 的迭代点及箭头] | Fission<br>`s₁: i = p`<br>`s₂: j = p` | `for (i=1; i<=N; i++)`<br>`  Y[i] = Z[i]; /*s1*/`<br>`for (j=1; j<=N; j++)`<br>`  X[j] = Y[j]; /*s2*/`<br><br>[依赖关系示意图：s₁ 与 s₂ 的迭代点及箭头] |
| `for (i=1; i<=N; i++) {`<br>`  Y[i] = Z[i];   /*s1*/`<br>`  X[i] = Y[i-1]; /*s2*/`<br>`}`<br><br>[依赖关系示意图：s₁ 与 s₂ 的迭代点及箭头] | Re-indexing<br>`s₁: p = i`<br>`s₂: p = i − 1` | `if (N>=1) X[1]=Y[0];`<br>`for (p=1; p<=N-1; p++){`<br>`  Y[p]=Z[p];`<br>`  X[p+1]=Y[p];`<br>`}`<br>`if (N>=1) Y[N]=Z[N];`<br><br>[依赖关系示意图：s₁ 与 s₂ 的迭代点及箭头] |
| `for (i=1; i<=N; i++)`<br>`  Y[2*i] = Z[2*i]; /*s1*/`<br>`for (j=1; j<=2*N; j++)`<br>`  X[j]=Y[j];      /*s2*/`<br><br>[依赖关系示意图：s₁ 与 s₂ 的迭代点及箭头] | Scaling<br>`s₁: p = 2 * i`<br>`(s₂: p = j)` | `for (p=1; p<=2*N; p++){`<br>`  if (p mod 2 == 0)`<br>`    Y[p] = Z[p];`<br>`  X[p] = Y[p];`<br>`}`<br><br>[依赖关系示意图：s₁ 与 s₂ 的迭代点及箭头] |

Figure 11.35: Primitive affine transforms (I)