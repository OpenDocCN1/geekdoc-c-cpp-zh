
```ada
(for all J in Items'Range =>
    (for all K in J + 1 .. Items'Last => Items(J) <= Items(K)));
end Searchers;
```

该前置条件使用两个嵌套的全称量化表达式来断言数组中的每一项都位于（或等于）其后的所有项之前。SPARK 工具将照常在每个调用 `Binary_Search` 的位置创建一个验证条件，以证明该前置条件得到满足。

值得反复强调的是，Ada 中的断言是可执行的。考虑到这一点，请注意为 `Binary_Search` 给出的前置条件运行时间为 `$O(n^2)$`。相比之下，二分查找算法本身只运行 `$O(\log n)$` 时间。

表达数组已排序的另一种方式是

```ada
Pre => (for all J in Items'First .. Items'Last - 1 =>
            Items (J) <= Items (J+1))
```

这种方式的优点是运行时间仅为 `$O(n)$`，而且也可能被认为更清晰。然而，与它所附着的算法相比，它的渐近速度仍然更慢。由于断言可以在大型数组上使用量化表达式，甚至调用递归函数，因此它们可能消耗大量空间和时间。因此，表达力强的断言有可能使一个原本具有可接受性能特征的程序变得不可用。我们将在第 6.8 节进一步讨论这个问题。

### 6.2.2 *后置条件*

*后置条件*是一种在子程序完成其动作并将控制权返回给调用者时断言为真的条件。它描述子程序的效果。因此，后置条件是从我们的程序必须满足的功能需求中推导出的形式化陈述。

后置条件通过 `Post` 方面（aspect）引入。作为示例，再次考虑 `Searchers` 包。下面给出该包的一个版本，其中 `Binary_Search` 过程已被赋予一个后置条件：

```ada
package Searchers2
   with SPARK_Mode => On
is
   subtype Index_Type is Positive range 1 .. 100;
   type Array_Type is array (Index_Type) of Integer;

   procedure Binary_Search (Search_Item : in  Integer;
                            Items       : in  Array_Type;
                            Found       : out Boolean;
                            Result      : out Index_Type)
      with
         Pre  => (for all J in Items'Range =>
                     (for all K in J + 1 .. Items'Last => Items(J) <= Items(K))),
         Post => (if Found then Search_Item = Items (Result)
                     else (for all J in Items'Range => Search_Item /= Items(J)));
end Searchers2;
```

该后置条件表示：如果过程报告已找到搜索项，那么该项存在于数组中报告的位置。else 子句表示：如果过程没有找到搜索项，那么该项不存在于数组中的任何位置。

前置条件和后置条件具有对偶关系。前置条件是调用者的义务，需要在调用子程序之前通过运行时测试或证明来表明该条件为真。在子程序内部，前置条件可用于验证条件的假设中，在子程序体的上下文中被视为已知条件。

另一方面，后置条件是子程序自身的义务，需要表明当子程序返回时该条件为真。调用上下文可以在调用点之后出现的验证条件的假设中使用后置条件。

调用者感兴趣的是易于证明的弱前置条件，以及能提供大量可在调用后使用的信息的强后置条件。相反，实现者希望得到在所要实现的子程序中提供大量信息的强前置条件，以及易于证明的弱后置条件。调用的双方都希望尽可能少地做出承诺，但尽可能多地获得承诺。

当然，在实际程序中，正如在现实生活中一样，必须取得平衡。后置条件描述子程序正确意味着什么，因此理想情况下应作为子程序设计的一部分来编写。后置条件越具体（越强），它捕获的关于子程序行为的信息就越多。通常需要提供前置条件来支持后置条件。

例如，对于 `Binary_Search`，除非实现“知道”数组已经排序，否则它没有机会证明后置条件。该算法依赖于这一点。因此，如果要证明后置条件，前置条件是必要的。

`Binary_Search` 过程只有 `in` 和 `out` 参数。对于 `in out` 参数（或 `In_Out` 全局项），有时需要在后置条件中引用参数（或全局项）的原始值。作为示例，考虑一个过程，它求一个自然数的最小质因数，并在将该因数除出后返回该因数和原始数：

