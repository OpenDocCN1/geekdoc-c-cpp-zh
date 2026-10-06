

# ISO/IEC 14882:2017(E)

表 90 — 关联容器要求（除容器之外）（续上）

| 表达式 | 返回类型 | 断言/注释前置/后置条件 | 复杂度 |
| --- | --- | --- | --- |
| a.merge(a2) | void | **前置条件：** `a.get_allocator() == a2.get_allocator()`。尝试提取 a2 中的每个元素并使用 a 的比较对象将其插入 a 中。对于带有键的容器，如果 a 中存在一个键与 a2 中某个元素的键等价的元素，则该元素将不会从 a2 中提取。**后置条件：** 指向 a2 转移元素的指针和引用将指向这些作为 a 成员的相同元素。指向已转移元素的迭代器将继续指向它们对应的元素，但它们现在的行为表现为指向 a 的迭代器，而不是指向 a2 的迭代器。**异常：** 除非比较操作符抛出异常。 | N log(N)，其中 N 的值为 a2.size()。 |
| a.erase(k) | size_type | 删除容器中所有键与 k 等价的元素；返回删除的元素数量。 | log(a.size()) + count(k) |
| a.erase(q) | iterator | 删除 q 指向的元素。返回一个指向被删除元素之前的 q 的迭代器。如果不存在此类元素，则返回 a.end()。 | 摊还常数级 |
| a.erase(r) | iterator | 删除 r 指向的元素。返回一个指向被删除元素之前的 r 的迭代器。如果不存在此类元素，则返回 a.end()。 | 摊还常数级 |

# ISO/IEC 14882:2017(E)

表 90 — 关联容器要求（除容器之外）（续上）

| 表达式 | 返回类型 | 断言/注释前/后置条件 | 复杂度 |
| --- | --- | --- | --- |
| a.erase(q1, q2) | iterator | 删除范围 [q1, q2) 内的元素。返回一个在任何元素被删除之前指向 q2 所向元素的迭代器。如果不存在此类元素，则返回 a.end()。 | log(a.size()) + N，其中 N 的值为 distance(q1, q2)。 |
| a.clear() | void | a.erase(a.begin(), a.end()) 返回 true。 | 与 a.size() 线性相关。 |
| b.find(k) | iterator const_ | 返回指向具有 k 的元素的迭代器，如果未找到该元素，则返回 b.end() | 对数级 |
| a_tran.find(ke) | iterator const_ | 返回指向具有键的元素的迭代器，满足 c(r, ke) && !c(ke, r)，如果未找到该元素，则返回 a_tran.end()。 | 对数级 |
| b.count(k) | size_type | 返回键为 k 的元素数量 | log(b.size()) |
| a_tran.count(ke) | size_type | 返回键为 r 且满足 c(r, ke) && !c(ke, r) 的元素数量 | log(a_tran.size()) + a_tran.count(ke) |
| b.lower_bound(k) | iterator const_ | 返回指向第一个键小于 k 的元素的迭代器，如果未找到此类元素，则返回 b.end()。 | 对数级 |
| a_tran.lower_bound(k1) | iterator const_ | 返回指向第一个键 r 满足 c(kl, r) 的元素的迭代器，如果未找到此类元素，则返回 a_tran.end()。 | 对数级 |
| b.upper_bound(k) | iterator const_ | 返回指向第一个键大于 k 的元素的迭代器，如果未找到此类元素，则返回 b.end()。 | 对数级 |
| a_tran.upper_bound(ku) | iterator const_ | 返回指向第一个键 r 满足 c(ku, r) 的元素的迭代器，如果未找到此类元素，则返回 a_tran.end()。 | 对数级 |

# ISO/IEC 14882:2017(E)

表 90 — 关联容器要求（除容器之外）（续上）

| 表达式 | 返回类型 | 断言/注释前置/后置条件 | 复杂度 |
| --- | --- | --- | --- |
| b.equal_=range(k) | pair<iterator, iterator>; pair<const_iterator, const_iterator> | 等同于 make_pair(b.lower_bound(k), b.upper_bound(k))。 | 对数级 |
| a_tran_.equal_=range(ke) | pair<iterator, iterator>; pair<const_iterator, const_iterator> 针对常量 a_tran_ | 等同于 make_pair(a_tran_.lower_bound(ke), a_tran_.upper_bound(ke))。 | 对数级 |

*insert* 和 *erase* 成员不会影响容器迭代器和引用的有效性，而 *erase* 成员会失效指向删除元素的迭代器。

**extract** 方法会导致指向移除元素的迭代器；指向移除元素的指针和引用仍然有效。然而，当元素由 nodetype 所有时，通过此类指针和引用访问元素是未定义的。通过 *node* 获取的引用和指针仅在元素成功插入时有效。

关联容器的基本属性是它们按键的非降序进行迭代，其中非降序是由构造它们时使用的比较操作符定义的。对于任何两个可解引用迭代器 i 和 j，如果 i 到 j 的距离为正，则存在关系：

```
value_comp(i, j) == false
```

对于具有唯一键的关联容器，存在更强的条件：

```
value_comp(i, j) != false
```

通过传递比较对象构造关联容器时，如果该对象是通过引用传递的，容器不存储该对象的指针或引用。当通过拷贝构造函数或赋值运算符拷贝关联容器时，目标容器应使用被拷贝容器的比较对象，就像传递给目标容器构造函数一样。

成员模板 *find*、`lower_bound*、`upper_bound*、*count*、*equal_range* 和 *emplace* 可以重载，以接受与容器键进行比较的值，而不是键本身。这使得在比较是透明的情况下，可以在不构造键的情况下进行搜索。

比较被认为是透明的，如果它满足了 `std::transparent` 的要求。这意味着它提供了可以接受不同类型参数的 `operator==`、`operator!=`、`<`、<=`>` 和 `>=`。如果比较是透明的，成员函数 *find*、`lower_bound*、`upper_bound*、*count* 和 *equal_range* 可以接受一个与容器键进行比较的值，而无需构造键对象。

