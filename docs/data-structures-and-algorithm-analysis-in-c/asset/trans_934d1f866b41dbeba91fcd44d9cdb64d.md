

散列函数利用允许溢出的事实，并使用 unsigned int 以避免引入负数。

图 5.4 中描述的散列函数不一定在表分布方面是最好的，但它确实具有极度简单的优点，并且速度相当快。如果键非常长，散列函数计算起来会花费太多时间。在这种情况下，常见的做法是不使用所有字符。此时，键的长度和特性将影响选择。例如，键可以是一个完整的街道地址。散列函数可能会从街道地址中选择几个字符，也许还会从城市名称和邮政编码中选择几个字符。一些程序员通过仅使用奇数位置上的字符来实现他们的散列函数，其想法是计算散列函数节省的时间将弥补稍微不够均匀分布的函数。

剩下的主要编程细节是冲突解决。当插入一个元素时，如果它散列到与已插入元素相同的值，那么我们就发生了冲突并需要解决它。有几种方法可以处理这个问题。我们将讨论两种最简单的方法：分离链接和开放寻址；然后我们将看一些最近发现的替代方案。

## 5.3 分离链接

第一种策略，通常称为分离链接，是保留一个所有散列到相同值的元素的列表。我们可以使用标准库的列表实现。如果空间紧张，最好避免使用它们（因为这些列表是双向链接的并浪费空间）。在本节中，我们假设键是前 10 个完全平方数，但散列函数只是 hash(x) = x mod 10。（表大小不是质数，但这里为简单起见使用。）图 5.5 显示了结果的分离链接散列表。

执行搜索时，我们使用散列函数来确定要遍历哪个列表。然后我们搜索相应的列表。执行插入时，我们检查相应的列表以查看元素是否已经存在（如果预期有重复项，通常会保留一个额外的数据成员，在匹配时该数据成员将递增）。如果元素确实在其中，它可以插入到列表的前面，因为这很方便，而且最近插入的元素在不久的将来最有可能被访问。

![](img/e449061a0cac9cafaefd979fab665b33_214_0.png)

图 5.5 分离链接散列表

```cpp
template <typename HashedObj>
class HashTable
{
  public:
    explicit HashTable( int size = 101 );

    bool contains( const HashedObj & x ) const;

    void makeEmpty( );
    bool insert( const HashedObj & x );
    bool insert( HashedObj && x );
    bool remove( const HashedObj & x );

  private:
    vector<list<HashedObj>> theLists;   // The array of Lists
    int currentSize;

    void rehash( );
    size_t myhash( const HashedObj & x ) const;
};
```

图 5.6 分离链接散列表的类型声明

分离链接实现的类接口如图 5.6 所示。散列表存储一个链表数组，这些链表在构造函数中分配。

类接口说明了一个语法点：在 C++11 之前，在 theLists 的声明中，两个 `>>` 之间需要一个空格；因为 `>>` 是一个 C++ 标记，并且它比 `>` 长，所以 `>>` 会被识别为该标记。在 C++11 中，不再是这种情况了。

正如二叉搜索树仅适用于可比较对象一样，本章中的散列表仅适用于提供散列函数和相等运算符（operator== 或 operator!=，或可能两者都有）的对象。

与要求散列函数同时接受对象和表大小作为参数不同，我们的散列函数仅将对象作为参数并返回适当的整型类型。实现此目的的标准机制使用函数对象，散列表的协议是在 C++11 中引入的。具体来说，在 C++11 中，散列函数可以由函数对象模板表示：

```cpp
template <typename Key>
class hash
{
  public:
    size_t operator()( const Key & k ) const;
};
```

该模板为 int 和 string 等标准类型提供了默认实现；因此，图 5.4 中描述的散列函数可以实现为

```cpp
template <>
class hash<string>
{
public:
    size_t operator()( const string & key )
    {
        size_t hashVal = 0;

        for( char ch : key )
            hashVal = 37 * hashVal + ch;

        return hashVal;
    }
};
```

类型 size_t 是表示对象大小的无符号整型类型；因此，它保证能够存储数组索引。实现散列表算法的类可以调用泛型散列函数对象来生成整型类型 size_t，然后将结果缩放为合适的数组索引。在我们的散列表中，这体现在私有成员函数 myhash 中，如图 5.7 所示。

```cpp
1      size_t myhash( const HashedObj & x ) const
2      {
3          static hash<HashedObj> hf;
4          return hf( x ) % theLists.size( );
5      }
```

图 5.7 散列表的 myhash 成员函数

图 5.8 说明了一个 Employee 类，该类可以存储在泛型散列表中，并使用 name 成员作为键。Employee 类通过提供相等运算符和散列函数对象来实现 HashedObj 要求。

```cpp
// Example of an Employee class
class Employee
{
  public:
    const string & getName( ) const
    {
        return name;
    }

    bool operator==( const Employee & rhs ) const
    {   return getName( ) == rhs.getName( );  }

    bool operator!=( const Employee & rhs ) const
    {   return !( *this == rhs ); }

  // Additional public members not shown

  private:
    string name;
    double salary;
    int seniority;

  // Additional private members not shown
};

template<>
class hash<Employee>
{
  public:
    size_t operator()( const Employee & item )
    {
        static hash<string> hf;
        return hf( item.getName( ) );
    }
};
```

图 5.8 可用作 HashedObj 的类示例

实现 makeEmpty、contains 和 remove 的代码如图 5.9 所示。接下来是插入例程。如果要插入的项已经存在，则什么都不做；否则，我们将其放入列表中（参见图 5.10）。元素可以放在列表中的任何位置；在我们的情况中，使用 push_back 最方便。whichList 是一个引用变量；有关此引用变量用法的讨论，请参见第 1.5.2 节。

除了链表之外，还可以使用任何方案来解决冲突：二叉搜索树甚至另一个散列表都可以工作，但我们预期如果表很大且散列函数良好，所有列表都应该很短，因此基本的分离链接不会尝试任何复杂的方法。

我们定义散列表的负载因子 $\lambda$ 为散列表中元素数量与表大小的比率。在上面的示例中，$\lambda = 1.0$。列表的平均长度是 $\lambda$。执行搜索所需的工作量是评估散列函数所需的常数时间加上遍历列表的时间。在不成功的搜索中，平均需要检查的节点数量是 \(\lambda\)。成功的搜索需要遍历大约 \(1 + (\lambda/2)\) 个链接。要理解这一点，请注意，正在搜索的列表包含存储匹配项的那个节点，加上零个或多个其他节点。在包含 \(N\) 个元素和 \(M\) 个列表的表中，“其他节点”的预期数量是 \((N-1)/M = \lambda - 1/M\)，这基本上是 \(\lambda\)，因为假设 \(M\) 很大。平均情况下，会搜索一半的“其他节点”，因此加上匹配节点，我们得到的平均搜索成本是 \(1 + \lambda/2\) 个节点。此分析表明，表大小并不重要，但负载因子很重要。分离链接散列的一般规则是使表大小大约等于预期的元素数量（换句话说，令 \(\lambda \approx 1\)）。在图 5.10 的代码中，如果负载因子超过 1，我们通过在第 10 行调用 `rehash` 来扩展表大小。`rehash` 在第 5.5 节中讨论。如前所述，保持表大小为质数也是一个好主意，以确保良好的分布。

