

```cpp
// Returns true if word1 and word2 are the same length
// and differ in only one character.
bool oneCharOff( const string & word1, const string & word2 )
{
    if( word1.length( ) != word2.length( ) )
        return false;

    int diffs = 0;

    for( int i = 0; i < word1.length( ); ++i )
        if( word1[ i ] != word2[ i ] )
            if( ++diffs > 1 )
                return false;

    return diffs == 1;
}
```

图 4.70 检查两个单词是否仅有一个字符不同的例程

```cpp
// Computes a map in which the keys are words and values are vectors of words
// that differ in only one character from the corresponding key.
// Uses a quadratic algorithm.
map<string,vector<string>> computeAdjacentWords( const vector<string> & words )
{
    map<string,vector<string>> adjWords;

    for( int i = 0; i < words.size( ); ++i )
        for( int j = i + 1; j < words.size( ); ++j )
           if( oneCharOff( words[ i ], words[ j ] ) )
           {
               adjWords[ words[ i ] ].push_back( words[ j ] );
               adjWords[ words[ j ] ].push_back( words[ i ] );
           }

    return adjWords;
}
```

图 4.71 计算包含单词作为键和仅有一个字符不同的单词向量作为值的映射的函数。此版本在 89,000 词的词典上运行需要 1.5 分钟。

存储每个集合，相同的惯用法也适用。代码如图 4.72 所示。第 8 行显示第二个映射的声明，第 11 行和第 12 行填充映射，然后使用额外的循环遍历每个单词组。与第一个算法相比，第二个算法编码难度仅略大，运行时间为 18 秒，大约快六倍。

```cpp
// Computes a map in which the keys are words and values are vectors of words
// that differ in only one character from the corresponding key.
// Uses a quadratic algorithm, but speeds things up a little by
// maintaining an additional map that groups words by their length.
map<string,vector<string>> computeAdjacentWords( const vector<string> & words )
{
   map<string,vector<string>> adjWords;
   map<int,vector<string>> wordsByLength;

   // Group the words by their length
   for( auto & thisWord : words )
      wordsByLength[ thisWord.length( ) ].push_back( thisWord );

   // Work on each group separately
   for( auto & entry : wordsByLength )
   {
      const vector<string> & groupsWords = entry.second;

      for( int i = 0; i < groupsWords.size( ); ++i )
         for( int j = i + 1; j < groupsWords.size( ); ++j )
            if( oneCharOff( groupsWords[ i ], groupsWords[ j ] ) )
            {
               adjWords[ groupsWords[ i ] ].push_back( groupsWords[ j ] );
               adjWords[ groupsWords[ j ] ].push_back( groupsWords[ i ] );
            }
   }

   return adjWords;
}
```

图 4.72. 计算包含单词作为键和仅有一个字符不同的单词向量作为值的映射的函数。它按单词长度将单词分组。此版本在 89,000 词的词典上运行需要 18 秒。

我们的第三个算法更复杂，并使用了额外的映射！与之前一样，我们按单词长度对单词进行分组，然后分别处理每个组。为了了解该算法的工作原理，假设我们正在处理长度为 4 的单词。首先，我们想找到单词对，例如 wine 和 nine，它们除了第一个字母外完全相同。实现这一点的方法如下：对于每个长度为 4 的单词，删除第一个字符，留下一个三个字符的单词代表。构建一个映射，其中键是代表，值是所有具有该代表的单词的向量。例如，在考虑四字母单词组的第一个字符时，代表“ine”对应“dine”、“fine”、“wine”、“nine”、“mine”、“vine”、“pine”、“line”。代表“oot”对应“boot”、“foot”、“hoot”、“loot”、“soot”、“zoot”。这个最新映射中的每个单独向量作为值，构成一个单词团，其中任何单词都可以通过单字符替换变为任何其他单词，因此在构建这个最新映射后，很容易遍历它并将条目添加到正在计算的原始映射中。然后我们将继续处理四字母单词组的第二个字符，使用一个新映射，然后是第三个字符，最后是第四个字符。

The general outline is

```
for each group g, containing words of length len
  for each position p (ranging from 0 to len-1)
  {
    Make an empty map<string,vector<string>> repsToWords
    for each word w
    {
      Obtain w's representative by removing position p
      Update repsToWords
    }
    Use cliques in repsToWords to update adjWords map
  }
```

图 4.73 包含该算法的实现。运行时间改进为两秒。值得注意的是，虽然使用额外的映射使算法更快，语法也相对简洁，但代码并未利用映射的键保持有序这一事实。

