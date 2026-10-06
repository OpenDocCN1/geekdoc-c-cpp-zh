

# ISO/IEC 14882:2017(E)

当序列中间频繁发生插入和删除时，应使用该方法。当插入和删除发生在序列的开头或结尾时，deque 是首选的数据结构。

表 87 — 序列容器要求（除 container 之外）

| 表达式 | 返回类型 | 断言/后置条件 |
|---|---|---|
| X(n, t); U(n, t); | | 要求：T 必须可拷贝到 X 中。后置条件：distance(begin(), end()) == n 构造一个包含 n 个 t 拷贝的序列容器 |
| X(i, j); U(i, j); | | 要求：T 必须可构造插入到 X 的 *i 位置。对于 vector，迭代器不会移动且满足向前迭代器要求 (27.2.5)，T 必须可移动插入到 X 中。范围 [i, j) 中的每个迭代器应恰好被解引用一次。后置条件：distance(begin(), end()) == distance(i, j) 构造一个等于范围 [i, j) 的序列容器 |
| X(il) a = il | X | 等于 X(il.begin(), il.end()) 要求：T 可拷贝到 X 且可赋值给 X。将范围 [il.begin(), il.end()) 赋值给 a。所有元素要么被赋值要么被销毁。返回：*this |
| a.emplace(p, args) | iterator | 要求：T 可从 args 构造并插入 X 中。T 也是可移动插入到 X 并可赋值的。对于 vector 和 deque，T 满足 影响：在 p 之前插入一个用 std::forward<Args>(args)... 构造的类型 T 对象。 |

# ISO/IEC 14882:2017(E)

表 87 — 序列容器要求（除 container 之外）（续）

| 表达式 | 返回类型 | 断言/注前置/后置条件 |
|---|---|---|
| a.insert(p,t) | iterator | 要求：T 必须可拷贝插入到 X。对于 vector 和 deque，T 也必须可赋值。影响：在 p 之前插入一个 T 的拷贝。 |
| a.insert(p,rv) | iterator | 要求：T 必须可移动到 X。对于 vector 和 deque，T 也必须可赋值。影响：在 p 之前插入一个 rv 的拷贝。 |
| a.insert(p,n,t) | iterator | 要求：T 必须可拷贝插入到 X 且可赋值。在 p 之前插入 n 个 T 的拷贝。 |
| a.insert(p,i,j) | iterator | 要求：T 可从 #1 构造并插入 X 中。对于 vector 和 deque，T 也必须可移动构造、可赋值且可交换 (20.5.3.2)。范围 [i, j] 中的每个迭代器应恰好被解引用一次。要求：i 和 j 不是指向 a 的迭代器。在 p 之前插入 [i, j] 中元素的拷贝。a.insert(p, il.begin(), il.end()). |
| a.erase(q) | iterator | 要求：对于 vector 和 deque，T 必须可赋值。影响：删除 q 指向的元素。 |
| a.erase(q1,q2) | iterator | 要求：对于 vector 和 deque，T 必须可赋值。影响：删除范围 [q1, q2] 中的元素。 |
| a.clear() | void | 销毁 a 中的所有元素。使所有引用 a 元素的引用、指针和迭代器失效，并可能使末尾迭代器失效。后置条件：a.empty() 返回 true。复杂度：线性。 |

# 表 87 — 序列容器要求（除 container 之外）（续）

| 表达式 | 返回类型 | 断言/注前置/后置条件 |
|---|---|---|
| a.assign(i,j) | void | 要求：T 必须从 X 构造且可从 T 赋值。对于 vector，如果迭代器不满足向前迭代器要求 (27.2.5)，T 也必须可移动插入到 X 中。范围 [i, j) 中的每个迭代器应恰好被解引用一次。要求：i, j 不是指向 a 的迭代器。用 [i, j) 的拷贝替换 a 中的元素。使所有引用 a 元素的引用、指针和迭代器失效。对于 vector 和 deque，还使末尾迭代器失效。 |
| a.assign(il) | void | a.assign(begin(), il.end()). 要求：T 必须可拷贝插入到 X 且可赋值。t 不是指向 a 的引用。用 n 个 t 的拷贝替换 a 中的元素。使所有引用 a 元素的引用、指针和迭代器失效。对于 vector 和 deque，还使末尾迭代器失效。 |
| a.assign(n,t) | void | |

- 5 a.insert(p, t) 返回的迭代器指向插入到 a 中的 t 拷贝。
- 6 a.insert(p, rv) 返回的迭代器指向插入到 a 中的 rv 拷贝。
- 7 a.insert(p, n, t) 返回的迭代器指向插入到 a 中的第一个元素的拷贝，或者在 n = 0 时指向 p。
- 8 a.insert(p, i, j) 返回的迭代器指向插入到 a 中的第一个元素的拷贝，或者在 i = j 时指向 p。
- 9 a.insert(p, il) 返回的迭代器指向插入到 a 中的第一个元素的拷贝，或者在 il 为空时指向 p。
- 10 a.emplace(p, args) 返回的迭代器指向从 args 构造到 a 中的新元素。
- 11 a.erase(q) 返回的迭代器指向插入到 a 中的 t 拷贝。
- 12 a.erase(q1,q2) 返回的迭代器指向被删除元素之后的元素。 |
