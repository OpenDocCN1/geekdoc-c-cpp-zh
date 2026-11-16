

### 前向传递:

![](img/e423791fd87c536ca132e7d760db042c_12_0.png)

### 构造的函数闭包:

| 导数 | 闭包 | 参数 (d) | 结果 |
| :--- | :--- | :--- | :--- |
| $c_{\oplus_2}$ | $\lambda d \rightarrow c_{r_1} (d \otimes 60) \oplus c_{\ominus_1} (d \otimes 5)$ | 1 | 170 |
| $c_{\ominus_1}$ | $\lambda d \rightarrow c_{r_2} (d \otimes 10) \oplus c_{\ominus_2} (d \otimes 6)$ | 5 | 110 |
| $c_{\ominus_2}$ | $\lambda d \rightarrow c_{r_3} d \oplus c_1 d$ | 50 | 50 |
| $c_{\ominus_2}$ | $\lambda d \rightarrow c_{r_4} d \oplus c_{r_4} d$ | 30 | 60 |
| $c_1$ | $\lambda d \rightarrow \{ \}$ | 50 | 0 |
| $c_{r_4}$ | $\lambda d \rightarrow \{ x \mapsto d \}$ | 60, 50, 30, 30 | 60, 50, 30, 30 |

图 4. x × (x + 1) × (x + ·) 的反向模式自动微分，其中 x = 5。

图 4 表明，该计算有效地在多个遍中工作，这是反向模式自动微分的关键特征。在前向（自底向上）遍（由黑色箭头显示）中，算法计算 Nagata 数，其中包含每个子表达式的值，以及节点之间作为函数闭包 c : d ⇢ Sparse v, d 的依赖关系，例如最终结果的 N 300 c$_{\ominus_2}$。在后向（自顶向下）遍（由红色从左到右的箭头显示）中，我们在参数 1 上调用函数闭包 c$_{\ominus_2}$（使用 abs$_{\rightarrow}$）。它将标量累加器向下传播。在每个向下步骤中，累加器会发生变化，以反映当子表达式变化 1 时整体导数变化多少。最后，叶节点的结果被相加（由蓝色从右到左的箭头显示）以得出整体导数。传统的命令式算法通常通过命令式更新来完成此操作。我们将在 5.3 节推导该形式，但首先我们要解决加法的线性开销。

## 5.2. 累加

我们可以以与优化标量乘法非常相似的方式优化 d-模块的加法结构：即考虑具有加法齐次性属性的 e → e 函数的表示：

```
f (x ⊗ y) = x ⊗ f y
```

该表示也称为 e 的 Cayley 表示 [23,24]，其最著名的示例是差分列表 [25] 或 Hughes 列表 [26]。同样，Haskell 类型 e → e 包含不具有齐次性属性的函数；这些函数不包含在 Cayley e 类型中。

加法的保持源于 f 的结果是一个半模的事实。

```
type Cayley e = e -> e
rep₀ :: Monoid e => e -> Cayley e
rep₀ e = λe' -> e' ⊕ e
abs₀ :: Monoid e => Cayley e -> e
abs₀ f = f zero
```

该表示通常隐含另一种“强度缩减”，即从 e 的二元运算符 (⊕) 到函数组合 (∘)。由此，我们将加法的时间复杂度从 Sparse v d 的 O(V) 降低到 Cayley (Sparse v d) 的 O(1)。

```
instance Monoid (Cayley e) where
zero = id
f ⊕ g = g ∘ f
```

我们按照标准配方推导 Module 和 Kronecker 实例。然而，我们无法消除 Cayley e 的 Module 和 Kronecker 实例中的昂贵操作。确实，Module 实例要求在 Cayley e 和 e 之间转换，其中 rep₀ 重新引入了 e 的昂贵 O(V) 加法运算 (⊕)，而我们刚刚从 Monoid 实例中消除了该运算。

```
instance Module d e => Module d (Cayley e) where
d • f = rep₀ . (d • abs₀ . f)
```

通过 rep₀ 从 e 推导的 Kronecker 实例同样包含 e 的加法运算 (⊕)。

```
instance Kronecker v d e => Kronecker v d (Cayley e) where
delta v = λe -> e ⊕ delta v
```

幸运的是，我们可以再次为类型 e = d ↝ Cayley (Sparse v d) 定义一个专用的 Kronecker 实例，从而避免使用昂贵的 ⊕ 运算。确实，在 e 上定义的 (⊙) 运算不必使用 Cayley (Sparse v d) 上定义的运算。对于专用的 delta，我们改为计算：

