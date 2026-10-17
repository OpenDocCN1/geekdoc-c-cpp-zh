
> Dorothy admired the princess that, $t_i$ helped [NP the body $t_j$ [Goldilocks gives the sword to $t_j$]]. (9.4)

# 的每次出现都会被其上方最近的符号绑定。注意，这直接遵循岛屿约束，如果 # 的出现没有被其上方最近的符号绑定，则违反了岛屿约束。

为了处理依赖关系，我们将为解析器增加一个“提取材料”的栈。我们称之为栈解析器。

```
type StackParser a b = [a] -> [a] -> [[b], [a], [a]]
```

我们将对这种特殊版本感兴趣，即解析器的输出由解析树组成。

```
type SPARSER 4 b = StackParser a (ParseTree a b)
```

正如前面的章节所示，我们将首先构建几个目的特定的栈解析器。选择运算符的新版本如下：

```
(|>) :: StackParser a b -> StackParser a b
-> StackParser a b
```

等等，我看到 OCR 有一些重复和损坏部分。我将提供一个干净的版本。

## 9.7 处理提取（Extractions）

subject–PARSER Cat 可以实现如下：

```haskell
spR :: SPARSER Cat Cat
spR = \ us xs ->
[ (Branch "Cat " "S" (fs (t2c np)) [] [np',vp,ws,zs] |
(np,vs,ys) <- prsNP us xs,
(vp,ws,zs) <- prsVP vs ys,
np' <- assignT Nom np,
agreeC np vp,
subcatlist (t2c vp) == [] ]
```

针对如 (9.5) 的条件句示例的第一规则。

> 如果一位公主爱慕一个矮人，他爱了她。

```haskell
cond1R :: SPARSER Cat
cond1R = \ us xs ->
[ (Branch "Cat " "S" [] []) [cond,s1,s2], ws, zs) |
(cond,vs,ys) <- leafPS "COND" xs,
(s1,vs1,ys1) <- prsS vs ys,
(s2,ws,zs) <- prsS vs1 ys1 ]
```

针对如 (9.6) 的条件句示例的第二规则。

> 如果一位公主爱慕一个矮人，他爱了她。

```haskell
cond2R :: SPARSER Cat
cond2R = \ us xs ->
[ (Branch "Cat " "S" [] []) [cond,s1,s2], ws, zs) |
(cond,vs,ys) <- leafPS "COND" xs,
(s1,vs1,ys1) <- prsS vs ys,
(_,vs2,ys2) <- leafPS "THEN" vs1 ys,
(s2,ws,zs) <- prsS vs2 ys2 ]
```

如 (9.5) 和 (9.6) 的条件句语义将在第 12 章处理。

解析一个 NP 有三种方式实现：在输入列表中找到 NP、应用规则 NP → DET CN，以及从提取栈中弹出 NP。

```haskell
prsNP :: SPARSER Cat Cat
prsNP :: leafPS "NP" <| > nR <| pop "NP"
```

该规则的实现方式应该是：将外部的空隙传递给下一个成分，永远不在 NP 内部被消耗。这是为了实施复杂 NP 约束（Complex NP Constraint）。因此，我们将输入栈的内容传递到输出提取栈。

```haskell
nR :: SPARSER Cat Cat
R = \ us xs =
[ (Branch (Cat " NP" fs []) [det,cn] xs, (us+ws, zs) |
(det,ys) <- prsDET xs,
(cn,ws,zs) <- prsCN vs ys,
fs <- combine (t2c det) (t2c cn),
agreeC det cn ]
```

限定词类别始终位于输入列表中：

```haskell
prsDET :: SPARSER Cat Cat
prsDET = leafPS "DET"
```

**练习 9.13** 实现一个限定词规则，它由一个限定词函数和一个名词组成。

普通名词是词汇性的，或者通过从句规则形成：

```haskell
prsCN :: SPARSER Cat Cat
prsCN = leafPS "CN" <| > cnrelR
```

谓语短语（VP）可以是有限形式，或者是助动词加不定式形式：

```haskell
prsVP :: SPARSER Cat Cat
prsVP = finVP <| > auxVp
```

这两个规则都使用了以下栈解析器版本的关键 VP 规则：

```haskell
vpR :: SPARSER Cat Cat
vpR = \us xs ->
[(Branch (Cat " VP") (fs (t2c vp)) [] (vp:xps,ws,zs) |
  (vp,vs) <- leafFS "VP" us xs,
  subcatlist <- subcatList (t2c vp),
  (xps,ws) <- prNsorPP vs,
  match subcatlist (map t2c xp) ]
```

