

在下一次对一对 A 进行比较时，情况相同；第二次比较是在索引 4（一个 C）和索引 6（一个 D）之间，因此第一组的元素前进。

| | A | A | D | R |
|---|---|---|---|---|
| S0 的 SA | 0 | 3 | 6 | 9 |

| | A | A | A | B | B | C | R |
|---|---|---|---|---|---|
| S1 和 S2 的 SA | 10 | 7 | 5 | 8 | 1 | 4 | 2 |

| 最终 SA | 10 | 7 | 0 | 3 | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 输入 S | A | B | R | A | C | A | D | A | B | R | A |
| 索引 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |

此时，在一段时间内没有平局，因此我们快速推进到每组的最后一个字符：

| | A | A | D | R |
|---|---|---|---|---|
| S0 的 SA | 0 | 3 | 6 | 9 |

| | A | A | A | B | B | C | R |
|---|---|---|---|---|---|
| S1 和 S2 的 SA | 10 | 7 | 5 | 8 | 1 | 4 | 2 |

| 最终 SA | 10 | 7 | 0 | 3 | 5 | 8 | 1 | 4 | 6 | | |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 输入 S | A | B | R | A | C | A | D | A | B | R | A |
| 索引 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |

最后，我们到达末尾。两个 R 之间的比较要求我们比较下一个字符，它们位于索引 10 和 3。由于此比较是在 S1 元素和 S0 元素之间，如前所述，我们无法查找结果并必须直接比较。但它们也是相同的，因此现在我们必须比较索引 11 和 4，索引 11 自动获胜（因为它已超过字符串末尾）。因此索引 9 中的 R 前进，然后我们可以完成合并。请注意，如果我们未到达字符串末尾，本可以利用这样一个事实：S2 元素和 S1 元素之间的比较意味着顺序可以从 S1 + S2 的后缀数组中获得。

| | A | A | D | R |
|---|---|---|---|---|
| S0 的 SA | 0 | 3 | 6 | 9 |

| | A | A | A | B | B | C | R |
|---|---|---|---|---|---|
| S1 和 S2 的 SA | 10 | 7 | 5 | 8 | 1 | 4 | 2 |

| 最终 SA | 10 | 7 | 0 | 3 | 5 | 8 | 1 | 4 | 6 | 9 | 2 |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 输入 S | A | B | R | A | C | A | D | A | B | R | A |
| 索引 | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |

```cpp
/**
 * Fill in the suffix array information for String str
 * str is the Input String
 * sa is an existing array to place the suffix array
 * LCP is an existing array to place the LCP information
 */
void createSuffixArray( const string & str, vector<int> & sa, vector<int> & LCP )
{
    if( sa.size( ) != str.length( ) || LCP.size( ) != str.length( ) )
        throw invalid_argument( "Mismatched vector sizes" );
    int N = str.length( );
    vector<int> s( N + 3 );
    vector<int> SA( N + 3 );
    for( int i = 0; i < N; ++i )
        s[ i ] = str[ i ];
    makeSuffixArray( s, SA, N, 250 );
    for( int i = 0; i < N; ++i )
        sa[ i ] = SA[ i ];
    makeLCPArray( s, sa, LCP );
}
```

图 12.32 用于设置对 makeSuffixArray 的首次调用的代码；创建适当大小的数组，并为保持简单，仅使用 256 个 ASCII 字符代码

由于这是标准合并，每对后缀最多进行两次比较，因此此步骤耗时线性。整个算法因此满足 T(N) = T(2N/3) + O(N) 并耗时线性。虽然我们只计算了后缀数组，但 LCP 信息也可以在算法运行时计算，但涉及一些棘手的细节，通常 LCP 信息是由单独的线性时间算法计算的。

最后，我们提供一个可用于计算后缀数组的工作实现；而不是完全实现步骤 1 来对原始字符进行排序，我们将假设字符串中仅存在一小组 ASCII 字符（位于值 1–255）。在图 12.32 中，我们分配带有三个预留填充槽的数组并调用 makeSuffixArray，即基本的线性时间算法。

图 12.33 显示了 makeSuffixArray。在第 11 到 15 行，它分配所有所需的数组，并确保 S0 和 S1 具有相同数量的元素（第 16 到 21 行）；然后它将工作委派给 assignNames、computeS12、computeS0 和 merge。

