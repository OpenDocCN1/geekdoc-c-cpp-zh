
```haskell
transDET :: ParseTree Cat Cat -> (Term -> LF)
-> (Term -> LF)
-> LF
transDET (Leaf (Cat "every" "DET" _)) =
\ p q -> let i = fresh[p,q] in Qt All (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "all" "DET" _)) =
\ p q -> let i = fresh[p,q] in Qt All (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "some" "DET" _)) =
\ p q -> let i = fresh[p,q] in Qt Sm (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "a" "DET" _)) =
\ p q -> let i = fresh[p,q] in Qt Sm (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "several" "DET" _)) =
\ p q -> let i = fresh[p,q] in Qt Sm (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "no" "DET" _)) =
\ p q -> let i = fresh[p,q] in Neg (Qt Sm (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "the" "DET" _)) =
\ p q -> let i = fresh[p,q] in Qt Th (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "most" "DET" _)) =
\ p q -> let i = fresh[p,q] in Qt Most (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "many" "DET" _)) =
\ p q -> let i = fresh[p,q] in Qt Many (MkAbstract i (p (Var i))
(q (Var i)))
transDET (Leaf (Cat "few" "DET" _)) =
\ p q -> let i = fresh[p,q] in Neg (Qt Many (MkAbstract i (p (Var i))
(q (Var i))))
```

一个特殊情况是限定词 `which`。它将用于对变量抽象：

```haskell
transDET (Leaf (Cat "which" "DET" _)) =
\ p q -> let i = fresh[p,q] in Conj [p (Var 0),q (Var 0)]
```

普通名词可以是词性的，也可以是复杂的。以下是这情况的翻译：

```haskell
transCN :: ParseTree Cat -> Term -> LF
transCN (Leaf (Cat name "CN" _)) = \ x -> Rel name
transCN (Branch (Cat "CN" _)) [cn]) = \ x -> Conj [transCN x]
```

关系从句有两种类型：带有关系代词或不带。

```haskell
transREL :: ParseTree Cat -> Term -> LF
transREL (Branch (Cat "COMP" _ ) [rel,s]) =
\ x -> sub (transS)
transREL (Branch (Cat "COMP" _ ) [s]) =
\ x -> sub (transS)
```

PP 有两种类型：带有提取空位的简单 PP 和复杂的 PP。VP 的部分模式如下：

```haskell
transPP :: ParseTree Cat -> (Term -> LF) -> LF
transPP (Leaf (Cat "#" _)) = \ p -> p (Var 0)
transPP (Branch (Cat "#" _)) [prep,np]) = transNP np
```

```haskell
transVP :: ParseTree Cat -> Term -> LF
transVP (Branch (Cat "VP" _ _) []) =
\ t -> Rel name
transVP (Branch (Cat "VP" _ _) [Leaf (Cat name "VP" _]),np]) =
\ subj -> transNP np (obj -> Rel name [obj])
transVP (Branch (Cat "VP" _ _) [Leaf (Cat name "VP" _]),pp]) =
\ subj -> transNP np (obj -> transPP (iobj -> Rel name [obj]))
transVP (Branch (Cat "VP" _ _) [Leaf (Cat "did" "AUX"),vp]) =
transVP vp
transVP (Branch (Cat "VP" _ _) [Leaf (Cat "didn't" "AUX"),vp]) =
\ x -> Neg ((transVP vp) x)
transVP (Branch (Cat "VP" _ _) [Leaf (Cat "#" "AUX"),vp]) =
transVP vp
```

**练习 9.15** 上哪些情况没有被涵盖？检查词汇和剩余情况的翻译。

疑问句包含一个带有 Wh-空位的嵌入句子。如果我们假设这个空位由变量 `Var 0` 翻译，我们就可以将疑问句翻译为该变量的抽象：

```haskell
transWH :: ParseTree Cat Cat -> Abstract
transWH (Branch Cat "WH" _ ) [wh,s] =
MkAbstract 0 (Conj [transWH wh, s])
```

这留下了以下 Wh-NP 的翻译：

```haskell
transW :: ParseTree Cat Cat -> LF
transW (Branch (Cat "NP" fs _) [det,cn]) =
transCN cn (Var 0)
transW (Leaf (Cat "elem" fs)) = Rel "man" [Var 0]
| Masc 'elem' fs = Rel "woman" [Var 0]
| Fem 'elem' fs = Rel "person" [Var 0]
| MasCorFem 'elem' fs = Rel "thing" [Var 0]
| otherwise = Rel "thing" [Var 0])
transW (Branch (Cat "PP" fs _) [prep,np])
| Masc 'elem' fs = Rel "man" [Var 0]
| Fem 'elem' fs = Rel "woman" [Var 0]
| MasCorFem 'elem' fs = Rel "person" [Var 0]
| otherwise = Rel "thing" [Var 0])
```

