

```cpp
cout << "Line 14: newVList: ";                         //Line 14
print(newVList);                                         //Line 15

    //inner_product function
sum = inner_product(vecList.begin(), vecList.end(),
                    newVList.begin(), 0);               //Line 16

cout << "Line 17: Inner product of vecList "
     << "and newVList: " << sum << endl;                //Line 17

sum = inner_product(vecList.begin(), vecList.end(),
                    newVList.begin(), 0,
                    plus<int>(), minus<int>());          //Line 18

cout << "Line 19: Inner product of vecList and "
     << "newVList, using - for *: "
     << sum << endl;                                     //Line 19

    //partial_sum function
partial_sum(vecList.begin(), vecList.end(),
            newVList.begin());                           //Line 20

cout << "Line 21: newVList with partial sum : ";        //Line 21
print(newVList);                                         //Line 22

    //partial_sum: the default + is replaced by *
partial_sum(vecList.begin(), vecList.end(),
            newVList.begin(), multiplies<int>());        //Line 23

cout << "Line 24: newVList with partial "
     << "multiplication: " << endl
     << " ";                                             //Line 24
print(newVList);                                         //Line 25

return 0;
}

void print(vector<int> vList)
{
    ostream_iterator<int> screenOut(cout, " ");         //Line 26
    copy(vList.begin(), vList.end(), screenOut);         //Line 27
    cout << endl;                                        //Line 28
}
```

## 示例运行：
```text
Line 4: vecList: 1 2 3 4 5 6 7 8
Line 7: Sum of the elements of vecList = 36
Line 9: Product of the elements of vecList = 40320
Line 11: newVList: 1 1 1 1 1 1 1 1
Line 14: newVList: 1 2 6 12 20 30 42 56
Line 17: Inner product of vecList and newVList: 1093
Line 19: Inner product of vecList and newVList, using - for *: -133
Line 21: newVList with partial sum: 1 3 6 10 15 21 28 36
Line 24: newVList with partial multiplication:
          1 2 6 24 120 720 5040 40320
```

前面的输出本身已说明清楚。具体细节留作练习。

## 快速回顾