有限 VP 的解析器：

```haskell
finVpR :: SPARSER Cat
finVpR = \us xs -> [(vp',vs) | (vp,vs) <- vpR us xs,
  vp' <- assignTense ]
```

由助动词和不定式组成的 VP 可以实现如下：

```haskell
auxpR :: SPARSER Cat Cat
auxpR = \us xs ->
  [Branch (Cat " VP") (fs (t2c aux)) []
    [aux,inf'], ws, zs) |
      (aux,vs) <- leafSA us xs,
      (inf,zs) <- vpR ys,
      inf' <- assignT inf ]
```

助动词位于输入列表中，或从提取栈中弹出。第二种情况处理疑问句和特殊疑问句中的助动词位移。

```haskell
prsAUX :: SPARSER Cat Cat
prsAUX = leafPS "AUX" <|> pop "AUX"
```

PP 通过规则构造或从提取栈中弹出：

```haskell
prsPP :: SPARSER Cat Cat
prsPP = ppR <|> pop "PP"
```

PP 规则将介词与 NP 结合。

```haskell
ppR :: SPARSER Cat Cat
ppR = \us xs ->
  [ (Branch (Cat " NP" fs []) [prep,np'], ws, zs) |
    (prep,vs) <- prsP xs,
    (np,zs) <- prsNP vs,
    np' <- assignT AccOr np,
    fs <- combine (t2c prep) (t2c np') ]
```

介词均位于输入列表中：

```haskell
prsP :: SPARSER Cat Cat
prsP = leafPS "PREP"
```

动词需项列表包含 NP 或 PP。处理它们的方式如下：

```haskell
prsNorPP :: SPARSER Cat Cat
prsNorPP = prsNP <| > prsPP
```

```haskell
prsNsorPP :: [Cat] -> [(ParseTree Cat], [Cat])
prsNsorPP = many prsNorPP
```

复杂 CN 使用 `prsREL` 解析器处理从句：

```haskell
cnrelR :: SPARSER Cat Cat
cnrelR = \us xs ->
  [ (Branch (Cat " CN" (t2c cn)) []
    [cn,rel], ws, zs) |
    (cn,vs,ys) <- leafPS "CN" xs,
    (rel,ws,zs) <- prsREL vs,
    agreeC cn ]
```

**练习 9.14** 假设我们将定义中的 `leafPS "CN"` 替换为 `prsCN`。会发生什么？为什么？

## 9.7 提取（Extractions）

有两个从句规则：一个用于关系代词开头的从句，另一个用于没有代词的从句。

```haskell
prsREL :: SPARSER Cat Cat
prsREL = relclauseR | thatlessR
```

普通从句由关系词和一个带有 NP 空隙的句子组成。带有 NP 空隙的句子通过将空隙推句子解析器创建。

```haskell
relclauseR :: SPARSER Cat
relclauseR = \us xs ->
[Branch (Cat " COMP" fs []) [rel, ws, zs] |
(rel,vs,zs) <- leafPS "REL" xs,
s <- [fs (t2c rel)],
gap <- [Cat "#NP" fs],
(s,ws,zs) <- push gap vs ]
```

无代词从句等价于以零关系代词开头。约束条件是提取的 NP 不能是主语，且嵌入句的主语没有 Wh 特性。这处理了如“我爱慕的公主”和“我把剑给的王子”之类的从句。

```haskell
thatlessR :: SPARSER Cat
thatlessR = \us xs ->
[ (Branch (Cat " COMP" [] []) [s], vs, zs) |
gap <- [Cat "#NP" AccOrDat],
(s,vs,zs) <- push gap xs,
notElem Wh (fs (t2c s))]
```

作为额外，我们可以将提取栈用于提取 NP 以外的其他用途。为了处理一般疑问句，我们从句子中提取助动词。这将“Did she love me?”分析为“Did, she #_i love me.”。

```haskell
prsYN :: SPARSER Cat Cat
prsYN = \us xs ->
[(Branch (Cat "- YN" [] []) [aux,ws,zs] |
  (aux,vs,ys) <- prsAUX us xs,
  gap <- [Cat "#" "AUX" (fs (t2c aux)) []],
  (s,ws,zs) <- push gap vs ys ] ]
```