还有一些未完成的工作。关系类的替换规则使用替换函数，将无界的 `Var 0` 替换为新项。结果是 `sub x` 的类型为 `LF`，而 `\x -> sub x lf` 的类型为 `Term -> LF`。

```haskell
subst :: Term -> Term -> Term -> Term
subst x (Const name) = Const name
subst x (Var n) | n == 0 = x
  | otherwise = Var n
| x == Var n = error "bad substitution"
```

## 9.8 添加语义

`bInLFs` 函数用于为预测列表计算一个新的逻辑索引（fresh index）。请注意，该新索引用于 `transDET` 的定义。

```haskell
freshIndex :: [LF] -> Int
freshIndex lfs = i+1
where i = foldr max 0 (bInLFs lfs)

fresh :: [Term -> LF] -> Int
fresh preds = freshIndex (map ($ dummy) preds)
where dummy = Const ""
```

以下函数用于处理并翻译声明性句子。

```haskell
process :: String -> [LF]
process string = map transS (parses string)
```

Wh 疑问句会有不同的处理，因为它们翻译的是抽象。

```haskell
processW :: String -> [Abstract]
processW string = map transWH (parses string)
```

这里是示例调用：

```haskell
> P process "Alice admired the princess that Atreyu gave the sword to."
[The (\ x2 conj[princess[x2],The (\ x1 sword[x1])
  (\ x1 gave[atreyu,x1,x2]))
  (\\ x2 admired[alice,x2]))]]
> processW "To whom did Atreyu give the dwarf that shuddered?"
[(\\ x0 conj[person[x0]],The (\ x1 conj[dwarf[x1],shuddered[x1]])
  (\\ x1 give[atreyu,x1,x0]))]]
```

从解析到解释的流程最后一步留给你们完成。

**练习 9.16** 编写函数，在适当的模型中解释本节介绍的逻辑形式（logical forms）。

## 9.9 进一步阅读

关于树关系关系的逻辑在 [BGMV93]（模态逻辑）和 [BRVs95]（一阶逻辑）中被提出。第 9.1 节中使用的位置二元关系可以用逻辑术语轻松描述。

[PW83] 将自然语言解析等同于逻辑推演。形式语言理论背景下的解析圣经是 [AU72]。用 Prolog 解析自然语言片段是 [PS87] 的主题。函数式编程背景下的解析器组合器（Parser combinators）在 [Wad85] 中介绍，并在 [Hut92] 中进行了进一步讨论。[JS01] 中也可以找到解析器组合器的示例。第 9.7 节中使用解析器组合器处理空隙（gaps）的方法基于 [Eij03]。

形式上讲，提取文法（extraction grammars）比上下文无关文法强大，因为它们允许定义顺序索引语言（sequentially indexed languages）。顺序索引语言是上下文无关语言以及 [Gaz88] 中线性索引语言的真扩展。更多细节请参阅 [Eij07b]。

一种用于开发多语言自然语言应用的特殊编程语言是 Grammatical Framework（简称 GF），其核心是解析。GF 类似于 Haskell，但专门用于语法编写。参见 [Ran09] 和 http://www.grammaticalframework.org。

# 10

# 处理关系与作用域

## 总结

在本章中，我们将动词短语解释为不同元数（arities）的关系，使用一种任意元数的关系类型。在类型论中编码关系以使得通常的逻辑操作可以应用于它们（用术语来说，关系应该是“可合取的”），这一问题在语义学文献中已得到广泛研究。我们将在关系类型上定义合取、析取和补。接下来，我们将限定词短语（determiner phrases）解释为从 (n+1) 元关系到 n 元关系的函数，将 n 元限定词短语序列解释为从 (n+m) 元关系到 n 元关系的函数，并处理此类函数的作用域翻转（scope reversal）。

## 10.1 解释 NP 列表

（注：不再将句子 "Every unicorn ate a lettuce leaf"每只独角兽都吃了一片生菜叶）分析为关系，而是……

# 处理关系与作用域

这里是 Keenan 显示的几个关于量词不可重现的进一步示例。

城堡里的三位骑士对待了同一位公主。(10.2)

婚礼上的女性们都戴着不同的帽子。(10.3)

巨魔们对不同的问题给出了不同的答案。(10.4)

