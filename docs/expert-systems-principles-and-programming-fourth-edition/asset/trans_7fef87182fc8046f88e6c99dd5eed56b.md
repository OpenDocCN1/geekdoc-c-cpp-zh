

在谓词逻辑下是有效的论证。事实上，所有三段论逻辑都是一阶谓词逻辑的有效子集，并且可以在其下被证明为有效。

The only valid syllogistic form of the proposition is:

> 若苏格拉底是人，则苏格拉底是必死的
> 苏格拉底是人
> 因此，苏格拉底是必死的

Let:

```
p = Socrates is a man
q = Socrates is mortal
```

The argument becomes:

```
p → q
p
∴ q
```

which is a valid syllogistic form of modus ponens.

As another example, consider the following classic argument:

> 所有马都是动物
> 因此，马的头
> 是动物的头

We know that this argument is correct and yet it cannot be proved under propositional logic, although it can be proven under predicate logic (see Problem 3.12).

## 3.8 一阶谓词逻辑

Syllogistic logic can be completely described by predicate logic. Table 3.12 shows the four categorical statements and their representation in predicate logic. In addition to the rules of inference previously discussed, predicate logic has rules that deal with quantifiers.

Table 3.12 使用谓词逻辑表示四类三段论

| 类型 | 图式 | 谓词表示 |
|---|---|---|
| A | 所有 S 是 P | (∀x) (S(x) → P(x)) |
| E | 没有 S 是 P | (∀x) (S(x) → ~P(x)) |
| I | 有些 S 是 P | (∃x) (S(x) ∧ P(x)) |
| O | 有些 S 不是 P | (∃x) (S(x) ∧ ~P(x)) |

The Rule of Universal Instantiation essentially states that an individual may be substituted for a universal. For example, if φ is any proposition or propositional function:

```
(∀ x) Φ(x)
∴ Φ(a)
```

is a valid inference, where a is an instance. That is, a refers to a specific individual while x is a variable that ranges over all individuals. For example, this can be used to prove that Socrates is human:

```
(∀ x) H(x)
∴ H(Socrates)
```

where H(x) is the propositional function that says x is a human. The above states that for every x, that x is human, and so by inference Socrates is human.

Other examples of the Rule of Universal Instantiation are:

```
(∀ x) A(x)
∴ A(c)
```

```
(∀ y) (B(y) ∨ C(b))
∴ B(a) ∨ C(b)
```

```
(∀ x) [A(x) ∧ (∃ x) (B(x) ∨ C(y))]
∴ A(b) ∧ (∃ x) (B(x) ∨ C(y))
```

In the first example, the instance c is substituted for x. In the second example, notice that the instance a is substituted for y but not for b since b is not included in the scope of the quantifier. That is, a quantifier such as ∀x applies only to x variables. The variables such as x and y used with quantifiers are called bound while the others are called free. In the third example, the quantifier x has as its scope all A(x). That is, ∀x does not apply to the existential quantifier ∃x and its scope over B(x) ∨ C(y). The convention of nested quantifiers such as this is that the scope ends when a new quantifier is used, even if it uses the same variable, such as x. The formal proof of the syllogism:

```
All men are mortal
Socrates is a man
∴ Socrates is mortal
```

is shown following, where H = man, M = mortal, and s = Socrates:

- 1. (∀ x) (H(x) → M(x))
- 2. H(s) ... ∴ M(s)
- 3. H(s) → M(s) ... 1 全称实例化
- 4. M(s) ... 2,3 肯定前件

## 3.9 逻辑系统

A logic system is a collection of objects such as rules, axioms, statements, and so forth organized in a consistent manner. The logic system has several goals.

The first goal is to specify the forms of arguments. Since logical arguments are meaningfulness in a semantic sense, a valid form is essential if the validity of the argument is to be determined. Thus, one important function of a logic system is to determine the well-formed formulas (wffs) that are used in arguments. Only wffs can be used in logic arguments. For example, in syllogistic logic,

```
All S is P
```

could be a wff, but:

```
All
All is S P
Is S all
```

are not wffs. Although the symbols of the alphabet are meaningless, the sequence of symbols that make up the wff is meaningful.

The second goal of a logic system is to indicate the rules of inference that are valid. The third goal of a logic system is to extend itself by discovering new rules of inference and so extend the range of arguments that can be proven. By extending the range of arguments, new wffs, called theorems, can be proven by a logic argument.

When a logic system is well developed it can be used to determine the validity of arguments in a way that is analogous to calculations in systems such as arithmetic, geometry, calculus, physics, and engineering. Logic systems have been developed such as the Sentential or Propositional Calculus, the Predicate Calculus, and so forth. Each system relies on formal definitions of its axioms or postulates, which are the fundamental definitions of the system. From these axioms people (and sometimes computer programs such as the Automated Mathematician) try to determine what can be proven. Anyone who has studied Euclidean geometry in high school is familiar with axioms and the derivation of geometric theorems. Just as geometric theorems can be derived from geometric axioms, so can logic theorems be derived from logic axioms.

An axiom is simply a fact or assertion that cannot be proven from within the system. Sometimes we accept certain axioms because they make “sense” by appealing to commonsense or observation. Other axioms, such as “parallel lines meet at infinity,” do not make intuitive sense because they appear to contradict Euclid’s axiom of parallel lines as never meeting. However, this axiom about parallel lines meeting at infinity is just as reasonable from a purely logical viewpoint as Euclid’s and is the basis of one type of non-Euclidean geometry.

A formal system requires the following:

- 1. 一组符号的字母表。
- 2. 这些符号的有限字符串集合，即wff。
- 3. 公理，系统的定义。
- 4. 推理规则，使得一个wff A可以作为有限wff集合G（G = {A1, A2 ... An}）的结论被推导出来。这些wff必须是公理或逻辑系统的其他定理。例如，命题逻辑系统可以仅使用肯定前件来推导新定理。

If the argument:

```
A1, A2, ... An ∴ A
```

is valid, then A is said to be a theorem of the formal logic system and is written with the symbol |- . For example, G |- A means that A is a theorem of the set of wffs, G. A more explicit schema of a proof that A is a theorem is the following:

```
A1, A2, ... An |- A
```

The symbol |- , which indicates that the following wff is a theorem, is not a symbol of the system. Instead, |- is a metasymbol, because it is used to describe the system itself. An analogy is a computer language such as Java. Although programs can be specified using Java's syntax, there is no syntax in Java for indicating a valid program.

A rule of inference in a formal system specifies exactly how new assertions, the theorems, can be obtained from axioms and previously derived theorems. An example of a theorem is our syllogism about Socrates, written in predicate logic form:

```
(∀ x) (H(x) → M(x)) , H(s) |- M(s)
```

where H is the predicate function for man and M is the predicate function for mortal. Since M(s) can be proven from its axioms on the left, it is a theorem of these axioms. However, note that M(Zeus) would not be a theorem since Zeus, the Greek god, is not a man, and there is no alternative way of showing M(Zeus).

If a theorem is a tautology, it follows that G is the null set since the wff is always true and so does not depend on any other axioms or theorems. A theorem that is a tautology is written with the symbol |- as in:

```
|- A
```

For example, if A = p v ~p, then:

```
|- p v ~p
```

states that p v ~p is a theorem, which is a tautology. Notice that whatever values are assigned to p, either T or F, the theorem p v ~p is always true. An assignment of truth values is an interpretation of a wff. A model is an interpretation in which the wff is true. For example, a model of p → q is p = T and q = T. A wff is called consistent or satisfiable if there is an interpretation that makes it

