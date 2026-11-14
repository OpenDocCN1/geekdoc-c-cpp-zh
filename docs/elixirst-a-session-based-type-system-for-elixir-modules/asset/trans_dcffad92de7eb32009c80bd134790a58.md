

**定义 A.2（绑定变量）。**

\(\mathbf{bv}(t) \stackrel{\text{def}}{=} \begin{cases} \emptyset & t = e \text{ or } t = \text{send}(w, \{..l, \tilde{e}..\}) \text{ or } t = f(\tilde{e}) \\ \{ x \mid x \in \mathbf{bv}(t_1) \cup \mathbf{bv}(t_2) \} & t = (x = t_1; t_2) \\ \bigcup_{i \in I} \mathbf{bv}(t_i) \cup \mathbf{vars}(\tilde{p}_i) & t = \text{receive do } (\{l_i, \tilde{p}_i \rightarrow t_i\})_{i \in I} \text{end} \\ \bigcup_{i \in I} \mathbf{bv}(t_i) \cup \mathbf{vars}(p_i) & t = \text{case } e \text{ do } (p_i \rightarrow t_i)_{i \in I} \text{end} \end{cases}\)

**定义 A.3（变量替换）。**

\( e \lfloor e' / a \rfloor \stackrel{\text{def}}{=} \begin{cases} e' & e = x \\ y & e = y, y \neq x \\ b & e = b \\ e_1 \lfloor e' / a \rfloor \diamond e_2 \lfloor e' / a \rfloor & e = e_1 \diamond e_2 \\ \text{not } (e' \lfloor e' / a \rfloor) & e = \text{not } e' \\ \{ e_1 \lfloor e' / a \rfloor \diamond e_2 \lfloor e' / a \rfloor \} & e = \{ e_1 \diamond e_2 \} \\ \{ e_1 \lfloor e' / a \rfloor, \dots, e_n \lfloor e' / a \rfloor \} & e = \{ e_1, \dots, e_n \} \end{cases}\)

\( t \lfloor e' / a \rfloor \stackrel{\text{def}}{=} \begin{cases} \text{send}(w \lfloor e' / a \rfloor, \{..l, e_1 \lfloor e' / a \rfloor, \dots, e_n \lfloor e' / a \rfloor \}) & t = \text{send}(w, \{..l, e_1, \dots, e_n\}) \\ \text{receive do } (\{l_i, \tilde{p}_i \rightarrow t_i \lfloor e' / a \rfloor \})_{i \in I} \text{end} & t = \text{receive do } (\{l_i, \tilde{p}_i \rightarrow t_i\})_{i \in I} \text{end} \\ f (e_1 \lfloor e' / a \rfloor, \dots, e_n \lfloor e' / a \rfloor) & t = f (e_1, \dots, e_n) \\ \text{case } e \lfloor e' / a \rfloor \text{ do } (p_i \rightarrow t_i \lfloor e' / a \rfloor)_{i \in I} \text{end} & t = \text{case } e \text{ do } (p_i \rightarrow t_i)_{i \in I} \text{end} \\ y = t_1 \lfloor e' / a \rfloor; t_2 \lfloor e' / a \rfloor & t = (y = t_1; t_2), a \neq y \end{cases}\)

**定义 A.4（类型）。** 该偏函数定义基本值的类型。

\(\text{type}(\text{boolean}) \stackrel{\text{def}}{=} \text{boolean} \quad \text{type}(\text{number}) \stackrel{\text{def}}{=} \text{number}\)
\(\text{type}(\text{atom}) \stackrel{\text{def}}{=} \text{atom} \quad \text{type}(t) \stackrel{\text{def}}{=} \text{pid}, \text{ where } t \text{ is a pid instance}\)

**定义 A.5（变量模式）。** 从给定模式 \(p\) 计算有序变量集。

\(\mathbf{vars}(\tilde{p}) \stackrel{\text{def}}{=} \mathbf{vars}(p_1, \dots, p_n) \stackrel{\text{def}}{=} \mathbf{vars}(p_1) \cup \dots \cup \mathbf{vars}(p_n)\)

\(\mathbf{vars}(p) \stackrel{\text{def}}{=} \begin{cases} \emptyset & p = b \\ \{ x \} & p = x \\ \mathbf{vars}(w_1) \cup \mathbf{vars}(w_2) & p = [ w_1 \mid w_2 ] \\ \bigcup_{i \in 1..n} \mathbf{vars}(w_i) & p = [ w_1, \dots, w_n ] \end{cases}\)

**定义 A.6（函数详情）。** 我们可以从函数列表（\(\tilde{Q}\)）中提取函数详情（即 params、body、param_types、return_type、dual），并使用集合推导式构建映射，如下所示。函数列表（\(\tilde{Q}\)）可能包含公共（\(\tilde{D}\)）和私有（\(\tilde{P}\)）函数。

\(\mathbf{details}(\tilde{Q}) \stackrel{\text{def}}{=} \left\{ f/n : \left[ \begin{array}{l} \text{"dual"} = y, \text{params} = \tilde{x}, \\ \text{param\_types} = \tilde{T}, \\ \text{return\_type} = T, \\ \text{body} = t \end{array} \right] \mid \dots \right\} \cup \dots \)

**定义 A.7（函数名和元数）。** 该定义获取所有公共函数名及其元数的集合。

\(\mathbf{functions}(\tilde{D}) \stackrel{\text{def}}{=} \left\{ f/n \mid \dots \right\} \in \tilde{D} \)

**定义 A.8（所有会话类型）。** 函数 \(\mathbf{sessions}(\tilde{D})\) 返回每个带注释公共函数对应的会话类型。

```
sessions(D) def = { f/n : S | [ @session "S"; @spec... def f(y, x0, ..., xn) do t end ] D }
```

如果使用 @dual 注释代替 @session，则会自动计算双会话类型。

## 附录 B. 证明

在本附录中，我们展示了命题 1、定理 2 和定理 4 的完整证明，这些证明在正文中被省略了。

### B.1. 命题 1 的证明

在证明命题 1 之前，我们必须分析与闭合项相关的一些属性，以了解它们如何影响变量替换（定义 A.3）。引理 5 表明，如果变量 x 不存在于项 t 内部，那么，如果我们用某个值初始化 x，项 t 必须保持不变，即 t[γ/τ] = t。限制这一陈述，推论 6 表明，如果 x 不是 t 中的自由变量，则应保持相同结果。引理 7 包含两个陈述，用于比较项（或表达式）中的自由变量与包含替换的自由变量。

### 引理 5. x ∉ fv(t) ∧ x ∉ bv(t) 意味着 t[γ/τ] = t

**证明。** 对 t 的结构进行归纳。

### 推论 6. x ∉ fv(t) 意味着 t[γ/τ] = t

**证明。** 引理 5 的推论。

### 引理 7。

- i. x ∈ fv(t) 意味着 fv(t{γ/λ}) = fv(t)
- ii. x ∈ fv(e) 意味着 fv(e{γ/λ}) = fv(e)

**证明.** 分别对 t 和 e 的结构进行归纳，对应项 i 和 ii。

### 引理 8. match(p, v) = [v1 ... vn / x1 ... xn] 意味着 vars(p) = (x1, ..., xn)

**证明.** 对 p 的结构进行归纳。

- [p = b] 函数 match(b, v) 仅在 v = b 时成功。因此，根据 match 定义，当 v = b 时，

```
match(b, b) = []
```

根据 vars 定义，vars(b) = ∅，这与等式 (B.1a) 的结果一致，因为未进行变量替换。

- [p = x] 根据 match 定义，对于任意 v，

```
match(x, v) = [γ/τ]
```

根据 vars 定义，vars(x) = (x)，这与等式 (B.1b) 替换中的变量匹配。

- [p = w1 | w2] 根据 match 定义，对于 v = v1 | v2，

```
match(p, v) = match(w1, v1).match(w2, v2) = [γ1/τ1][γ2/τ2] where
```

```
match(w1, v1) = [γ1/τ1]
```

```
match(w2, v2) = [γ2/τ2]
```

通过对 w1 和 w2 从等式 (B.1d) 和 (B.1e) 进行情况分析，我们得出结论

```
vars(w1) = {x1}
```

```
vars(w2) = {x2}
```

我们需要证明 vars(w1 | w2) = {x1, x2}。根据 vars 定义和等式 (B.1f) 及 (B.1g)，vars(w1 | w2) = vars(x1) ∪ vars(x2) = {x1} ∪ {x2}。此结果与等式 (B.1c) 替换中的变量匹配。

- [p = {w1, ..., wn}] 与前一种情况类似。

### 引理 9（闭合表达式）。fv(e) = ∅ 且 e → e' 意味着 fv(e') = ∅

**证明.** 对 e 的结构进行归纳。

引理 5-9 使我们能够证明闭合项命题（命题 1）。根据该命题，我们可以说闭合项 t 在转换为某个新项 t' 并产生动作 α 后仍保持闭合。引理 9 类似；它表明表达式在归约后仍保持闭合。

### 命题 1（闭合项）。如果 fv(t) = ∅ 且 t →α t'，则 fv(t') = ∅

**证明.** 对 t 的结构进行归纳。

- [t = e] 根据规则 [rExpression] 和表达式引理，立即成立。

- [t = (x = t1 ; t2)] 鉴于 t 的当前结构，我们可以通过两种情况推导 t →α t'：

  1. [rLET1] 根据规则，t' = (x = t1' ; t2) 且

  ```
  t1 →α t1' (B.2a)
  ```

  从前提 fv(t) = ∅ 出发，根据 fv 定义，fv(t1) ∪ (fv(t2) \ {x}) = ∅，或等价地

  ```
  fv(t1) = ∅ (B.2b)
  ```

  ```
  fv(t2) \ {x} = ∅ (B.2c)
  ```

  如果将归纳假设应用于等式 (B.2a) 和 (B.2b)，我们得到

  ```
  fv(t1') = ∅ (B.2d)
  ```

  因此，根据等式 (B.2c) 和 (B.2d) 以及 fv 定义，我们得到 fv(x = t1' ; t2) = ∅，如所要求。

  2. [rLET2] 根据规则，t = (x = v ; t2) 且 t' = t2 [v/x]。由于 fv(t) = ∅，根据自由变量定义，fv(v) ∪ (fv(t2) \ {x}) = ∅，或等价地

  ```
  fv(v) = ∅ (B.2e)
  ```

  ```
  fv(t2) \ {x} = ∅ (B.2f)
  ```

  我们需要证明 fv(t') = ∅，即 fv(t2 [v/x]) = ∅，因此我们考虑两种子情况：

  a. 如果 x ∉ fv(t2)，则根据推论 6，t2 = t2 [v/x]。将其代入等式 (B.2f)，得到 fv(t2 [v/x]) = ∅，如所要求。

  b. 如果 x ∈ fv(t2)，则根据引理 7，我们得到 fv(t2 [v/x]) = fv(t2) \ {x}。如果将其代入等式 (B.2f)，则该情况成立。

- [t = send(w, (t1.e1, ..., tn.en))] 鉴于 t 的当前结构，我们可以通过两种情况推导 t →α t'：

  1. [rCHOICE1] 根据此规则，我们知道 α = τ 且

  ```
  t' = send(w, {1 ↓ v1, ..., vk-1, ek', ..., en})
  ```

  ```
  ek → ek' (B.3a)
  ```

  由于 fv(t) = ∅，根据 fv 定义

  ```
  fv(t) = ∅ (B.3b)
  ```

  ```
  fv(v_i) = ∅ for i ∈ 1..k-1 (B.3c)
  ```

  ```
  fv(e_i) = ∅ for i ∈ k..n (B.3d)
  ```

  将闭合表达式引理应用于等式 (B.3a) 和 (B.3d)，得到 fv(ek) = ∅。结合此信息与等式 (B.3b-d) 和 fv 定义，得到 fv(t') = ∅，如所要求。