```ada
procedure Smallest_Factor (N     : in out Positive;
                           Factor :    out Positive)
   with
      Post => Is_Prime(Factor) and
              (N = N'Old / Factor) and
              (N'Old rem Factor = 0);
```

这里我们使用一个函数 `Is_Prime`，当且仅当其参数是质数时返回真。

该过程会改变 `N` 的值。然而，我们可以在后置条件中使用 `'Old` 属性引用其原始值。这意味着编译器必须在调用过程之前维护 `N` 值的一个副本，以便在计算后置条件时使用该副本。这里，`N` 只是一个整数，因此保留它的副本并不昂贵。然而，这是断言可能潜在地消耗大量资源的另一个例子；考虑参数是大型数据结构的情况。

一般来说，我们可以将子程序的*前状态*称为子程序开始执行之前整个程序的状态。类似地，我们可以将子程序的*后状态*称为子程序返回之后整个程序的状态。用这些术语来说，`'Old` 属性可以说会复制前状态的一部分，以便在计算后置条件时使用。

在将 `'Old` 与数组一起使用时需要小心。考虑以下四个表达式。这里，`A` 是一个数组，`Index` 是数组索引子类型的变量。

- `A'Old(Index)` 访问由当前 `Index` 所给位置处的原始数组元素。这里，*原始*表示前状态的一部分，而*当前*表示后置条件执行时的值，即后状态的一部分。
- `A(Index'Old)` 访问由原始 `Index` 所给位置处的当前数组元素。
- `A'Old(Index'Old)` 访问由原始 `Index` 所给位置处的原始数组元素。当进入子程序时，原始数组（整体）和原始 `Index` 都会被保存。
- `A(Index)'Old` 与 `A'Old(Index'Old)` 大致相同。特别地，它引用表达式 `A(Index)` 的原始值。然而，当进入子程序时，只保存 `A(Index)` 的原始值，而不是整个数组。

最后一种情况说明了一条通用规则。`'Old` 的前缀可以是任意表达式，其值在进入子程序时被保存。例如，后置条件中的 `(X + Y)'Old` 会导致表达式 `X + Y` 的原始值被保存，并在计算后置条件时使用。后置条件中每次使用 `'Old` 都意味着创建一个单独的保存值。我们还注意到，由于用作 `'Old` 前缀的表达式会被复制，因此它不能具有受限类型。⁷

前面展示的 `Smallest_Factor` 的后置条件并未完全描述该过程的预期行为。它只说明 `Factor` 是 `N` 原始值的某个质因数，但不一定是最小的那个。尽管该后置条件没有达到它所能达到的强度，但它仍然向调用上下文传递了有用的信息。证明该后置条件将始终得到满足，是对该过程正确性的部分证明。其余性质可以通过测试来探索。我们将在第 8.4 节更详细地描述证明与测试之间的相互作用。

该后置条件可以加强如下：

```ada
procedure Smallest_Factor (N      : in out Positive;
                           Factor : out Positive)
   with
      Post => (N = N'Old / Factor) and
              (N'Old rem Factor = 0) and
              (for all J in 2 .. Factor - 1 => N'Old rem J /= 0);
```

新增的量化表达式表示，原始 `N` 没有比 `Factor` 更小的其他因数。不再需要直接断言 `Factor` 是质数，因为一个数的最小因数总是质数，这是一个数学事实。注意，现在后置条件依赖于一个在程序范围之外证明的数学性质。这是设计与实现之间相互作用的一个例子。尽管 SPARK 允许你将软件的构造形式化，但它本身并不是一套完整的形式化设计方法。

函数结果通常是匿名的，因此要在函数的后置条件中引用它们，必须使用 `'Result` 属性。考虑 `Smallest_Factor` 的一个函数版本，它返回一个自然数的最小因数：

```ada
function Smallest_Factor (N : in Positive) return Positive
   with
      Post => (N rem Smallest_Factor'Result = 0) and
              (for all J in 2 .. Smallest_Factor'Result - 1 => N rem J /= 0);
```
