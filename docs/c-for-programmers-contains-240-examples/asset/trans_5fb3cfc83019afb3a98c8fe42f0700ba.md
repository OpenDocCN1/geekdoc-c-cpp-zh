

以高效的索引访问（使用下标运算符）读取和修改其元素，这一点与 vector 十分相似。deque 类还针对在其前端和后端进行高效插入和删除操作进行了实现，这一点与 list 十分相似（不过，list 还能够在列表中间高效地进行插入和删除）。deque 类支持随机访问迭代器，因此 deque 可以与所有 STL 算法一起使用。deque 最常见的用途之一是维护一个先进先出（FIFO）的元素队列。事实上，deque 是队列适配器的默认底层实现（第 20.4.2 节）。

deque 的额外存储空间可以在其任一端以多个内存块的形式分配，这些内存块通常维护为一个指向各内存块的指针数组。² 由于 deque 的内存布局不连续，deque 迭代器必须比用于遍历 vector 或基于指针的数组的指针更加智能。

## 性能提示 20.13

> 通常，deque 的开销高于 vector。

## 性能提示 20.14

> deque 中间的插入和删除操作经过优化，以尽量减少复制的元素数量，因此对于此类修改，它比 vector 更高效，但不如 list 高效。

deque 类提供了与 vector 类相同的基本操作，同时增加了成员函数 push_front 和 pop_front，分别用于在 deque 的开头插入和删除元素。

图 20.18 演示了 deque 类的特性。请记住，图 20.14、图 20.15 和图 20.17 中介绍的许多函数也可以用于 deque 类。要使用 deque 类，必须包含头文件 `<deque>`。

第 13 行实例化了一个可以存储 double 值的 deque。第 17～19 行使用函数 push_front 和 push_back 在 deque 的开头和末尾插入元素。请记住，所有序列容器都提供 push_back，但只有 list 类和 deque 类提供 push_front。

```
1  // Fig. 20.18: fig20_18.cpp
2  // Standard Library class deque test program.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
7  #include <deque> // deque class-template definition
8  #include <algorithm> // copy algorithm
9  #include <iterator> // ostream_iterator
10
int main()
{
13     std::deque< double > values; // create deque of doubles
```

图 20.18 | 标准库 deque 类模板。（第 1 部分，共 2 部分）

2. 这是特定于实现的细节，并非 C++ 标准的要求。

```
14  std::ostream_iterator< double > output( cout, " " );
15
16  // insert elements in values
17  values.push_front( 2.2 );
18  values.push_front( 3.5 );
19  values.push_back( 1.1 );
20
21  cout << "values contains: ";
22
23  // use subscript operator to obtain elements of values
24  for ( unsigned int i = 0; i < values.size(); i++ )
25      cout << values[ i ] << ' ';
26
27  values.pop_front(); // remove first element
28  cout << "\nAfter pop_front, values contains: ";
29  std::copy( values.begin(), values.end(), output );
30
31  // use subscript operator to modify element at location 1
32  values[ 1 ] = 5.4;
33  cout << "\nAfter values[ 1 ] = 5.4, values contains: ";
34  std::copy( values.begin(), values.end(), output );
35  cout << endl;
36  return 0;
37 } // end main
```

values contains: 3.5 2.2 1.1  
After pop_front, values contains: 2.2 1.1  
After values[ 1 ] = 5.4, values contains: 2.2 5.4

图 20.18 | 标准库 deque 类模板。（第 2 部分，共 2 部分）

第 24～25 行的 for 语句使用下标运算符获取 deque 中每个元素的值并输出。请注意，条件使用 size 函数，以确保不会尝试访问 deque 边界之外的元素。

第 27 行使用 pop_front 函数演示删除 deque 的第一个元素。请记住，只有 list 类和 deque 类提供 pop_front（vector 类不提供）。

第 32 行使用下标运算符创建一个左值。这使得我们可以直接为 deque 中的任意元素赋值。

## 20.3 关联容器