从一般疑问句可以看出，我们将特殊疑问句分析为带有提取 NP 或 PP 的一般疑问句。这把“Who did she love?”分析为“Who, did_j love #_j i.”

```haskell
isWH :: ParseTree Cat -> Bool
isWH tr = Wh elem (fs (t2c tr))
```

```haskell
prsWH :: SPARSER Cat Cat
prsWH = \us xs ->
 [Branch (Cat "- WH" [] []) [whyn,ws,zs] |
  (wh,vs,ys) <- prsNorPP us xs,
  isWH,
  gapfs <- [filter (/= Wh) (fs (t2c wh))],
  gap <- [Cat "#" (catLabel (t2c wh)) []],
  (yn,ws,zs) <- push gap vs ys ]
```

## 9.8 添加语义

这是一个应该解析的句子测试套件：

这是一个不应该解析的字符串测试套件。

```haskell
testSuite2 :: [String]
testSuite2 =
  [ "Dorothy 爱慕了被 Alice 帮助的那个男孩",
  "Dorothy 爱慕了那个帮助",
  "Dorothy 爱慕了那个 " ++ "Atreyu 帮助的给剑的公主" ]
```

```haskell
data Term = Const String | Var Int deriving (Eq,Ord)
```

泛义量词为：

```haskell
data GQ = Sm | All | Th | Most | Many | Few
deriving (Eq,Show,Ord)
```

抽象（Abstract）是 lambda 项的 LF 表示。

```haskell
data Abstract = MkAbstract Int LF deriving (Eq,Ord)
```

抽象出现在量化的逻辑形式中。量化由一个泛义量词和两个抽象组成：一个用于量词的限制，另一个用于它的体。

```haskell
data LF = Rel String [Term]
| Eq Term Term
| Neg LF
| Impl LF
| Equi LF
| Conj [LF]
| Disj [LF]
| Qt Abstract Abstract
deriving (Eq,Ord)
```

为这些数据类型定义 `show` 函数是非常方便的：

```haskell
instance Show Term where
show (Const name) = name
show (Var i) = 'x': show i
```

```haskell
instance Show Abstract where
show (MkAbstract i lf) =
"(\\ x" ++ show i ++ " " ++ show lf ++ " ")
```

## 9.8 添加语义

```haskell
instance Show LF where
show (Rel args) = r ++ show args
show (Eq t1 t2) = show t1 ++ "==" ++ show t2
show (Neg lf) = "'\' : (show lf)
show (Impl lf1 lf2) = "(" ++ show lf1 ++ "==>"
  ++ show lf2 ++ ")"
show (Equi lf1 lf2) = "(" ++ show lf1 ++ "<>"
  ++ show lf2 ++ ")"
show (Conj []) = "true"
show (Conj lfs) = "conj" ++ concat [ show lfs ]
show (Disj []) = "false"
show (Disj lfs) = "disj" ++ concat [ show lfs ]
show (Qt q1 a2) = show q1 ++ '\'' : show a1
  ++ ++ '\'' : show a2
```

接下来，我们将为每个类别的解析规则与逻辑形式翻译进行匹配。所有句子都是 `[s NP VP]` 形式，因此我们只需要检查一种类型的解析树：

```haskell
transS :: ParseTree Cat Cat -> LF
transS (Branch (Cat "S" _ _) [np,vp]) =
  (transNP np) (transVP vp)
```

是非疑问句的翻译与句子的类型相同。解释上没有区别；区别在于：陈述句的 LF 翻译用于做出断言，而是非疑问句的翻译用于查询。因此，我们添加以下内容：

```haskell
transS (Branch (Cat "YN" _)
  [Leaf (Cat "did" "AUX") [],s]) = transS S
transS (Branch (Cat "YN" _)
  [Leaf (Cat "didn't" "AUX") [],s]) = Neg (transS S)
```

NP 可以通过三种方式形成，因此我们必须检查三种模式：

```haskell
transNP :: ParseTree Cat ->
(Term -> LF) -> LF
transNP (Leaf (Cat "#" "NP" _)) = \ p -> p (Var 0)
transNP (Leaf (Cat name "NP" _)) = \ p -> p (Const name)
transNP (Branch (Cat "NP" _)) = [det,cn] =
    (transDET det) (transCN cn)
```

限定词是泛义量化的构建基石。这里是亚里士多德量词以及其他一些限定词：
