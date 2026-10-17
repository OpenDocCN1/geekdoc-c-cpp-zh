
> 使用 `_` 代替上一步中的 `x`，因为我们没有使用它。如果我们不使用变量，编译器会产生警告。

当我们使用代数替换时，这看起来如何：

```
length (1 : 2 : 3 : Nil)    -- original call
1 + length (2 : 3 : Nil)    -- substitute using ②
1 + (1 + length (3 : Nil))   -- substitute using ②
1 + (1 + (1 + length Nil))   -- substitute using ②
1 + (1 + (1 + 0))            -- substitute using ①
1 + (1 + 1)                  -- reduce
1 + 2                        -- reduce
3                            -- reduce
```

我们有 4 次替换，这意味着我们有 4 次递归调用。`List` 越长，我们的递归调用就越多。

### 5.15. 尾递归

`length` 函数是学习 `Tail Recursion` 的绝佳示例。

在深入探讨该主题之前，我们需要谈谈大多数计算机在最低级别调用函数时的工作方式。当函数被调用时，其代码必须被执行，并且当函数完成时，程序需要返回到调用它的位置。

它知道如何返回到调用函数的方式是通过实现一个称为 *Stack* 的数据结构。

栈保存了调用过程的完整记录。就像一叠盘子，最后一个放上的盘子是第一个取下的盘子。这就是为什么栈被称为 *LIFO* 数据结构或 *后进先出*。

这里有一个例子：

```purescript
f :: Int -> Int
f x = g x ①
g :: Int -> Int
g x = h x ②
h :: Int -> Int
h x = x + 10 ③
```

+   ① `f` 调用 `g`。
+   ② `g` 调用 `h`。
+   ③ `h` 返回计算结果。

接下来，让我们看看调用 `f` 并传入 `10` 的底层过程：

```
f 10      -- original caller calls f
          -- push return address of original caller onto the Stack
g 10      -- f calls g
          -- push return address of f onto Stack
h 10      -- g calls h
          -- push return address
```

此时，栈看起来像这样：

![](img/8c0e9b687c62642e828ccb5481e11313_172_0.png)

看着这个栈，我们会按顺序返回到 g，然后是 f，最后是原始调用者。如果你把栈想象成一叠盘子，这个顺序就说得通了。

到目前为止，我们只看到了执行到调用 h 为止的情况。让我们从这一点继续执行代码：

```
h returns 20  -- pops the top of the Stack (getting g)
               -- returns 20 to g
g returns 20  -- pops the top of the Stack (getting f)
               -- returns 20 to f
f returns 20  -- pops the top of the Stack (getting original caller)
               -- returns 20 to the original caller
```

那是一个简单的例子，我们只需要栈上的 3 个槽位。

让我们回头看看我们的 length 函数：

```
length :: ∀ a. List a -> Int
length Nil      = 0
length (_ : xs) = 1 + length xs ①
```

#### ① 递归函数调用。

我们可以看到，它对列表中的每个元素都会调用一次自身。如果列表有 2 个元素，那么我们将发起 2 次调用，并需要栈上的 2 个槽位。

如果我们有一个包含 1000 个元素的列表，就需要栈上的 1000 个槽位。一百万个元素将需要一百万个槽位。

总有一天，我们会遇到一个足够长的列表，用尽栈中所有可用的槽位。这被称为栈溢出（Stack Overflow）。你可能听说过一个以这个不幸事件命名的网站。

我们的 length 函数的问题在于，它是递归的，但不是尾递归的。

> 如果函数的最后一个操作是递归调用，那么该函数就是尾递归的。

当一个函数是尾递归时，编译器可以很聪明地不在栈上保存返回位置，因为调用方函数已经没有剩余工作要做，没有理由再返回去。

这样就能避免我们的栈溢出。

下面再次给出 length：

```
length :: ∀ a. List a -> Int
length Nil      = 0
length (_ : xs) = 1 + length xs ①
```

① `length` 看起来像是尾递归，因为 `length` 调用是我们输入的最右侧内容，但它并不是最后执行的操作。在这个例子中，最后执行的是将 1 加到对 `length` 的递归调用结果上。正是这个加法导致该函数不是尾递归的。

