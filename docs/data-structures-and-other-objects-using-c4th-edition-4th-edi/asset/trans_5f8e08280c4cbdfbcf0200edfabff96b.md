

## 图 9.9 玩泰迪熊游戏的函数

## 函数实现

```cpp
bool bears(int initial, int goal, int increment, int n)
// Precondition: All parameters are non-negative integers.
// Postcondition: The method has determined whether it is possible to reach the goal in the
// following Teddy Bear game. In the game, your friend gives you a certain number of bears.
// The number of bears is called initial, and your goal is to end up with a particular number of
// bears, called the goal number. At any point in the game, you have two choices: (a) You can
// ask for (and receive) increment more bears, or (b) if you have an even number of bears,
// then you can give half of them back to your friend. Each time you do (a) or (b), that is called
// a step in the game.
// The return value is true if and only if the goal can be reached in n steps or fewer.
{
    if (initial == goal)
        return true;
    else if (n == 0)
        return false;
    else if (bears(initial+increment, goal, increment, n-1))
        return true;
    else if (((initial % 2 == 0) && bears(initial/2, goal, increment, n-1)))
        return true;
    else
        return false;
}
```

## 第 9.2 节自测练习

- 9. 假设你以宽度 8 和 epsilon 1 调用 random_fractal。那么 random_fractal 将进行两次递归调用，而每次调用又会进行更多调用，如此下去，直到宽度小于或等于 epsilon。包括原始调用在内，random_fractal 总共会被调用多少次？

- 10. 复制第 454 页图 9.6 中的迷宫，将魔法挂毯移到更困难的位置。运行 traverse_maze 函数，假装你身处这个迷宫并遵循函数的指示。（不要越过墙壁窥视。）

- 11. 修改 random_fractal 函数，使中点的移动不再是随机的。相反，第一个中点应向上移动 width 的量，下一层递归的中点应向下移动 width 的量，下一层再向上移动，然后向下，如此下去。

- 12. 假设你正在探索一个包含 10 行 20 列的矩形迷宫。如果你从迷宫入口开始并调用 traverse_maze，最多会产生多少次递归调用？

## 9.3 关于递归的推理

> 关于宇宙学和太阳系结构的讲座结束后，威廉·詹姆斯被一位老妇人拦住了。
>
> "詹姆斯先生，您认为太阳是太阳系的中心，地球是一个围绕其旋转的球体这一理论听起来很有说服力，但它是错误的。我有一个更好的理论，"老妇人说。
>
> "是什么理论？"詹姆斯礼貌地问道。
>
> "我们生活在地壳上，而地壳位于一只巨大的海龟背上。"
>
> 詹姆斯不希望动用他掌握的大量科学证据来粉碎这个荒谬的小理论，因此决定委婉地劝阻他的对手，让她看到自己立场的一些不足之处。
>
> "夫人，"他问道，"如果您的理论正确，那么这只海龟站在什么上面？"
>
> "詹姆斯先生，您是个非常聪明的人，这是个非常好的问题，"老妇人回答说，"但我有答案。答案是：第一只海龟站在第二只更大的海龟背上，而第二只海龟正站在它正下方。"
>
> "但这第二只海龟站在什么上面？"詹姆斯耐心地追问道。
>
> 老妇人得意地得意洋洋地说："没用的，詹姆斯先生——海龟一直延伸到底。"
>
> J. R. Ross
> 《语法中的变量约束》

在我们所有的递归思维示例中，一系列递归调用最终都达到了一个不再涉及进一步递归的调用（即，它达到了停止情况）。另一方面，如果每个递归调用都产生另一个递归调用，那么理论上递归调用将永远运行下去。这被称为无限递归。在实践中，这样的函数将运行直到计算机用于激活记录的内存耗尽并异常终止程序。换句话说，递归声明不应该是“一直递归到底”。否则，就像那位老妇人对太阳系的解释一样，递归调用将永远不会结束，除非是令人沮丧的结束。

在本节中，我们将向您展示如何推理递归函数，既证明没有无限递归，也证明递归函数的结果是正确的。作为示例，我们将从一个名为 power 的新递归函数开始，它计算形式为 x^n 的幂，其中 x 是任意双精度浮点数，n 是整数。因此，power(3.0, 2) 是 3.0^2（即 9.0），power(4.2, 3) 是 4.2^3（即 74.088）。对于任何非零的 x 值，x^0 的值定义为 1，例如 power(9.1, 0) 是 1。对于负指数 -n，返回值定义为：
x^-n = 1/x^n { x 是任意实数，且 -n 是负整数 }

例如，power(3.0, -2) 是 1/3.0^2（即 1/9）。唯一禁止的幂是当 n 不是正数时计算 0^0。以下是该函数的完整规范：

```cpp
double power(double x, int n);
// Precondition: If x is zero, then n must be positive.
// Postcondition: The value returned is x raised to the power n.
```

我们的实现首先检查前置条件，然后处理几种情况。第一种情况是 n 为非负数时，这很简单。这种情况通过将局部变量 product 设置为 1，然后反复将 product 乘以 x 来计算。重复乘法发生 n 次，如下面的 for 循环所示：

```cpp
if (n >= 0)
{
    product = 1;
    for (count = 1; count <= n; ++count)
        product = product * x;
    return product;
}
```

要了解负指数需要什么，让我们考虑一个具体的例子。假设我们正在计算 power(3.0, -2)，它必须返回值 3.0^-2。但这个值等于 1/3.0^2。负幂与分母中的正幂相同。这意味着，如果我们知道当 n 为正数时函数返回正确答案，那么我们可以通过表达式 1/power(3.0, 2) 计算出 power(3.0, -2) 的正确值。通过递归思考，每当 n 为负数时，power 可以通过递归调用来计算其答案，如下所示：

```cpp
return 1/power(x, -n); // When n is negative (and so -n is positive)
```

请记住，在这个语句中，n 是负数（例如 -2），因此 -n 是正数，因此表达式 1/power(x, -n) 中的递归函数调用具有正的第二个参数。带有正的第二个参数时，我们的 power 函数不再进行进一步的递归调用（即，停止情况），因此递归结束。

这引出了我们推理递归的第一种一般技术，可以应用于图 9.10 中的完整 power 函数：

> **一级递归**
>
> 假设每种情况要么是停止情况，要么是进行递归调用且该调用为停止情况。那么最深的递归调用仅深一层，因此不会发生无限递归。

## 图 9.10 仅具有一级递归的幂函数实现

## 函数实现

```cpp
double power(double x, int n)
// Precondition: If x is zero, then n must be positive.
// Postcondition: The value returned is x raised to the power n.
// Library facilities used: cassert
{
    double product; // The product of x with itself n times
    int count;
    if (x == 0)
        assert(n > 0);
    if (n >= 0)
    {
        product = 1;
        for (count = 1; count <= n; ++count)
            product = product * x;
        return product;
    }
    else
        return 1/power(x, -n);
}
```

## 函数的示例结果

| 使用这些参数调用 | 函数调用的返回值 |
|---|---|
| x n | |
| 3.0 2 | 9.0 |
| 2.0 -3 | 0.125 |
| 4.1 0 | 1.0 |
| -2.0 3 | -8.0 |

www.cs.colorado.edu/~main/chapter9/powers.cxx WWW

## 如何确保没有无限递归

一般来说，递归调用不会仅在一层深处停止。递归调用不需要立即达到停止情况。程序员已经开发出基于数学归纳法原理的方法，来推理超越一层深度的递归调用。这种推理可以增强您对递归函数避免无限递归的信心。作为示例，为了证明没有无限递归，让我们重写 power 函数，使其

