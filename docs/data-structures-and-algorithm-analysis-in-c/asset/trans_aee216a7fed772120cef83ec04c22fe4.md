

/**
 * Cubic maximum contiguous subsequence sum algorithm.
 */
int maxSubSum( const vector< int > & a )
{
    int maxSum = 0;

    for( int i = 0; i < a.size( ); ++i )
        for( int j = i; j < a.size( ); ++j )
        {
            int thisSum = 0;

            for( int k = i; k < j; ++k )
                thisSum += a[ k ];

            if( thisSum > maxSum )
                maxSum = thisSum;
        }

    return maxSum;
}

### 图 2.5 算法 1

事实证明，更精确的分析（考虑到这些循环的实际大小）表明答案是 \(\Theta(N^3)\)，而我们上面的估计高出了 6 倍（这没关系，因为常数不重要）。这在一般这类问题中都成立。精确分析是从求和 \(\sum_{i=0}^{N-1} \sum_{j=i}^{N-1} \sum_{k=i}^{j} 1\) 得到的，它告诉我们第 14 行被执行了多少次。该求和可以从内到外求值，使用第 1.2.3 节中的公式。特别是，我们将使用前 N 个整数和前 N 个平方数的求和公式。首先，我们有

\(\sum_{k=i}^{j} 1 = j - i + 1\)

接下来我们求值

\(\sum_{j=i}^{N-1} (j - i + 1) = \frac{(N - i + 1)(N - i)}{2}\)

这个求和可以通过观察得出，它只是前 \(N - i\) 个整数的和。为了完成计算，我们求值

\(\sum_{i=0}^{N-1} \frac{(N-i+1)(N-i-1)}{2} = \sum_{i=1}^{N} \frac{(N-i+1)(N-i+2)}{2}\)
\(= \frac{1}{2} \sum_{i=1}^{N} N^2 - \left(N + \frac{3}{2}\right) \sum_{i=1}^{N} i + \frac{1}{2} \sum_{i=1}^{N} (N^2 + 3N + 2) \sum_{i=1}^{N} 1\)
\(= \frac{1}{2} \frac{N(N+1)(2N+1)}{6} - \left(N + \frac{3}{2}\right) \frac{N(N+1)}{2} + \frac{N^2 + 3N + 2}{2} N\)
\(= \frac{N^2 + 3N + 2N}{6}\)

我们可以通过去掉一个 for 循环来避免立方运行时间。这并不总是可行的，但在这种情况下，算法中存在大量不必要的计算。改进算法纠正的低效率可以通过注意到 \(\sum_{i=k}^{N} A_k = \sum_{i=1}^{N} A_k\) 来看出，因此算法 1 中第 13 行和第 14 行的计算代价过高。图 2.6 显示了一个改进的算法。算法 2 显然是 \(O(N^2)\)；分析比之前更简单。

/**
 * Quadratic maximum contiguous subsequence sum algorithm.
 */
int maxSubSum2( const vector<int> & a )
{
  int maxSum = 0;

  for( int i = 0; i < a.size( ); ++i )
  {
    int thisSum = 0;
    for( int j = i; j < a.size( ); ++j )
    {
      thisSum += a[ j ];

      if( thisSum > maxSum )
        maxSum = thisSum;
    }
  }

  return maxSum;
}

### 图 2.6 算法 2

然后递归地求解这些子问题。这是“分解”部分。“合并”阶段包括将两个子问题的解拼合在一起，并可能进行少量额外工作，以得到整个问题的解。

在我们的情况中，最大子序列和可能出现在三个位置之一。要么它完全出现在输入的左半部分，要么完全出现在右半部分，要么它跨越中间并同时出现在两个半部分中。前两种情况可以递归求解。最后一种情况可以通过找到第一个半部分中包含第一个半部分最后一个元素的最大和，以及第二个半部分中包含第二个半部分第一个元素的最大和来得到。然后可以将这两个和相加。例如，考虑以下输入：

| 第一半 | 第二半 |
| :--- | :--- |
| 4 -3 5 -2 | -1 2 6 -2 |

第一个半部分的最大子序列和为 6（元素 A1 到 A3），第二个半部分为 8（元素 A6 到 A7）。

第一个半部分中包含第一个半部分最后一个元素的最大和为 4（元素 A1 到 A4），第二个半部分中包含第二个半部分第一个元素的最大和为 7（元素 A5 到 A7）。因此，跨越两个半部分并经过中间的最大和为 4 + 7 = 11（元素 A1 到 A7）。

因此，我们看到，在形成大最大子序列的三种方式中，对于我们的示例，最佳方式是包含两个半部分的元素。因此，答案是 11。图 2.7 展示了这种策略的实现。

算法 3 的代码值得评论。递归函数调用的一般形式是传递输入数组以及左右边界，这些边界界定了被操作的数组部分。一个单行驱动程序通过传递边界 0 和 N – 1 以及数组来设置此过程。

第 8 到 12 行处理基本情况。如果 left == right，则只有一个元素，如果该元素非负，则它是最大子序列。left > right 的情况不可能发生，除非 N 为负（尽管代码中的微小扰动可能会搞乱这一点）。第 15 和 16 行执行两个递归调用。我们可以看到，递归调用始终处理比原始问题更小的问题，尽管代码中的微小扰动可能会破坏这一属性。第 18 到 24 行和 26 到 32 行计算触及中心分隔线的两个最大和。这两个值的和是跨越两个半部分的最大和。例程 max3（未显示）返回三种可能性中最大的一个。