那么，我们能否重写 `length`，使它变成尾递归呢？

我相信你已经猜到这是可能的，否则我为什么要等到现在才提起这个话题呢？

要把 `length` 重写为尾递归，我们必须先完成所有计算，然后再进行递归，这样后面就没有任何剩余工作了。

但怎么做呢？

就 `length` 而言，先做计算意味着我们要把 1 加到一个累加的 `length` 值上，然后把它传递给每次递归调用。

让我们写出这样的 `length`：

```
length :: ∀ a. Int -> List a -> Int ①
length acc Nil      = acc ②
length acc (x : xs) = length (acc + 1) xs ③
```

① 为累加中的 `length` 值在类型签名中添加了 `Int`。
② `acc` 是用于累加 `length` 值的累加器。因此，当到达列表末尾时，我们可以返回 `acc`，也就是最终的 `length` 值。
③ 现在我们是尾递归了，因为我们在递归之前先加 1，而且没有理由从递归调用返回，因为没有任何剩余工作了。

所以，我们可以恭喜自己写出了这个尾递归函数，天下太平了，对吧？

错。

我们的新版本给 `length` 的调用者带来了负担：他们必须传入 `acc` 参数，而且该参数必须以 0 开头，否则我们的 `length` 计算结果就会出错：

```
list = 1 : 2 : 3 : 4 : Nil
len = length 0 list ① ②
badLen = length 7 list ① ③
```

① 我们必须传入初始的 `length` 值，它应该是 0。
② 这次调用会产生正确的 `length` 值。
③ 这次调用会产生错误的 `length` 值，因为它会相差 7。

这很糟糕。那么，我们怎样才能鱼与熊掌兼得呢？

解决这个两难问题的办法是，用原来的类型签名来编写 `length` 函数，也就是没有 `acc` 参数。然后，我们立即调用一个私有的尾递归版 `length` 函数，我们把它命名为 `go`，并将 `acc` 参数设为 0：

```
length :: ∀ a. List a -> Int
length l = go 0 l where ① ② ③
  go :: Int -> List a -> Int ④
  go acc Nil      = acc
  go acc (_ : xs) = go (acc + 1) xs ⑤
```

① `length` 负责确保以 0 作为起始值传入。我们只需要把这处代码写对一次，而不必像之前那样在每次调用 `length` 时都传对。
② 在这种情况下，把我们的私有函数命名为 `go` 是一种惯用做法。我不太清楚这背后的历史，但这个传统始于 Haskell。
③ `go` 是私有的，因为我们是用 `where` 关键字声明它的。
④ 这就是我们把 `length` 的尾递归版本出于历史原因改名为 `go` 的实现。
⑤ 这就是我们的尾递归调用。

现在，`length` 的调用者不必担心尾递归的要求。`length` 通过确保 0 是累计 `length` 值的起始值来管理这一切。

#### 5.15.1. 关于尾递归的几点思考

尾递归非常节省栈空间，但它更难编写、更难推理，而且会让代码库更复杂。一开始就把所有递归函数都写成这种形式，被称为过早优化。我们只在必要时才优化代码。

事实证明，并非所有递归函数都能轻易写成尾递归；即使能写，函数本身的复杂度也可能使其难以维护。还有一些情况下，你虽然节省了栈空间，却转而使用了堆空间。有时候这是可以接受的，因为我们拥有的堆通常比栈大得多。

> 堆是程序可用的一个内存区域。随着程序运行，变量会从堆中分配。通常，堆比栈大得多。

所以，如果我们能轻松地把某个函数写成尾递归，那可能值得去做。但最好不要过早优化代码，而是等到真正需要时再说。重要的是要知道尾递归这种东西的存在，并且像 PureScript（和 Haskell）这样的编译器足够聪明，能够利用它。

但这并不意味着我们应该为了那 1% 的情况，让自己背负额外复杂性的负担。

### 5.16. 编写 head