- 1. STL 的三个主要组成部分是容器、迭代器和算法。
- 2. STL 容器是类模板。
- 3. 迭代器用于逐步访问容器中的元素。
- 4. 算法用于操作容器中的元素。
- 5. 容器的主要类别是序列容器、关联容器和容器适配器。
- 6. 三种预定义的序列容器是 vector、deque 和 list。
- 7. vector 容器在动态数组中存储和管理其对象。
- 8. 由于数组是随机访问数据结构，因此可以随机访问 vector 的元素。
- 9. 实现 vector 容器的类名是 vector。
- 10. vector 容器中的元素插入通过使用 insert 和 push_back 操作完成。
- 11. vector 容器中的元素删除通过使用 pop_back、erase 和 clear 操作完成。
- 12. 指向 vector 容器的迭代器使用 typedef iterator 声明，该 typedef 声明为 vector 类的公有成员。
- 13. 所有容器共有的成员函数是默认构造函数、带参构造函数、复制构造函数、析构函数、`empty`、`size`、`max_size`、`swap`、`begin`、`end`、`rbegin`、`rend`、`insert`、`erase`、`clear` 以及关系运算符函数。
- 14. 成员函数 begin 返回指向容器中第一个元素的迭代器。
- 15. 成员函数 end 返回指向容器中最后一个元素之后位置的迭代器。
- 16. 除上文第 13 项列出的成员函数外，所有序列容器共有的其他成员函数是 insert、push_back、pop_back、erase、clear 和 resize。
- 17. copy 算法用于将给定范围内的元素复制到另一个位置。
- 18. 使用 `ostream` 迭代器的 copy 函数也可用于输出容器的元素。
- 19. 当我们创建类型为 `ostream` 的迭代器时，还要指定该迭代器将输出的元素类型。
- 20. deque 容器实现为动态数组，使得元素可以在数组两端插入。
- 21. deque 可以向任一方向扩展。
- 22. 包含 `class deque` 定义的类名是 `deque`。
- 23. 除所有容器共有的操作外，可用于操作 `deque` 元素的其他操作是 `assign`、`push_front`、`pop_front`、`at`、数组下标运算符 `[]`、`front` 和 `back`。
- 24. list 容器实现为双向链表。因此，列表中的每个元素都指向其直接前驱和直接后继（第一个和最后一个元素除外）。
- 25. 包含 `class list` 定义的类名是 `list`。
- 26. 除序列容器共有的操作外，可用于操作 list 容器中元素的其他操作是 `assign`、`push_front`、`pop_front`、`front`、`back`、`remove`、`remove_if`、`unique`、`splice`、`sort`、`merge` 和 `reverse`。
- 27. 迭代器的五个类别是输入迭代器、输出迭代器、前向迭代器、双向迭代器和随机访问迭代器。
- 28. 输入迭代器用于从输入流输入数据。
- 29. 输出迭代器用于向输出流输出数据。
- 30. 前向迭代器可以引用同一集合中的同一元素，并多次处理同一元素。
- 31. 双向迭代器是前向迭代器，也可以反向遍历元素。
- 32. 双向迭代器可用于 `list`、`set`、`multiset`、`multimap`、`map` 和 `multimap` 类型的容器。
- 33. 随机访问迭代器是双向迭代器，可以随机处理容器中的元素。
- 34. 随机访问迭代器可用于 `vector`、`deque` 和 `string` 类型的容器，以及数组。
- 58. STL 提供了三种迭代器——`back_inserter`、`front_inserter` 和 `inserter`——称为插入迭代器，用于在目标位置插入元素。
- 59. `back_inserter` 使用容器的 `push_back` 操作代替赋值运算符。
- 60. `front_inserter` 使用容器的 `push_front` 操作代替赋值运算符。
- 61. 由于 vector 类不支持 `push_front` 操作，因此该迭代器不能用于 vector 容器。
- 62. `inserter` 迭代器使用容器的 `insert` 操作代替赋值运算符。
- 63. 函数 `fill` 用于填充容器中的元素，函数 `fill_n` 用于填充接下来的 n 个元素。
- 64. 函数 `generate` 和 `generate_n` 用于生成元素并填充序列。
- 65. 函数 `find`、`find_if`、`find_end` 和 `find_first_of` 用于查找给定范围内的元素。
- 66. 函数 `remove` 用于从序列中移除某些元素。
- 67. 函数 `remove_if` 用于根据指定条件从序列中移除元素。
- 68. 函数 `remove_copy` 通过从第一个序列中排除某些元素，将序列中的元素复制到另一个序列。
- 69. 函数 `remove_copy_if` 通过使用指定条件从第一个序列中排除某些元素，将序列中的元素复制到另一个序列。
- 70. 函数 `swap`、`iter_swap` 和 `swap_ranges` 用于交换元素。
- 71. 函数 `search`、`search_n`、`sort` 和 `binary_search` 用于搜索元素。
- 72. 函数 `adjacent_find` 用于查找满足某个条件的连续元素的首次出现。
- 73. 算法 `merge` 合并两个已排序列表。
- 74. 算法 `inplace_merge` 用于合并两个已排序的连续序列。
- 75. 算法 `reverse` 反转给定范围内元素的顺序。
- 76. 算法 `reverse_copy` 在复制到目标范围时反转给定范围内的元素。源不被修改。
- 77. 算法 `rotate` 旋转给定范围内的元素。
- 78. 算法 `rotate_copy` 按旋转后的顺序将源元素复制到目标位置。
- 79. 算法 `count` 统计给定值在给定范围内出现的次数。

![](img/f97f778697507bb6fdd80c5991210cba_1512_0.png)