算法 3 显然比之前的两个算法都需要更多的编码工作。然而，代码更短并不总是意味着代码更好。正如我们在之前显示算法运行时间的表格中所见，对于除最小输入大小以外的所有情况，该算法比其他两个算法快得多。

运行时间分析与计算斐波那契数的程序类似。设 T(N) 为求解大小为 N 的最大子序列和问题所需的时间。如果 N = 1，则程序执行第 8 到 12 行需要一些常数时间，我们将其称为一个单位。因此，T(1) = 1。否则，

```
1 /**
2  * Recursive maximum contiguous subsequence sum algorithm.
3  * Finds maximum sum in subarray spanning a[left..right].
4  * Does not attempt to maintain actual best sequence.
5  *
6  * int maxSubRec( const vector<int>& a, int left, int right )
7  {
8  if( left == right )  // Base case
9  {
10  if( a[ left ] > 0 )
11  return a[ left ];
12  else
13  return 0;
14 }
15
16 int center = ( left + right ) / 2;
17 int maxLeftSum  = maxSubRec( a, left, center );
18 int maxRightSum = maxSubRec( a, center + 1, right );
19
20 int maxLeftBorderSum = 0, leftBorderSum = 0;
21 for( int i = center; i >= left; --i )
22 {
23  leftBorderSum += a[ i ];
24  if( leftBorderSum > maxLeftBorderSum )
25  maxLeftBorderSum = leftBorderSum;
26 }
27
28 int maxRightBorderSum = 0, rightBorderSum = 0;
29 for( int j = center + 1; j <= right; ++j )
30 {
31  rightBorderSum += a[ j ];
32  if( rightBorderSum > maxRightBorderSum )
33  maxRightBorderSum = rightBorderSum;
34 }
35
36 return max3( maxLeftSum, maxRightSum,
37  maxLeftBorderSum + maxRightBorderSum );
38 }
39
40 /**
41  * Driver for divide-and-conquer maximum contiguous
42  * subsequence sum algorithm.
43  */
44 int maxSubSum3( const vector<int>& a )
45 {
46  return maxSubRec( a, 0, a.size( ) - 1 );
47 }
```

### 图 2.7 算法 3

程序必须执行两个递归调用、第 19 到 32 行之间的两个 for 循环，以及少量的记账工作，例如第 14 行和第 34 行。这两个 for 循环合起来遍历子数组中的每个元素，循环内部有常数工作量，因此第 19 到 32 行花费的时间是 O(N)。第 8 到 14 行、18、26 和 34 行的代码都是常数工作量，因此与 O(N) 相比可以忽略不计。其余工作在第 15 和 16 行完成。这些行求解两个大小为 N/2 的子序列问题（假设 N 是偶数）。因此，这些行各花费 T(N/2) 单位时间，总共为 2T(N/2)。算法的总时间为 2T(N/2) + O(N)。这给出了以下方程

T(1) = 1
T(N) = 2T(N/2) + O(N)

为了简化计算，我们可以将上述方程中的 O(N) 项替换为 N，因为 T(N) 无论如何都将用大 O 表示法表示，这不会影响答案。在第 7 章中，我们将看到如何严格地求解这个方程。目前，如果 T(N) = 2T(N/2) + N，且 T(1) = 1，则 T(2) = 4 = 2 * 2，T(4) = 12 = 4 * 3，T(8) = 32 = 8 * 4，T(16) = 80 = 16 * 5。显而易见且可推导的规律是，如果 N = 2^k，则 T(N) = N * (k + 1) = N log N + N = O(N log N)。

此分析假设 N 是偶数，因为否则 N/2 未定义。由于分析的递归性质，它仅在 N 是 2 的幂时才真正有效，因为否则我们最终会得到一个大小不是偶数的子问题，方程无效。当 N 不是 2 的幂时，需要稍微复杂一些的分析，但大 O 结果保持不变。

在未来的章节中，我们将看到递归的几个巧妙应用。在这里，我们介绍了第四个算法来查找最大子序列和。这个算法比递归算法更容易实现，而且效率也更高。它如图 2.8 所示。

时间边界正确的原因应该是显而易见的，但要理解算法为何实际有效需要稍加思考。为了概述逻辑，请注意，与算法 1 和 2 类似，j 表示当前序列的结束，而 i 表示当前序列的开始。如果我们不需要知道实际最佳子序列的位置，则可以将 i 的使用从程序中优化掉，但在设计算法时，让我们假设 i 是需要的，并且我们正在尝试改进算法 2。一个观察是，如果 a[i] 为负，那么它不可能是最优子序列的起始，因为任何以包含 a[i] 开头的子序列都可以通过从 a[i+1] 开头来改进。同样，任何负子序列都不可能是最优子序列的前缀（相同逻辑）。如果在内层循环中，我们检测到从 a[i] 到 a[j] 的子序列为负，那么我们可以推进 i。关键的观察是，我们不仅可以将 i 推进到 i + 1，还可以实际上将 i 一直推进到 j + 1。要理解这一点，设 p 为 i + 1 和 j 之间的任何索引。任何从索引 p 开始的子序列都不会比从索引 i 开始并包含从 a[i] 到 a[p - 1] 的子序列的相应子序列更长，因为后者子序列不是负的（j 是导致从索引 i 开始的子序列变为负的第一个索引）。因此，将 i 推进到 j + 1 是无风险的；我们不会错过最优解。

这个算法是许多巧妙算法的典型：运行时间显而易见，但正确性并非如此。对于这些算法，正式的正确性证明（更正式的