有了 `length` 之后，`head` 函数应该相对容易。再次强调，在 Pursuit 中搜索时，请确保你查看的是来自 `Data.List` 的 `head`。

添加以下代码进行测试：

```
log $ show $ head Nil
log $ show $ head ("abc" : "123" : Nil)
```

① 测试空列表这种边界情况。打印 `Nothing`。
② 测试一般情况。打印 `(Just 2)`。

在这个过程中，你会遇到几个编译器问题。试着自行解决；如果卡住了，请参考下面的提示部分。

#### 5.16.1. 关于 `head` 的提示

如果你还没有写完 `head`，请先把你写的内容注释掉，然后添加下面这个 `head` 的桩版本：

```
head :: ∀ a. List a -> Maybe a
head _ = Nothing
```

这个函数只是为了让你能跟得上进度。

如果你已经完成了 `head` 函数，那么你可能注意到编译器在抱怨它不知道 `Maybe` 是什么。那是因为你需要从 `Data.Maybe` 中导入它。

所以，如果你还没有试过，请现在就这样做，然后再继续往下读。

如果你只是添加了以下代码：

```
import Data.Maybe (Maybe)
```

但现在你在 `Nothing` 和/或 `Just` 上遇到了错误，那是因为上面的导入只导入了类型 `Maybe`，并没有导入数据构造器 `Nothing` 和 `Just`。

请记住，构造类型 `Maybe` 的值的唯一方式是使用它的数据构造器。

所以我们需要把 `import` 语句改为：

```
import Data.Maybe (Maybe(..))
```

这应该能解决你与 `Maybe` 等相关的所有问题。但现在，编译器对我给你的测试代码有意见了。你可能会遇到类似这样的错误：

![](img/8c0e9b687c62642e828ccb5481e11313_177_0.png)

And if you’re like me, the first time you see this, all you can do is scratch your head and wonder. There’s a lot of information here and you can get overloaded with all of it.

The most import part for our situation is the following:

```
No type class instance was found for Data.Show.Show t2
```

The real key here is t2. That tells us that the Type Inference engine has failed to figure out a Concrete Type. If it had, it would have been something like Int, Boolean or some uppercased Type name.

But it’s lowercased meaning that it’s still a Type Parameter that the Type Inference couldn’t figure out based on how you’re using it. Why though?

To answer that, we need to look at the code in question:

```
log $ show $ head Nil
```

Now, imagine we are doing the Type Inference instead of the compiler, and we’re trying to figure out the Types in this line of code. First, we know the Types for log, show and head because those have been explicitly typed, e.g. here’s head:

```
head :: ∀ a. List a -> Maybe a
```

But what about Nil? What’s its Type?

Let’s refer back to List’s definition to see if we can ferret out it’s Type:

```
data List a = Nil | Cons a (List a)
```

If we use the Data Constructor, Nil, we will construct a Type, List a. But what Type is a?

There is no way to tell.

If we look at the other test code line I gave you, we can determine List’s Type easily:

```
log $ show $ head ("abc" : "123" : Nil)
```

It’s Type is List String.

But with an empty List, there are no elements to interrogate. It could be a List of anything, viz. List a, where a is our anything. The problem is that the compiler wants to verify that a can be passed to show (more on that later).

How do we fix this then?

Type Inference infers what Types our values are by how we use them. But when there isn’t enough evidence, as in the case of our empty List, then we must explicitly specify the Type.

Here’s how to properly do that:

```
log $ show (head Nil :: Maybe Unit)
```

We parenthesize the call to head and specify an explicit Type for its return value. But why Unit as the List element Type?

It really doesn’t matter. It just needs any valid Type that we can show (more on that later). By using Unit, we are signaling to anyone reading our code that the element Type really doesn’t matter. Had we used Int or some other non-trivial Type, the reader of our code (which could very well be us some time in the future), may think there’s more to that list than meets the eye.

Returning to the error message for a minute:

```
No type class instance was found for Data.Show.Show t2
```

It’s worth noting that during Type Inference, the compiler will "lose" your names and create any unknown type names with a t and a number. Here it has come up with t2 for our a.
