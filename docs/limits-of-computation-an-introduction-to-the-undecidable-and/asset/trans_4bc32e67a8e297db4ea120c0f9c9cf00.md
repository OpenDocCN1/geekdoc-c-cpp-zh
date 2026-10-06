
这些内容可能很难理解。如果我们用特殊语言 $L_\varepsilon = \{\varepsilon\}$，那么：

$L_1/L_\varepsilon = L_1$

$L_1 \setminus L_2 = L_2$

$L_i/L_1 = L_\varepsilon$ 或 $\varnothing$（取决于 $\varepsilon$ 是否在 $L_1$ 中）

$L_i/\Sigma^* = \text{Prefix}(L_1) = \{ \text{以 $L_i$ 中的元素开头；删除右侧的任何字符}\}$

$\Sigma^* \setminus L_2 = \text{Suffix}(L_2) = \{ \text{以 $L_2$ 中的元素开头；删除左侧的任何字符}\}$

# 示例

$(01)^*/1 = (01)^0$

$(01)^*/11 = \varnothing$

$0^*\0*1^* = 0*1^*$

$0^*1*0*1^* = 1^*$

关于符号说明：01 是一个字符串，但 $(01)^*$ 和 $0*1^*$ 表示字符串集合，或者在我们符号表示中表示语言。（如果这是一门形式语言课程，我们会说 $(01)^*$ 和 $01^*$ 是具有关联语言的正则表达式，但在这里我们避免对正则表达式的讨论。）

因此，可以说 $(01)^*/1$ 是一个语言，而 1 是一个字符串，但该操作作用于两个语言。我们会说 1 可以代表字符串 1 和仅包含一个字符串的语言（或 $L_i = \{1\}$），并且从上下文中清楚看出使用的是哪一个。

人们还可以洗牌语言。$L_1$ 和 $L_2$ 的**洗牌**（shuffle）由通过洗牌 $L_1$ 中的任意字符串 $v$ 和 $L_2$ 中的任意字符串 $w$ 形成的所有字符串组成。这是可以写成形式 $v_1w_1v_2w_2...nv_n$ 的字符串集合，其中 $n \ge 1$ 且 $v_1, \dots, v_n$ 是字符串，使得拼接 $v_1 \dots v_n$ 属于 $L_1$，且 $w_1, \dots, w_n$ 是字符串，使得 $w_1 \dots w_n$ 属于 $L_2。

# 练习

- 1. 为这些新的字符串操作构造合理的定义。结果可能是一个字符串，也是一个字符串集合（一个语言）：
   - a. Permute(w) = 重新排列 $w$ 的字符。
   - b. Half(w) = 去掉一半字符的 $w$。
   - c. First_half(w) = ?

这些定义可以扩展到语言吗？如果是，如何扩展？如果对于 $\Sigma = \{a, b\}$ 上以 aa 开头并 bb 结尾的字符串 $L$：

   - a. Permute (L) 是什么？
   - b. Half (L) 是什么？
   - c. First_half (L) 是什么？

- 2. 考虑这三个语言和这三个同态（$\Sigma = \{a, b, c\}$）。

   - $L_1$ = 以 aa 开头并 bb 结尾的字符串
   - $L_2$ = 具有偶数个 a 的字符串
   - $L_3$ = 不包含子字符串 bbb 的字符串

   - $h_1: a \to bb, b \to ab, c \to cc$
   - $h_2: a \to \varepsilon, b \to abc, c \to \varepsilon$
   - $h_3: a \to b, b \to c, c \to aa$

   对于 $i = 1, 2, 3$ 和 $j = 1, 2, 3，$h_j(L_i)$ 是什么？

- 3.
   - a. 定义一个语言 $L_{smaller-than-w}$。如果 $w = aabb$，根据你的定义，$L_{smaller-than-w}$ 是什么？
   - b. 对于满足 $r < s$ 和 $v < w$ 的字符串 $r, s, v, w$，证明或反驳：
      - i. $rv < sw$
      - ii. $v^R < w^R$
      - iii. $w^R < v^R$
      - iv. 对于 $\text{Prefix}(v)$ 中的任何字符串 $x$，$x < v$

- 4. 假设 $\Sigma = \{a, b, c\}$ 且 $v = v_1, \dots, v_\mu, n = 3, v = abc$。给出将 $v$ 分为三个字符串的所有可能划分，$v = v_1v_2v_3$。

- 5. 令 $\Sigma = \{a, b, c\}$,语言 $L_\varepsilon = \{\varepsilon\}, L_\emptyset = \emptyset, L_{3k} = \{w|w \text{ 包含一个 a}\}$（对于某些 $k$）。找到：
   - a. $L_{3k}$
   - b. $L_\emptyset$
   - c. $L_{3k}$
   - d. $L_a$
   - e. $\text{Prefix}(L_{3k})$
   - f. $\text{Suffix}(L_a)$