STL 的关联容器通过键（通常称为搜索键）提供对元素进行存储和检索的直接访问。四种关联容器是 multiset、set、multimap 和 map。每种关联容器都会使其键保持有序。遍历关联容器时，会按照该容器的排序顺序进行遍历。multiset 类和 set 类提供用于操作值集合的操作，其中值就是键——每个键并没有单独对应的值。multiset 与 set 之间的主要区别在于，multiset 允许重复键，而 set 不允许。multimap 类和 map 类提供用于操作与键关联的值的操作（这些值有时称为映射值）。multimap 与 map 之间的主要区别在于，multimap 允许存储带有关联值的重复键，而 map 只允许存储带有关联值的唯一键。除了图 20.2 中介绍的所有容器共有的成员函数外，所有关联容器还支持其他几个成员函数，包括 find、lower_bound、upper_bound 和 count。接下来的几个小节将介绍每种关联容器以及关联容器共有成员函数的示例。

### 20.3.1 multiset 关联容器

multiset 关联容器能够快速存储和检索键，并且允许重复键。元素的排序由比较器函数对象决定。例如，对于一个整数 multiset，可以使用比较器函数对象 less<int> 对键进行排序，使元素按升序排列。我们将在第 20.7 节详细讨论函数对象。所有关联容器中键的数据类型都必须能够根据指定的比较器函数对象正确地进行比较——使用 less<T> 排序的键必须支持使用运算符 < 进行比较。如果关联容器中使用的键属于用户定义的数据类型，则这些类型必须提供适当的比较运算符。multiset 支持双向迭代器（但不支持随机访问迭代器）。

图 20.19 演示了 multiset 关联容器，该容器存储按升序排列的整数 multiset。要使用 multiset 类，必须包含头文件 `<set>`。multiset 和 set 容器提供相同的基本功能。

第 10 行使用 typedef 为按升序排列的整数 multiset 创建了一个新的类型名称（别名），并使用函数对象 less<int>。升序是 multiset 的默认排序方式，因此第 10 行可以省略 std::less<int>。随后使用这个新类型（Ims）实例化一个整数 multiset 对象 intMultiset（第 19 行）。

## 良好的编程实践 20.1

> 使用 typedef，可以使包含较长类型名称（例如 multiset）的代码更易于阅读。

第 22 行的输出语句使用函数 count（所有关联容器都提供该函数）计算当前 multiset 中值 15 出现的次数。

```
1  // Fig. 20.19: fig20_19.cpp
2  // Testing Standard Library class multiset
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6  
7  #include <set> // multiset class-template definition
8  
9  // define short name for multiset type used in this program
10 typedef std::multiset< int, std::less< int > > Ims;
11 
12 #include <algorithm> // copy algorithm
13 #include <iterator> // ostream_iterator
14
```
```
int main()
{
    const int SIZE = 10;
    int a[ SIZE ] = { 7, 22, 9, 1, 18, 30, 100, 22, 85, 13 };
    Ims intMultiset; // Ims is typedef for "integer multiset"
    std::ostream_iterator< int > output( cout, " " );

    cout << "There are currently " << intMultiset.count( 15 )
         << " values of 15 in the multiset\n";

    intMultiset.insert( 15 ); // insert 15 in intMultiset
    intMultiset.insert( 15 ); // insert 15 in intMultiset
    cout << "After inserts, there are " << intMultiset.count( 15 )
         << " values of 15 in the multiset\n\n";

    // iterator that cannot be used to change element values
    Ims::const_iterator result;

    // find 15 in intMultiset; find returns iterator
    result = intMultiset.find( 15 );

    if ( result != intMultiset.end() ) // if iterator not at end
        cout << "Found value 15\n"; // found search value 15

    // find 20 in intMultiset; find returns iterator
    result = intMultiset.find( 20 );

    if ( result == intMultiset.end() ) // will be true hence
        cout << "Did not find value 20\n"; // did not find 20

    // insert elements of array a into intMultiset
    intMultiset.insert( a, a + SIZE );
    cout << "\nAfter insert, intMultiset contains:\n";
    std::copy( intMultiset.begin(), intMultiset.end(), output );

    // determine lower and upper bound of 22 in intMultiset
    cout << "\n\nLower bound of 22: "
         << *( intMultiset.lower_bound( 22 ) );
    cout << "\nUpper bound of 22: " << *( intMultiset.upper_bound( 22 ) );

    // p represents pair of const_iterators
    std::pair< Ims::const_iterator, Ims::const_iterator > p;

    // use equal_range to determine lower and upper bound
    // of 22 in intMultiset
    p = intMultiset.equal_range( 22 );

    cout << "\n\nequal_range of 22:" << "\n    Lower bound: "
         << *( p.first ) << "\n    Upper bound: " << *( p.second );
    cout << endl;
    return 0;
} // end main
```

