

## 常见编程错误 20.3

> 向量不能为空；否则，front 和 back 函数的结果未定义。

第 26–27 行展示了通过向量进行下标访问的两种方式（这也可以用于 deque 容器）。第 26 行使用重载的下标运算符，该运算符根据容器是否为常量，返回指定位置的值的引用或该值的常量引用。函数 at（第 27 行）执行相同的操作，但带有边界检查。函数 at 首先检查作为参数提供的值，并确定它是否在向量的边界内。如果不是，函数 at 会抛出在头文件 <stdexcept> 中定义的 out_of_bounds 异常（如第 36–43 行所示）。图 20.16 显示了一些 STL 异常类型。 （标准库异常类型在第 16 章 异常处理 中讨论。）

第 30 行使用了每个序列容器提供的 *insert* 函数的三个重载之一。第 30 行在第一个参数中指定的迭代器位置的元素之前插入值 22。在此示例中，迭代器指向向量的第二个元素，因此 22 被插入为第二个元素，原来的第二个元素变为向量的第三个元素。insert 的其他版本允许在容器的特定位置开始插入同一值的多个副本，或从另一个容器（或数组）插入一系列值，从原始容器中的特定位置开始。

第 46 行和第 51 行使用了所有一流容器都可用的两个 *erase* 函数。第 46 行表示应从容器中删除迭代器参数指定的位置处的元素（在此示例中，为向量开头的元素）。第 51 行指定应从容器中删除从第一个参数的位置开始到第二个参数的位置为止（不包括）的范围内的所有元素。在此示例中，向量的所有元素都被删除。第 53 行使用函数 *empty*（适用于所有容器和适配器）确认向量为空。

## 常见编程错误 20.4

> 删除包含指向动态分配对象的指针的元素不会删除该对象；这可能导致内存泄漏。

第 56 行演示了使用第二个和第三个参数指定值序列中起始位置和结束位置的 *insert* 函数的版本（pos-

| STL 异常类型 | 描述 |
|---|---|
| `out_of_range` | 表示下标超出范围——例如，当向 vector 成员函数 `at` 指定无效下标时。 |
| `invalid_argument` | 表示向函数传递了无效参数。 |
| `length_error` | 表示尝试创建过长的容器、字符串等。 |
| `bad_alloc` | 表示使用 `new`（或使用分配器）尝试分配内存失败，因为没有足够的内存可用。 |

**图 20.16** | 一些 STL 异常类型。

```
19  std::list< int > otherValues; // create list of ints
20
21  // insert items in values
22  values.push_front( 1 );
23  values.push_front( 2 );
24  values.push_back( 4 );
25  values.push_back( 3 );
26
27  cout << "values contains: ";
28  printList( values );
29
30  values.sort(); // sort values
31  cout << "\nvalues after sorting contains: ";
32  printList( values );
33
34  // insert elements of array into otherValues
35  otherValues.insert( otherValues.begin(), array, array + SIZE );
36  cout << "\nAfter insert, otherValues contains: ";
37  printList( otherValues );
38
39  // remove otherValues elements and insert at end of values
40  values.splice( values.end(), otherValues );
41  cout << "\nAfter splice, values contains: ";
42  printList( values );
43
44  values.sort(); // sort values
45  cout << "\nAfter sort, values contains: ";
46  printList( values );
47
48  // insert elements of array into otherValues
49  otherValues.insert( otherValues.begin(), array, array + SIZE );
50  otherValues.sort();
51  cout << "\nAfter insert and sort, otherValues contains: ";
52  printList( otherValues );
53
54  // remove otherValues elements and insert into values in sorted order
55  values.merge( otherValues );
56  cout << "\nAfter merge:\n   values contains: ";
57  printList( values );
58  cout << "\n   otherValues contains: ";
59  printList( otherValues );
60
61  values.pop_front(); // remove element from front
62  values.pop_back(); // remove element from back
63  cout << "\nAfter pop_front and pop_back:\n   values contains: "
64  printList( values );
65
66  values.unique(); // remove duplicate elements
67  cout << "\nAfter unique, values contains: ";
68  printList( values );
69
70  // swap elements of values and otherValues
71  values.swap( otherValues );
```

