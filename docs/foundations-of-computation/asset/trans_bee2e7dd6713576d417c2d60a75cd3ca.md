

由于陈述 \(\forall n \in \mathbb{N}, P(n)\) 为假，其否定 \(\neg(\forall n \in \mathbb{N}, P(n))\) 为真。该否定等价于 \(\exists n \in \mathbb{N}, \neg P(n)\)。令 \(X = \{n \in \mathbb{N} \mid \neg P(n)\}\)。由于 \(\exists n \in \mathbb{N}, \neg P(n)\) 为真，我们知道 \(X\) 非空。由于 \(X\) 是非空自然数集，它有一个最小元。令 \(x\) 为 \(X\) 的最小元。即，\(x\) 是使得 \(P(x)\) 为假的最小自然数。由于我们知道 \(P(0)\) 为真，\(x\) 不能为 0。令 \(y = x - 1\)。由于 \(x \neq 0\)，\(y\) 是自然数。由于 \(y < x\)，根据 \(x\) 的定义，我们知道 \(P(y)\) 为真。我们也知道 \(\forall k \in \mathbb{N} (P(k) \rightarrow P(k + 1))\) 为真。特别是，取 \(k = y\)，我们知道 \(P(y) \rightarrow P(y + 1)\)。由于 \(P(y)\) 和 \(P(y) \rightarrow P(y + 1)\)，我们通过肯定前件推导出 \(P(y + 1)\) 为真。但 \(y + 1 = x\)，所以我们推导出 \(P(x)\) 为真。这与 \(P(x)\) 为假的事实矛盾。这个矛盾证明了定理。

定理 2.4. 设 \(P\) 是一元谓词，其论域包含自然数。假设 \(P(0)\) 为真，并且对于每个自然数 \(k \ge 0\)，\((P(0) \wedge P(1) \wedge \cdots \wedge P(k)) \rightarrow P(k + 1)\) 为真。那么 \(\forall n \in \mathbb{N}, P(n)\) 为真。

证明。假设 \(P\) 是满足定理假设的谓词，并且假设陈述 \(\forall n \in \mathbb{N}, P(n)\) 为假。我们证明这个假设会导致矛盾。令 \(X = \{n \in \mathbb{N} \mid \neg P(n)\}\)。由于假设 \(\forall n \in \mathbb{N}, P(n)\) 为假，\(X\) 非空。因此 \(X\) 有一个最小元。令 \(x\) 为 \(X\) 的最小元。假设 \(P(0)\) 为真意味着 \(0 \notin X\)，所以我们必须有 \(x > 0\)。由于 \(x\) 是使得 \(P(x)\) 为假的最小自然数，我们知道 \(P(0), P(1), \dots,\) 和 \(P(x - 1)\) 全部为真。从这一点以及 \((P(0) \wedge P(1) \wedge \cdots \wedge P(x - 1)) \rightarrow P(x)\) 这一事实，我们推导出 \(P(x)\) 为真。但这与 \(P(x)\) 为假的事实矛盾。这个矛盾证明了定理。

## 练习

- 1. 如果不假设 \(a, b,\) 和 \(c\) 互不相同，那么集合 \(\{a, b, c\}\) 实际上可能包含 1、2 或 3 个元素。集合 \(\{a, b, \{a, c\}, \{a, b, c\}\}\) 可能包含多少个不同的元素？解释你的答案。

- 2. 对下列每组集合计算 \(A \cup B, A \cap B,\) 和 \(A \setminus B\)
  - a) \(A = \{a, b, c\}, B = \emptyset\)
  - b) \(A = \{1, 2, 3, 4, 5\}, B = \{2, 4, 6, 8, 10\}\)
  - c) \(A = \{a, b\}, B = \{a, b, c, d\}\)
  - d) \(A = \{a, b, \{a, b\}\}, B = \{\{a\}, \{a, b\}\}\)