```cpp
// Computes a map in which the keys are words and values are vectors of words
// that differ in only one character from the corresponding key.
// Uses an efficient algorithm that is O(N log N) with a map
map<string,vector<string>> computeAdjacentWords( const vector<string>& words )
{
    map<string,vector<string>> adjWords;
    map<int,vector<string>> wordsByLength;
    // Group the words by their length
    for( auto & str : words )
        wordsByLength[ str.length() ].push_back( str );
    // Work on each group separately
    for( auto & entry : wordsByLength )
    {
        const vector<string>& groupsWords = entry.second;
        int groupNum = entry.first;
        // Work on each position in each group
        for( int i = 0; i < groupNum; ++i )
        {
            // Remove one character in specified position, computing representative.
            // Words with same representatives are adjacent; so populate a map ...
            map<string,vector<string>> repToWord;

            for( auto & str : groupsWords )
            {
                string rep = str;
                rep.erase( i, 1 );
                repToWord[ rep ].push_back( str );
            }

            // and then look for map values with more than one string
            for( auto & entry : repToWord )
            {
                const vector<string> & clique = entry.second;
                if( clique.size() > 2 )
                for( int p = 0; p < clique.size(); ++p )
                for( int q = p + 1; q < clique.size(); ++q )
                {
                    adjWords[ clique[ p ] ].push_back( clique[ q ] );
                    adjWords[ clique[ q ] ].push_back( clique[ p ] );
                }
            }
        }
    }

    return adjWords;
}
```

![](img/e449061a0cac9cafaefd979fab665b33_198_0.png)

图 4.73（续）

因此，支持映射操作但不保证有序的数据结构可能性能更好，因为它被要求做的工作更少。第 5 章探讨了这种可能性，并讨论了 C++11 添加到标准库的替代映射实现背后的思想，即 unordered_map。无序映射将实现的运行时间从 2 秒缩短到 1.5 秒。

## 摘要

我们已经看到了树在操作系统、编译器设计和搜索中的应用。表达式树是一种更通用结构（称为分析树）的一个小示例，分析树是编译器设计中的核心数据结构。分析树不是二叉树，而是表达式树的相对简单的扩展（尽管构建它们的算法并不那么简单）。

搜索树在算法设计中至关重要。它们支持几乎所有有用的操作，且对数平均开销非常小。搜索树的非递归实现快一些，但递归版本更简洁、更优雅，也更容易理解和调试。搜索树的问题在于，其性能在很大程度上取决于输入是否随机。如果不是这种情况，运行时间会显著增加，以至于搜索树变成昂贵的链表。

我们看到了几种处理这个问题的方法。AVL 树通过坚持所有节点的左子树和右子树高度差最多为 1 来工作。这确保了树不会太深。不改变树的操作（如插入）都可以使用标准的二叉搜索树代码。改变树的操作必须恢复树。这可能有些复杂，尤其是在删除的情况下。我们展示了如何在 O(log N) 时间内在插入后恢复树。

我们还研究了伸展树。伸展树中的节点可以变得任意深，但在每次访问后，树都会以一种有些神秘的方式进行调整。净效果是，任何 M 次操作的序列都需要 O(M log N) 时间，这与平衡树所需的时间相同。

B 树是平衡的 M-way 树（与 2-way 或二叉树相对），非常适合磁盘；一种特例是 2-3 树（M = 3），这是实现平衡搜索树的另一种方式。

在实践中，所有平衡树方案的运行时间，虽然搜索稍快，但插入和删除比简单的二叉搜索树差（常数因子），但考虑到对容易获得的最坏情况输入所提供的保护，这通常是可以接受的。第 12 章讨论了一些额外的搜索树数据结构并提供了详细的实现。

最后说明：通过将元素插入搜索树，然后执行中序遍历，我们可以获得排序后的元素。这给出了一个 O(N log N) 排序算法，如果使用任何复杂的搜索树，这是最坏情况界限。我们将在第 7 章看到更好的方法，但没有一种具有更低的时间界限。

## 练习

- 4.1 对于图 4.74 中的树：
  - a. 哪个节点是根？
  - b. 哪些节点是叶子？

- 4.2 对于图 4.74 树中的每个节点：
  - a. 指出父节点。
  - b. 列出子节点。
  - c. 列出兄弟节点。
  - d. 计算深度。
  - e. 计算高度。

- 4.3 图 4.74 中树的深度是多少？

- 4.4 证明在 N 个节点的二叉树中，有 N + 1 个表示子节点的空指针链接。