```
72  cout << "\nAfter swap:\n   values contains: ";
73  printList( values );
74  cout << "\n   otherValues contains: ";
75  printList( otherValues );
76
77  // replace contents of values with elements of otherValues
78  values.assign( otherValues.begin(), otherValues.end() );
79  cout << "\nAfter assign, values contains: ";
80  printList( values );
81
82  // remove otherValues elements and insert into values in sorted order
83  values.merge( otherValues );
84  cout << "\nAfter merge, values contains: ";
85  printList( values );
86
87  values.remove( 4 ); // remove all 4s
88  cout << "\nAfter remove( 4 ), values contains: ";
89  printList( values );
90  cout << endl;
91  return 0;
92  } // end main
93
94  // printList function template definition; uses
95  // ostream_iterator and copy algorithm to output list elements
96  template < typename T > void printList( const std::list< T > &listRef )
97  {
98      if ( listRef.empty() ) // list is empty
99          cout << "List is empty";
100     else
101     {
102         std::ostream_iterator< T > output( cout, " " );
103         std::copy( listRef.begin(), listRef.end(), output );
104     } // end else
105  } // end function printList
```

values contains: 2 1 4 3
values after sorting contains: 1 2 3 4
After insert, otherValues contains: 2 6 4 8
After splice, values contains: 1 2 3 4 2 6 4 8
After sort, values contains: 1 2 2 3 4 4 6 8
After insert and sort, otherValues contains: 2 4 6 8
After merge:
  values contains: 1 2 2 2 3 4 4 4 6 6 8 8
  otherValues contains: List is empty
After pop_front and pop_back:
  values contains: 2 2 2 3 4 4 4 6 6 8
After unique, values contains: 2 3 4 6 8
After swap:
  values contains: List is empty
  otherValues contains: 2 3 4 6 8
After assign, values contains: 2 3 4 6 8
After merge, values contains: 2 2 3 3 4 4 6 6 8 8
After remove( 4 ), values contains: 2 2 3 3 6 6 8 8

第 18–19 行实例化了两个能够存储整数的 list 对象。第 22–23 行使用函数 push_front 在 values 的开头插入整数。函数 push_front 特定于类 list 和 deque（不适用于 vector）。第 24–25 行使用函数 push_back 在 values 的末尾插入整数。请记住，函数 push_back 是所有序列容器共有的。

第 30 行使用 list 成员函数 sort 以升序排列列表中的元素。 [注意：这与 STL 算法中的 sort 不同。] 函数 sort 的第二个版本允许您提供一个二元谓词函数，该函数接受两个参数（列表中的值），执行比较并返回指示结果的 bool 值。此函数决定列表中元素的排序顺序。此版本对于存储指针而非值的列表可能特别有用。 [注意：我们在图 20.28 中演示了一个一元谓词函数。一元谓词函数接受单个参数，使用该参数执行比较并返回指示结果的 bool 值。]

第 40 行使用 list 函数 splice 从 otherValues 中删除元素并将它们插入到 values 中，在第一个参数指定的迭代器位置之前。有另外两个版本的此函数。带三个参数的 splice 函数允许从第二个参数指定的容器中从第三个参数的迭代器指定的位置删除一个元素。带四个参数的 splice 函数使用最后两个参数指定应从第二个参数的容器中删除并放置在第一个参数指定的位置的范围。

在向 otherValues 插入更多元素并对 values 和 otherValues 进行排序后，第 55 行使用 list 成员函数 merge 删除 otherValues 的所有元素并以排序顺序将它们插入到 values 中。在执行此操作之前，两个列表必须以相同的顺序排序。merge 的第二个版本允许您提供一个谓词函数，该函数接受两个参数（列表中的值）并返回 bool 值。谓词函数指定 merge 使用的排序顺序。

第 61 行使用 list 函数 pop_front 删除列表中的第一个元素。第 62 行使用函数 pop_back（适用于所有序列容器）删除列表中的最后一个元素。

第 66 行使用 list 函数 unique 删除列表中的重复元素。在执行此操作之前，列表应按排序顺序排列（以便所有重复项并排），以保证消除所有重复项。unique 的第二个版本允许您提供一个谓词函数，该函数接受两个参数（列表中的值）并返回 bool 值，指定两个元素是否相等。

第 71 行使用函数 swap（适用于所有容器）交换 values 的内容与 otherValues 的内容。
第 78 行使用 list 函数 assign 用两个迭代器参数指定的范围内的 otherValues 的内容替换 values 的内容。assign 的第二个版本用第二个参数指定的值副本替换原始内容。函数的第一个参数指定副本的数量。第 87 行使用 list 函数 remove 从列表中删除所有值 4 的副本。

## 20.2.3 deque 序列容器

类 deque 提供了向量和列表在一个容器中的许多好处。术语 deque 是“双端队列”的缩写。类 deque 被实现为提供 ef-