- 3. 回顾 \(\mathbb{N}\) 表示自然数集。即，\(\mathbb{N} = \{0, 1, 2, 3, \dots\}\)。
  令 \(X = \{n \in \mathbb{N} \mid n \ge 5\}\)，令 \(Y = \{n \in \mathbb{N} \mid n \le 10\}\)，并令 \(Z = \{n \in \mathbb{N} \mid n \text{ 是偶数}\}\)。求下列各集：
  - a) \(X \cup Y\)
  - b) \(X \cap Y\)
  - c) \(X \setminus Y\)
  - d) \(\mathbb{N} \setminus Z\)
  - e) \(X \cap Z\)
  - f) \(Y \cap Z\)
  - g) \(Y \cup Z\)
  - h) \(Z \setminus \mathbb{N}\)

- 4. 求 \(P(\{1, 2, 3\})\)。（它有八个元素。）

- 5. 假设 \(a\) 和 \(b\) 是对象，且 \(a \neq b\)。设 \(A\) 和 \(B\) 为由 \(A = \{\{a, b\}\}\) 和 \(B = \{a, \{a, b\}\}\) 定义的集合。判断下列每个陈述是真还是假。解释你的答案。
  - a) \(b \in A\)
  - b) \(\{a, b\} \subseteq A\)
  - c) \(\{a, b\} \subset B\)
  - d) \(\{a, b\} \in B\)
  - e) \(\{\{a, b\}\} \in A\)
  - f) \(\{a, b\} \in B\)

- 6. 由于 \(P(A)\) 是一个集合，因此可以形成集合 \(P(P(A))\)。\(P(P(\emptyset))\) 是什么？\(P(P(\{a, b\}))\) 是什么？（它有十六个元素。）

- 7. 在英文句子 “She likes men who are tall, dark, and handsome” 中，她喜欢的是男人集合的交集还是并集？句子 “She likes men who are tall, men who are dark, and men who are handsome” 呢？

- 8. 如果 \(A\) 是任意集合，你能说出关于 \(A \cup A\) 的什么？关于 \(A \cap A\)？关于 \(A \setminus A\)？为什么？

- 9. 假设 \(A\) 和 \(B\) 是满足 \(A \subseteq B\) 的集合。你能说出关于 \(A \cup B\) 的什么？关于 \(A \cap B\)？关于 \(A \setminus B\)？为什么？

- 10. 假设 \(A, B,\) 和 \(C\) 是集合。证明 \(C \subseteq A \cap B\) 当且仅当 \((C \subseteq A) \wedge (C \subseteq B)\)。

- 11. 假设 \(A, B,\) 和 \(C\) 是集合，且 \(A \subseteq B\) 且 \(B \subseteq C\)。证明 \(A \subseteq C\)。

- 12. 假设 \(A\) 和 \(B\) 是满足 \(A \subseteq B\) 的集合。\(P(A) \subseteq P(B)\) 是否必然成立？为什么或为什么不成立？

- 13. 设 \(M\) 为任意自然数，并设 \(P(n)\) 为一个谓词，其论域包含所有大于或等于 \(M\) 的自然数。假设 \(P(M)\) 为真，并且对于所有 \(k \ge M\)，\(P(k) \to P(k + 1)\) 成立。证明对于所有 \(n \ge M\)，\(P(n)\) 为真。

## 2.2 集合的布尔代数

很明显，集合论与逻辑密切相关。集合的交集和并集可以用逻辑“与”和逻辑“或”算子来定义。记法 \(\{x \mid P(x)\}\) 使得可以使用谓词来指定集合。而且，如果 \(A\) 是任意集合，那么公式 \(x \in A\) 定义了一个一元谓词，对于实体 \(x\)，当且仅当 \(x\) 是 \(A\) 的成员时该谓词为真。因此，逻辑的许多规则在集合论中有类似规则，这不足为奇。

例如，我们已经注意到 \(\cup\) 和 \(\cap\) 是交换运算。这一事实可以使用逻辑规则来验证。设 \(A\) 和 \(B\) 为集合。根据集合相等的定义，我们可以通过显示 \(\forall x((x \in A \cup B) \leftrightarrow (x \in B \cup A))\) 来证明 \(A \cup B = B \cup A\)。但是对于任意 \(x\)，

```
x \in A \cup B \leftrightarrow x \in A \lor x \in B   (definition of \cup)
\leftrightarrow x \in B \lor x \in A   (commutativity of \lor)
\leftrightarrow x \in B \cup A   (definition of \cup)
```