在本章中，我们将短语从解释为关系归约器（relation reducers），一个由 $n$ 个 NP 组成的簇被解释为类型为 $\langle n \rangle$ 的函数。在这种 NP 簇解释可以还原为类型 (1) 函数的情况下，归约 $f_1 \circ \dots \circ f_n$ 对 NP 施加了作用域排序。这意味着，通过考虑归约类型 (1) 函数的不同排序，可以处理量词作用域，同时确保作用域的重排符合相关的参数绑定约束。例如，回想 *每一只独角兽——一棵在上面的生菜* 的解释。复合 $f \circ g$ 使得全称量词的作用域涵盖了存在量词。若若要重排 $f \circ g$ 的作用域，我们首先定义一个操作 $S$：

```
$S := \lambda R\lambda x\lambda y \mapsto (R y) x$.
```

这重新排列了关系的两个位置。$f$ 和 $g$ 的逆作用域读取可以表示为 $g \circ f \circ \mathbf{S}$。这对应于：

```
$\lambda R \mapsto \exists y(\text{LettuceLeaf} y \wedge \forall x(\text{Unicorn} x \to R xy))$.
```

将在下面的第 10.5 节详细讨论这些反转作用域映射。

## 10.2 一般关系

集合 $A$ 上的二元关系可以视为类型为 $A \to P(A)$ 的函数。它将 $A$ 的元素 $a$ 映射到 $A$ 的子集 $aR$，其中 $aR$ 是内容的简写：

```
{$x \in A | R ax\}$.
```

等价地，二元关系可以被视为类型为 $A \to A \to t$ 的函数。它将 $A$ 的元素 $a$ 映射到 $A$ 上的特征函数 $\chi_a$，其中当 $Rab$ 成立时 $\chi_a(b) = 1$。

同样，集合 $A$ 上的一元关系是类型为 $A \to t$ 的函数，集合 $A$ 上的三元关系是类型为 $A \to A \to A \to t$ 的函数，以此此类推。特殊情况是零元关系：这一个真值。注意，$A$ 上的 $(n+1)$ 元关系可以被视为从 $A$ 到 $A$ 上 $n$ 元关系类型的函数。

我们需要的是用于任意关系的数据类型。该数据类型的每个实例应该有一个确定的元数（arity），但两个实例可能有不同的元数。

但首先，我们声明模块并导入一些之前定义的相关模块。通过 `hiding` 关键字，我们指定了不想被导入的函数。

```
module HRAS where

import Data.List
import Model
import FSyn hiding (Form,Term,Var,Eq,Neg,
Impl,Equi,Conj,Disj)
import TCOM
import P
```

我们将使用以下辅助数据类型 `RL a r`。

```
data RL a r = Zero r
             | Succ (RL a (a -> r))
```

这允许我们从给定的 `r` 开始构建关系。两种情况是 `r` 和 `a -> r`。如果我们再次应用构造函数，对于 `RL a (a -> r)`，我们得到 `a -> r` 和 `a -> a -> r`。如果我们对 `RL a (a -> a -> r)` 应用构造函数，我们得到 `a -> a -> r` 和 `a -> a -> a -> r`，以此此类推。

我们需要的数据类型是 `RL Bool` 的部分情况：

```
type REL a = RL Bool
```

这表示从 `Bool` 开始，如果一个关系要么是零元关系（由标记 `Zero` 指示），要么是 $n$ 元关系（由标记 `Succ` 指示）。如果 $A$ 上的 $n$ 元关系满足 $n \ge 1$，则它可以被视为类型为 $A \to Rn-1$ 的函数，其中 $(n-1)$ 元关系。关系的元数通过计算 `Succ` 的次数来确定：

```
arity :: RL b -> Int
arity (Zero _) = 0
arity (Succ r) = arity r
```

# 处理关系与作用域

这是一个将关系应用于参数的通用函数。前提是关系至少是一一元的。

```
apply :: REL a -> a
apply (Zero _) = error "no argument"
apply (Succ r) x = apply' r

apply' :: (a -> r) -> a -> RL a
apply' (Zero f) x = Zero (f x)
apply' (Succ r) x = Succ (apply' r)
```

这些函数说明了类型 `RL r` 需要辅助数据。在 `apply' (Zero f)` 处，`f` 不是 `REL` 类型而是 `a -> r` 类型，我们还需要一个抽象操作。这种抽象会增加元数。如果 $f$ 是一个产生 0 元关系的函数，那么我们知道 $x$ 是 `Succ` 形式，`Boolean` 表示额外的元数，抽象是一个更通用的类型：