```
1 // find the suffix array SA of s[0..n-1] in {1..K}^n
2 // requires s[n]=s[n+1]=s[n+2]=0, n>=2
3 void makeSuffixArray( const vector<int> & s, vector<int> & SA, int n, int K )
4 {
5   int n0 = ( n + 2 ) / 3;
6   int n1 = ( n + 1 ) / 3;
7   int n2 = n / 3;
8   int t = n0 - n1; // 1 iff n%3 == 1
9   int n12 = n1 + n2 + t;
10
11  vector<int> s12( n12 + 3 );
12  vector<int> SA12( n12 + 3 );
13  vector<int> s0( n0 );
14  vector<int> SA0( n0 );
15
16  // generate positions in s for items in s12
17  // the "4*" adds a dummy mod 1 suffix if n%3 == 1
18  // at that point, the size of s12 is n12
19  for( int i = 0, j = 0; i < n + t; ++i )
20    if( i % 3 != 0 )
21      s12[ j++ ] = i;
22
23  int K12 = assignNames( s, s12, SA12, n0, n12, K );
24  computeS12( s12, SA12, n2, K12 );
25  computeS0( s, s0, SA0, SA12, n12, n0, n2, K );
26  merge( s, s12, SA, SA0, SA12, n, n0, n12, t );
27 }
```

图 12.33 线性时间后缀数组构建的主例程

```
// Assigns the new supercharacter names.
// At end of routine, SA will have indices into s, in sorted order
// and s12 will have new character names
// Returns the number of names assigned; note that if
// this value is the same as n12, then SA is a suffix array for s12.
int assignNames( const vector<int>& s, vector<int>& s12, vector<int>& SA12,
                 int n0, int n12, int K )
{
   // radix sort the new character trios
   radixPass( s12,  SA12,  s,  2, n12, K );
   radixPass( SA12, s12 ,  s,  1, n12, K );
   radixPass( s12 , SA12, s,  0, n12, K );
   // find lexicographic names of triples
   int name = 0;
   int c0 = -1, c1 = -1, c2 = -1;
   for( int i = 0; i < n12; ++i )
   {
      if( s[ SA12[ i ] ] != c0 || s[ SA12[ i ] + 1 ] != c1 ||
          s[ SA12[ i ] + 2 ] != c2 )
      {
         ++name;
         c0 = s[ SA12[ i ] ];
         c1 = s[ SA12[ i ] + 1 ];
         c2 = s[ SA12[ i ] + 2 ];
      }
      if( SA12[ i ] % 3 == 1 )
         s12[ SA12[ i ] / 3 ]      = name; // S1
      else
         s12[ SA12[ i ] / 3 + n0 ] = name; // S2
   }
   return name;
}
```

图 12.34 用于计算和分配三字符名称的例程

如图 12.34 所示，assignNames 首先执行三遍基数排序。然后，它按顺序分配名称（即数字），如果当前项目的三字符组与前一项不同，则使用下一个可用数字（回顾三字符组已由三遍基数排序排序，并且回顾 S0 和 S1 大小相同，因此在第 32 行，添加 n0 会增加 S1 中的元素数量）。我们可以使用第 7 章中的基本计数基数排序来获得线性时间排序。此代码显示在图 12.35 中。数组 in 表示对 s 的索引；排序结果的

```
1 // stably sort in[0..n-1] with indices into s that has keys in 0..K
2 // into out[0..n-1]; sort is relative to offset into s
3 // uses counting radix sort
4 void radixPass( const vector<int>& in, vector<int>& out,
5                 const vector<int>& s, int offset, int n, int K )
6 {
7     vector<int> count( K + 2 );    // counter array
8
9     for( int i = 0; i < n; ++i )
10        ++count[ s[ in[ i ] + offset ] + 1 ];    // count occurrences
11
12    for( int i = 1; i <= K + 1; ++i )    // compute exclusive sums
13        count[ i ] += count[ i - 1 ];
14
15    for( int i = 0; i < n; ++i )    // sort
16        out[ count[ s[ in[ i ] + offset ] ]++ ] = in[ i ];
17 }
```

```
18 // stably sort in[0..n-1] with indices into s that has keys in 0..K
19 // into out[0..n-1]
20 // uses counting radix sort
21 void radixPass( const vector<int>& in, vector<int>& out,
22                 const vector<int>& s, int n, int K )
23 {
24     radixPass( in, out, s, 0, n, K );
25 }
```

图 12.35 用于后缀数组的计数基数排序

基数排序的特点是索引被排序，使得 s 中的字符在这些索引处排序（索引按指定偏移量）。

图 12.36 包含用于计算 s12 和随后 s0 的后缀数组的例程。

最后，合并例程显示在图 12.37 中，一些支持例程在图 12.38 中。合并例程的基本外观和感觉与图 7.12 中看到的标准合并算法相同。

### 12.5 k-d 树

假设一家广告公司维护一个数据库，需要为某些选民生成邮寄标签。典型请求可能要求向年龄在 34 到 49 岁之间且年收入在 100,000 美元到 150,000 美元之间的人发送邮件。此问题称为二维范围查询。在一维中，该问题可以通过简单的递归算法在 O(M + log N) 平均时间内解决，方法是遍历预构建的二叉搜索树。这里 M 是数量

