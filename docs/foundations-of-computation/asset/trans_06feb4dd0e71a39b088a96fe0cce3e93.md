

| 双重补集 | $\overline{\overline{A}} = A$ |
| :--- | :--- |
| 杂项律 | $A \cup \overline{A} = U$<br>$A \cap \overline{A} = \emptyset$<br>$\emptyset \cup A = A$<br>$\emptyset \cap A = \emptyset$ |
| 幂等律 | $A \cap A = A$<br>$A \cup A = A$ |
| 交换律 | $A \cap B = B \cap A$<br>$A \cup B = B \cup A$ |
| 结合律 | $A \cap (B \cap C) = (A \cap B) \cap C$<br>$A \cup (B \cup C) = (A \cup B) \cup C$ |
| 分配律 | $A \cap (B \cup C) = (A \cap B) \cup (A \cap C)$<br>$A \cup (B \cap C) = (A \cup B) \cap (A \cup C)$ |
| 德摩根律 | $\overline{A \cap B} = \overline{A} \cup \overline{B}$<br>$\overline{A \cup B} = \overline{A} \cap \overline{B}$ |

图 2.2：集合的布尔代数部分定律。A、B 和 C 是集合。对于涉及补运算的定律，假设它们是某个全集 U 的子集。在大多数情况下，这些定律直接对应于图 1.2 中给出的命题逻辑布尔代数定律。

例如，我们可以通过如下计算验证这些定律中的第一条：

```
$\overline{A \cup B} = \{x \in U | x \notin (A \cup B)\}$ (definition of complement)
$= \{x \in U | \neg(x \in A \cup B)\}$ (definition of \(\notin\))
$= \{x \in U | \neg(x \in A \lor x \in B)\}$ (definition of \(\cup\))
$= \{x \in U | (\neg x \in A) \land (\neg x \in B)\}$ (DeMorgan's Law for logic)
$= \{x \in U | (x \notin A) \land (x \notin B)\}$ (definition of \(\notin\))
$= \{x \in U | (x \in \overline{A}) \land (x \in \overline{B})\}$ (definition of complement)
$= \overline{A} \cap \overline{B}$ (definition of \(\cap\))
```

可以使用简单的归纳证明来验证集合论中德摩根律的推广版本。（在此语境下，所有集合都假设是某个未命名全集的子集。）下面的简单计算验证了三个集合的德摩根律：

```
\overline{A \cup B \cup C} = \overline{(A \cup B) \cup C}
= (\overline{A \cup B}) \cap \overline{C} \quad \text{(by DeMorgan's Law for two sets)}
= (\overline{A} \cap \overline{B}) \cap \overline{C} \quad \text{(by DeMorgan's Law for two sets)}
= \overline{A} \cap \overline{B} \cap \overline{C}
```

由此，我们可以推导出四个集合、五个集合等等的类似定律。但是，仅仅说“等等”并不能严格证明这一事实。以下是对推广德摩根律的严格归纳证明：

**定理 2.5.** 对于任意自然数 \(n \ge 2\) 和任意集合 \(X_1, X_2, \dots, X_n\),

\(\overline{X_1 \cup X_2 \cup \cdots \cup X_n} = \overline{X_1} \cap \overline{X_2} \cap \cdots \cap \overline{X_n}\)

**证明.** 我们采用归纳法证明。在基础情形中，\(n=2\)，该陈述为 \(\overline{X_1 \cup X_2} = \overline{X_1} \cap \overline{X_2}\)。这成立，因为它只是两个集合德摩根律的直接应用。

在归纳步骤中，假设该陈述对 \(n = k\) 成立。我们要证明它对 \(n = k + 1\) 也成立。设 \(X_1, X_2, \dots, X_{k+1}\) 为任意 \(k + 1\) 个集合。则有：

```
\overline{X_1 \cup X_2 \cup \cdots \cup X_{k+1}} = \overline{(X_1 \cup X_2 \cup \cdots \cup X_k) \cup X_{k+1}}
= (\overline{X_1 \cup X_2 \cup \cdots \cup X_k}) \cap \overline{X_{k+1}}
= (\overline{X_1} \cap \overline{X_2} \cap \cdots \cap \overline{X_k}) \cap \overline{X_{k+1}}
= \overline{X_1} \cap \overline{X_2} \cap \cdots \cap \overline{X_{k+1}}
```

在此计算中，第二步由两个集合的德摩根律得出，第三步由归纳假设得出。□

正如逻辑定律允许我们对逻辑公式进行代数运算一样，集合论定律允许我们对集合进行代数运算。由于逻辑与集合论之间存在密切关系，它们的代数非常相似。集合的代数，如同逻辑的代数一样，是布尔代数。当乔治·布尔撰写他1854年的逻辑著作时，它实际上同样涉及集合论和逻辑。事实上，布尔并未明确区分谓词与使该谓词为真的对象集合。他的代数定律和公式同样适用于两种情况。更准确地说，如果我们只考虑某个给定全集 \(U\) 的子集，那么命题逻辑的基本符号和运算与集合论中的某些符号和运算之间存在直接对应关系，如下表所示：

