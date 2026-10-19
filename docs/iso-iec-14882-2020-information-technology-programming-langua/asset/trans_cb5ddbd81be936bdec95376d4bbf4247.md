

## 表 76：分配器感知容器要求（续）

| 表达式 | 返回类型 | 断言/说明 前置/后置条件 | 复杂度 |
|---|---|---|---|
| a = t | X& | 前置条件：T 可 Cpp17CopyInsertable 到 X 且 Cpp17CopyAssignable。后置条件：a == t | 线性 |
| a = rv | X& | 前置条件：如果 allocator_traits<allocator_type>::propagate_on_container_move_assignment::value 为 false，则 T 可 Cpp17MoveInsertable 到 X 且 Cpp17MoveAssignable。效果：a 的所有现有元素要么被移动赋值，要么被销毁。后置条件：a 等于赋值前 rv 的值。 | 线性 |
| a.swap(b) | void | 效果：交换 a 和 b 的内容 | 常数 |

18 某些容器成员函数和推导指引的行为取决于类型是否符合输入迭代器或分配器要求。实现确定一种类型不能作为输入迭代器所采用的程度是未指定的，除最低要求外，积分类型不得符合输入迭代器要求。同样，实现确定一种类型不能作为分配器所采用的程度是未指定的，除最低要求外，类型 A 只有在同时满足以下两个条件时才可作为分配器：

- (18.1) — 限定标识 A::value_type 有效且表示一个类型 (13.10.3)。
- (18.2) — 表达式 declval<A&>().allocate(size_t{}) 在作为未求值操作数处理时是良构的。

## 22.2.2 容器数据竞争 [container.requirements.dataraces]

1 为避免数据竞争 (16.4.6.10) 的目的，实现应将以下函数视为 const：begin、end、rbegin、rend、front、back、data、find、lower_bound、upper_bound、equal_range、at 以及在关联或无序关联容器中除外，operator []。

2 不考虑 16.4.6.10，实现必须避免在同一容器的不同元素中包含对象的不同元素被并发修改时发生数据竞争，除 vector<bool> 外。

3 [注 1：对于大小大于一的 vector<int> x，x[1] = 5 和 *x.begin() = 10 可以并发执行而不会发生数据竞争，但 x[0] = 5 和 *x.begin() = 10 并发执行可能导致数据竞争。作为一般规则的例外，对于 vector<bool> y，y[0] = true 可能与 y[1] = true 竞争。— 结束注]

## 22.2.3 序列容器 [sequence.reqmts]

1 序列容器将一组有限的同类型对象组织成严格的线性排列。库提供了四种基本的序列容器种类：vector、forward_list、list 和 deque。此外，array 作为序列容器提供，其序列操作有限，因为它具有固定的元素数量。库还提供了容器适配器，便于从基本序列容器种类（或用户定义的其它序列容器种类）构造抽象数据类型，如栈或队列。

2 [注 1：序列容器为程序员提供不同的复杂度权衡。vector 在大多数情况下是合适的。array 在翻译期间具有已知的固定大小。list 或 forward_list 支持从序列中间频繁插入和删除。deque 支持在序列开头或结尾进行高效的插入和删除。选择容器时，请记住 vector 最佳；如果选择其余，请添加注释说明原因！— 结束注]

# ISO/IEC 14882:2020(E)

3 在表 77 和表 78 中，X 表示序列容器类，a 表示包含类型为 T 的元素的类型为 X 的值，u 表示正在声明的变量的名称，A 表示如果限定标识 X::allocator_type 有效且表示一个类型 (13.10.3) 则为 X::allocator_type，否则为 allocator<T>，i 和 j 表示满足 Cpp17InputIterator 要求并引用可隐式转换为 value_type 的元素的迭代器，[i, j) 表示有效范围，il 指定类型为 initializer_list<value_type> 的对象，n 表示类型为 X::size_type 的值，p 表示指向 a 的有效常量迭代器，q 表示指向 a 的有效可解引用常量迭代器，[q1, q2) 表示 a 中有效常量迭代器的有效范围，t 表示 X::value_type 的左值或 const 右值，rv 表示 X::value_type 的非 const 右值。Args 表示模板参数包；args 表示模式为 Args&& 的函数参数包。

4 表达式的复杂度取决于序列。

## 表 77：序列容器要求（除容器外） [tab:container.seq.req]