```
delta v = {- definition of delta for d ↝ -}
λd -> d • delta v
= {- definition of (⊙) and delta for Cayley -}
λd -> rep₀ . (d • abs₀) . (λe -> e ⊕ delta v)
= {- definition of rep₀, and abs₀ -}
λd -> λe -> e ⊕ (d • (λe -> e ⊕ delta v) zero)
= {- β-reduction and unit of monoid (Fig. 3) -}
λd -> λe -> e ⊕ (d • delta v)
= {- equation (2) -}
λd -> λe -> insertWith (⊙) v d e
= {- η-reduction -}
λd -> insertWith (⊙) v d
```

因此，我们得到一个仅需 O(log V) 时间的 delta 实现。

```
instance (Ord v, Semiring d) => Kronecker v d (d ↝ Cayley (Sparse v d))
where delta = insertWith (⊙)
```

此外，Cayley e 表示保持了 e 的正确性。

```
instance CorrectAD v d e => CorrectAD v d (Cayley e) where
rep = rep₀ . rep
abs = abs₀ . abs₀
```

总结来说，对于类型 d ↝ Cayley (Sparse v d)，(⊙) 和 (⊕) 均需 O(1) 时间，而 delta 需 O(log V) 时间。因此，对于具有 N 个节点和 V 个变量的程序，abstractD 的时间复杂度现在为 O(N × log V)。

```
reverseAD_Cayley :: (Ord v, Semiring d)
=> (v -> d) -> Expr v -> d × (d ↝ Cayley (Sparse v d))
reverseAD_Cayley = abstractD
```

例如，与之前一样，example3 在 X = 5 处的导数为 170。

```
> (abs₀ . abs₀) (reverseAD_Cayley (λX -> 5) example3)
[X |-> 170]
```

请注意，我们可以将类型 Cayley (Sparse v d) 的值视为修改类型 Sparse v d 状态的计算的函数模型，即不可变映射。

## 5.3. 基于数组的反向模式

从性能角度来看，通过从不可变映射切换到可变数组（来自 Data.Array.ST）（附录 C），我们可以做得更好。使用这些来表示状态，而不是上面的纯函数式实现，我们可以执行原地更新。此外，数组可以由隐式环境（Control.Monad.Reader）提供。因此，我们可以使用类型 ReaderT (STArray s v) (ST s) ()，而不是类型 Cayley (Sparse v d)。将这个相当冗长的类型封装在类型别名 STCayley v d 中很方便。

```
type STCayley v d = ReaderT (STArray s v s) (ST s) ()
```

请注意，STCayley v d 对状态线程参数 s 进行多态量化，如果我们想使用 Haskell 的内置原语 runST :: (∀S. ST s a) -> a 来运行计算，这是必要的。

Cayley (Sparse v d) 和 STCayley v d 之间的同构本质上在数组和映射表示之间进行转换。

```
rep_∞ :: (Ix v, Semiring d) => Cayley (Sparse v d) -> STCayley v d
rep_∞ p = foldMap (λ (v, d) -> modifyAt (⊕ v) d (toList (p zero)))
abs_∞ :: (Ix v, Bounded v, Semiring d) => STCayley v d -> Cayley (Sparse v d)
abs_∞ q = runST (do arr <- newArray (minBound, maxBound) zero
runReaderT q arr
l <- getAssocs arr
return $ foldMap (λ (v, d) -> insertWith (⊕) v d l))
```

rep_∞ 函数使用辅助函数 modifyAt 来编辑数组中特定位置的值，这是映射上 insertWith 的对应物。

```
modifyAt :: v -> (d -> d) -> STCayley v d
modifyAt f v = do arr <- ask; x <- readArr arr v; writeArray arr v (f x)
```

使用 4.1 节的方法，Monoid 实例被证明是任何类型 m ()（其中 m 是单子）可用的通用实例。

```
instance Monoid (STCayley v d) where
zero = return ()
p ⊕ q = p >> q
```

由于我们使用 d -> STCayley v d，STCayley v d 的 Module 结构未被使用。因此，我们直接跳到 Kronecker 实例，其中使用可变数组的目的是将 delta 中 insertWith 的 O(log V) 时间复杂度降低到 modifyAt 的 O(1) 时间复杂度。

```
instance (Ix v, Semiring d) => Kronecker v d (STCayley v d) where
delta v = modifyAt (⊕one) v
```

在 d -> STCayley v d 组合中，这变为：

```
instance (Ix v, Semiring d) => Kronecker v d (d -> STCayley v d) where
delta v = λd -> modifyAt (⊕v) d
```

STCayley v d 的正确性是根据 Cayley (Sparse v d) 的正确性来建立的。

```
instance (Ix v, Ord v, Bounded v, Enum v, Semiring d, Eq d) =>
CorrectAD v d (STCayley v d) where
rep = rep_∞ . rep
abs = abs ∘ abs_∞
```