\(\cap\) 的交换律同样从 \(\cap\) 在 \(\land\) 中的定义得出，类似的论证表明并集和交集是结合运算。

命题逻辑的分配律在集合论中产生两个类似的规则。设 \(A, B,\) 和 \(C\) 为任意集合。则

\[
A \cup (B \cap C) = (A \cup B) \cap (A \cup C)
\]

和

\[
A \cap (B \cup C) = (A \cap B) \cup (A \cap C)
\]

这些规则称为集合论的分配律。要验证第一个分配律，我们只需注意对于任意 \(x\)，

```
x \in A \cup (B \cap C)
\leftrightarrow (x \in A) \lor ((x \in B) \land (x \in C))   (definition of \cup, \cap)
\leftrightarrow ((x \in A) \lor (x \in B)) \land ((x \in A) \lor (x \in C))   (distributivity of \lor)
\leftrightarrow (x \in A \cup B) \land (x \in A \cup C)   (definition of \cup)
\leftrightarrow x \in ((A \cup B) \cap (A \cup C))   (definition of \cap)
```

集合的第二个分配律以完全相同的方式得出。

虽然 \(\cup\) 类似于 \(\lor\)，\(\cap\) 类似于 \(\land\)，但我们尚未看到集合论中任何类似于逻辑“非”算子 \(\neg\) 的运算。

给定一个集合 \(A\)，人们可能会想尝试定义 \(\{x \mid \neg(x \in A)\}\)，即包含所有不属于 \(A\) 的元素的集合。不幸的是，集合论的规则不允许我们定义这样的集合。记法 \(\{x \mid P(x)\}\) 只能在 \(P\) 的论域是集合时使用，因此必须有一个底层集合，从中选择属于或不属于 \(A\) 的元素，即 \(A\) 是其子集的某个底层集合。我们可以通过将讨论限制在某个固定集合的子集上来绕过这个问题。这个集合将被称为 **全集**。请记住，全集仅针对某个特定讨论是“全集”的。它只是某个足够大的集合，能够包含讨论中的所有集合作为其子集。给定一个全集 \(U\) 和 \(U\) 的任意子集 \(A\)，我们可以定义集合 \(\{x \in U \mid \neg(x \in A)\}\)。

### 定义 2.1. 设 \(U\) 为给定的全集，设 \(A\) 为 \(U\) 的任意子集。我们定义 \(A\) 在 \(U\) 中的 **补集** 为集合 \(\overline{A}\)，由 \(\overline{A} = \{x \in U \mid x \notin A\}\) 定义。

通常，我们将简单地称 \(A\) 在 \(U\) 中的补集为 \(A\) 的补集，但你应该记住，每当使用集合的补集时，背景中必须存在某个全集。

鉴于集合上的补运算，我们可以寻找涉及否定的逻辑规则的类似物。例如，我们知道对于任何命题 \(p\)，\(p \wedge \neg p = \text{F}\)。因此，对于 \(U\) 的任何子集 \(A\)，

```
A \cap \overline{A} = \{x \in U \mid (x \in A) \wedge (x \in \overline{A})\} \quad \text{(definition of } \cap \text{)}
= \{x \in U \mid (x \in A) \wedge (x \notin A)\} \quad \text{(definition of complement)}
= \{x \in U \mid (x \in A) \wedge \neg(x \in A)\} \quad \text{(definition of } \notin \text{)}
= \emptyset
```

最后的等式成立是因为对于任何 \(x\)，命题 \((x \in A) \wedge \neg(x \in A)\) 为假。类似地，我们可以证明 \(A \cup \overline{A} = U\) 且 \(\overline{\overline{A}} = A\)（其中 \(\overline{\overline{A}}\) 是 \(A\) 的补集的补集，即通过取 \(\overline{A}\) 的补集得到的集合。）

处理集合补集时最重要的定律是集合的德摩根定律。这些定律直接从逻辑的德摩根定律得出，指出对于全集 \(U\) 的任何子集 \(A\) 和 \(B\)，

\[
\overline{A \cup B} = \overline{A} \cap \overline{B}
\]

和

\[
\overline{A \cap B} = \overline{A} \cup \overline{B}
\]