| 表达式 | 返回类型 | 断言/说明 前置/后置条件 |
|---|---|---|
| X(n, t) X u(n, t); |  | 前置条件：T 可 Cpp17CopyInsertable 到 X。后置条件：distance(begin(), end()) == n 效果：构造一个包含 n 个 t 的副本的序列容器 |
| X(i, j) X u(i, j); |  | 前置条件：T 可从 *i Cpp17EmplaceConstructible 到 X。对于 vector，如果迭代器不满足 Cpp17ForwardIterator 要求 (23.3.5.5)，T 也可 Cpp17MoveInsertable 到 X。后置条件：distance(begin(), end()) == distance(i, j) 效果：构造等于范围 [i, j) 的序列容器。范围 [i, j) 中的每个迭代器恰好被解引用一次。 |
| X(il) |  | 等价于 X(il.begin(), il.end()) |
| a = il | X& | 前置条件：T 可 Cpp17CopyInsertable 到 X 且 Cpp17CopyAssignable。效果：将范围 [il.begin(), il.end()) 赋给 a。a 的所有现有元素要么被赋值，要么被销毁。返回：*this。 |
| a.emplace(p, args) | iterator | 前置条件：T 可从 args Cpp17EmplaceConstructible 到 X。对于 vector 和 deque，T 也可 Cpp17MoveInsertable 到 X 且 Cpp17MoveAssignable。效果：在 p 之前插入使用 std::forward<Args>(args)... 构造的类型为 T 的对象。[注 2：args 可以直接或间接引用 a 中的值。— 结束注] |
| a.insert(p,t) | iterator | 前置条件：T 可 Cpp17CopyInsertable 到 X。对于 vector 和 deque，T 也可 Cpp17CopyAssignable。效果：在 p 之前插入 t 的副本。 |
| a.insert(p,rv) | iterator | 前置条件：T 可 Cpp17MoveInsertable 到 X。对于 vector 和 deque，T 也可 Cpp17MoveAssignable。效果：在 p 之前插入 rv 的副本。 |

# ISO/IEC 14882:2020(E)

表 77：序列容器要求（除容器外）（续）

| 表达式 | 返回类型 | 断言/说明 前置/后置条件 |
|---|---|---|
| a.insert(p,n,t) | iterator | *前置条件：* T 可 Cpp17CopyInsertable 到 X 且 Cpp17CopyAssignable。*效果：* 在 p 之前插入 n 个 t 的副本。 |
| a.insert(p,i,j) | iterator | *前置条件：* T 可从 *i Cpp17EmplaceConstructible 到 X。对于 vector 和 deque，T 也可 Cpp17MoveInsertable 到 X、Cpp17MoveConstructible、Cpp17MoveAssignable 且可交换 (16.4.4.3)。i 和 j 都不是指向 a 的迭代器。*效果：* 在 p 之前插入 [i, j) 中元素的副本。范围 [i, j) 中的每个迭代器应恰好被解引用一次。 |
| a.insert(p, il) | iterator | a.insert(p, il.begin(), il.end())。 |
| a.erase(q) | iterator | *前置条件：* 对于 vector 和 deque，T 可 Cpp17MoveAssignable。*效果：* 删除 q 指向的元素。 |
| a.erase(q1,q2) | iterator | *前置条件：* 对于 vector 和 deque，T 可 Cpp17MoveAssignable。*效果：* 删除范围 [q1, q2) 中的元素。 |
| a.clear() | void | *效果：* 销毁 a 中的所有元素。使引用、指向 a 元素的指针和迭代器失效，并可能使末尾迭代器失效。*后置条件：* a.empty() 为 true。*复杂度：* 线性。 |
| a.assign(i,j) | void | *前置条件：* T 可从 *i Cpp17EmplaceConstructible 到 X 且可从 *i 赋值。对于 vector，如果迭代器不满足前向迭代器要求 (23.3.5.5)，T 也可 Cpp17MoveInsertable 到 X。i 和 j 都不是指向 a 的迭代器。*效果：* 用 [i, j) 的副本替换 a 中的元素。使引用、指向 a 元素的指针和迭代器失效。对于 vector 和 deque，也使末尾迭代器失效。范围 [i, j) 中的每个迭代器应恰好被解引用一次。 |
| a.assign(il) | void | a.assign(il.begin(), il.end())。 |
| a.assign(n,t) | void | *前置条件：* T 可 Cpp17CopyInsertable 到 X 且 Cpp17CopyAssignable。t 不是指向 a 的引用。*效果：* 用 n 个 t 的副本替换 a 中的元素。使引用、指向 a 元素的指针和迭代器失效。对于 vector 和 deque，也使末尾迭代器失效。 |

5 从 a.insert(p, t) 返回的迭代器指向插入到 a 中的 t 的副本。

6 从 a.insert(p, rv) 返回的迭代器指向插入到 a 中的 rv 的副本。