| 逻辑 | 集合论 |
| :--- | :--- |
| T | U |
| F | ∅ |
| p ∧ q | A ∩ B |
| p ∨ q | A ∪ B |
| ¬p | \(\overline{A}\) |

任何涉及命题变量和符号 T、F、∧、∨、¬的有效逻辑公式或计算，都可以通过将公式中的命题替换为 U 的子集，并将逻辑符号替换为 U、∅、∩、∪ 和补运算符，转换为集合论中的有效公式或计算。

与逻辑一样，集合论的运算可以组合形成复杂表达式，例如 (A ∪ C) ∩ (B ∪ \(\overline{C}\) ∪ D)。在这样的表达式中，始终可以使用括号来指定运算的执行顺序。在没有括号的情况下，我们需要优先级规则来确定运算顺序。集合布尔代数的优先级规则直接继承自命题布尔代数。当并集和交集在没有括号的情况下一起使用时，交集的优先级高于并集。此外，当在没有括号的情况下使用多个同类型运算符时，则按从左到右的顺序求值。（当然，由于 ∪ 和 ∩ 都是结合运算，求值顺序是从左到右还是从右到左其实并不重要。）例如，A ∪ B ∩ C ∪ D 被求值为 (A ∪ (B ∩ C)) ∪ D。补运算是一种特殊情况。由于它通过在操作数上方画线来表示，因此永远不会出现关于公式的哪一部分适用该运算的歧义。

集合论定律可用于简化涉及集合的复杂表达式。（当然，像往常一样，“简化”的含义部分取决于观察者。）例如，对于任意集合 X 和 Y，

```
(X ∪ Y) ∩ (Y ∪ X) = (X ∪ Y) ∩ (X ∪ Y) (Commutative Law)
= (X ∪ Y) (Idempotent Law)
```

在第二步中，幂等律（即 A ∩ A = A）被应用，其中 A = X ∪ Y。对于使用补运算的表达式，通常认为将运算应用于单个集合（如 \(\overline{A}\)）比应用于公式（如 \(\overline{A \cap B}\)）更简单。德摩根律始终可用于简化补运算应用于公式的表达式。例如，

```
A \cap \overline{B \cup \overline{A}} = A \cap (\overline{B} \cap \overline{\overline{A}}) \quad \text{(DeMorgan's Law)}
= A \cap (\overline{B} \cap A) \quad \text{(Double Complement)}
= A \cap (A \cap \overline{B}) \quad \text{(Commutative Law)}
= (A \cap A) \cap \overline{B} \quad \text{(Associative Law)}
= A \cap \overline{B} \quad \text{(Idempotent Law)}
```

作为集合论与逻辑关系的最后一个示例，请考虑集合论表达式 \(A \cap (A \cup B)\) 及其对应的复合命题 \(p \land (p \lor q)\)。（它们对应是因为对于任意 \(x\)，\(x \in A \cap (A \cup B) \equiv (x \in A) \land (x \in A \lor x \in B)\)。）您可能会直观地觉得 \(A \cap (A \cup B) = A\) 显而易见。从形式上讲，这源于 \(p \land (p \lor q) \equiv p\) 这一事实，这可能不够直观，并且从逻辑定律代数证明起来出人意料地困难。但是，还有另一种方法可以检查逻辑等价是否有效：制作真值表。请考虑 \(p \land (p \lor q)\) 的真值表：

| p | q | \(p \lor q\) | \(p \land (p \lor q)\) |
|---|---|---|---|
| 假 | 假 | 假 | 假 |
| 假 | 真 | 真 | 假 |
| 真 | 假 | 真 | 真 |
| 真 | 真 | 真 | 真 |

该表格第一列和最后一列相同这一事实表明 \(p \land (p \lor q) \equiv p\)。将 \(p\) 取为命题 \(x \in A\)，将 \(q\) 取为命题 \(x \in B\)，可得出集合 \(A\) 和 \(A \cap (A \cup B)\) 具有相同的元素，因此相等。

## 练习

- 1. 使用逻辑定律验证并集和交集的结合律。也就是说，证明如果 \(A\)、\(B\) 和 \(C\) 是集合，则 \(A \cup (B \cup C) = (A \cup B) \cup C\) 且 \(A \cap (B \cap C) = (A \cap B) \cap C\)。

- 2. 证明对于任意集合 \(A\) 和 \(B\)，\(A \subseteq A \cup B\) 且 \(A \cap B \subseteq A\)。

- 3. 回顾，符号 \(\oplus\) 表示逻辑异或运算。如果 \(A\) 和 \(B\) 是集合，则通过 \(A \Delta B = \{x | (x \in A) \oplus (x \in B)\}\) 定义集合 \(A \Delta B\)。证明 \(A \Delta B = (A \setminus B) \cup (B \setminus A)\)。（\(A \Delta B\) 称为 \(A\) 和 \(B\) 的**对称差**。）

