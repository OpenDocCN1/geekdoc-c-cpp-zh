
- `slist_init` 函数并不是严格必要的，因为用户可以很容易初始化它。
- `slist_cleanup` 函数在提供了 `free_fn` 的情况下，通过遍历列表来释放内存。

# 24.2 插入

需要编写的函数如列表 24.3 所示的“头部插入”和“尾部插入”。对于熟悉指针的人来说，这些操作是简单的。例如，我们可以侵入式地存储数据：

```c
void slist_push_front(struct slist *list, char const *data) {
    struct slink *node = malloc(sizeof(struct slink));
    if (!node) return;
    strcpy(node->data, data);
    node->next = list->head;
    list->head = node;
    if (list->tail == nullptr)
        list->tail = node;
}

void slist_push_back(struct slist *list, char const *data) {
    struct slink *node = malloc(sizeof(struct slink));
    if (!node) return;
    strcpy(node->data, data);
    node->next = nullptr;
    if (list->tail != nullptr) {
        list->tail->next = node;
    } else {
        list->head = node;
    }
    list->tail = node;
}
```

列表 24.3: 插入

- `slist_push_front` 在列表头部插入新节点。如果列表为空，则 `tail` 也指向该节点。
- `slist_push_back` 在列表尾部插入新节点。如果列表为空，则 `head` 也指向该节点。

需要编写的函数如列表 24.4 所示的“头部弹出”和“尾部弹出”。

```c
char* slist_pop_front(struct slist *list) {
    if (list->head == nullptr) return nullptr;
    struct slink *node = list->head;
    list->head = node->next;
    if (list->head == nullptr)
        list->tail = nullptr;
    return node->data;
}

char* slist_pop_back(struct slist *list) {
    if (list->tail == nullptr) return nullptr;
    struct slink *node = list->tail;
    if (list->head == list->tail) {
        list->head = list->tail = nullptr;
    } else {
        struct slink *curr = list->head;
        while (curr->next != list->tail)
            curr = curr->next;
        curr->next = nullptr;
        list->tail = curr;
    }
    return node->data;
}
```

列表 24.4: 弹出

- `slist_pop_front` 从头部弹出并返回数据。如果列表变空，则将 `tail` 设为空。
- `slist_pop_back` 从尾部弹出并返回数据。由于是单链表，这需要找到尾部的前一个节点。

# 24.5 遍历

需要编写的函数如列表 24.5 所示的“遍历列表”。

```c
void slist_traverse(struct slist *list, void (*func)(char const *)) {
    for (struct slink *curr = list->head; curr != nullptr; curr = curr->next) {
        func(curr->data);
    }
}
```

列表 24.5: 遍历

- `slist_traverse` 接收一个回调函数对列表中的每个元素执行操作。

# 24.6 查找

需要编写的函数如列表 24.6 所示的“查找元素”。

```c
char const* slist_find(struct slist *list, char const *name) {
    for (struct slink *curr = list->head; curr != nullptr; curr = curr->next) {
        if (strcmp(curr->data, name) == 0)
            return curr->data;
    }
    return nullptr;
}
```

列表 24.6: 查找

- `slist_find` 遍历列表并返回与 `name` 匹配的第一个元素；如果未找到则返回 `nullptr`。

```cpp
void slist_pop_front( struct slist *list ) {
    if ( list->head == nullptr)
        return;
    auto const new_head = list->head->next;
    free(list->head);
    list->head = new_head;
    if ( list->head == tail)
        list->tail = nullptr;
}
```

```cpp
void slist_pop_back(struct slist *list ) {
    if ( list->head == nullptr)
        return;
    auto new_tail = list->head;
    while ( new_tail->next != list->tail )
        new_tail = new_tail->next;
    free(list->tail);
    new_tail->next = nullptr;
    list->tail = new_tail;
}
```

# 列表 24.5: 单链表弹出函数

是时候实现一个双向链表了，即带有对应 next 指针的 dlink 的 dlist。但由于增加了一个 prev 指针，且大小还是 slist 的两倍，代价是巨大的。考虑到这一点，`slist_pop_back` 的实现应该使其在 O(n) 时间内运行。

当然，你可以同时实现 slist 和 dlist，并在大多数时候使用 slist，也许只是偶尔使用一次 slist_slist_pop_back。只有当你确实需要频繁使用 slist_pop_back 时，才使用 dlist。

## 24.5 从中间删除

偶尔，你可能需要从列表的中间删除一个节点（link）。看起来你可能无法通过单链表做到这一点，因为仅仅给出一个指向要删除的 link 的指针，你也无法获取前一个 slist 的 next，从而通过当前 link 的 next 来更新它。你所能做的是写一个类似于列表 24.6 所示的函数。

`slist_free` 函数执行了遍历列表的机械操作，跟踪并更新指针，但它将是否删除某个 link 的决策委托给一个谓词函数（predicate function），该函数接收一个 link 指针，仅在应该删除它时才返回 true。

- 为了方便起见，第 1–2 行声明了一个谓词函数的类型。除了 link 之外，它还接收一个 pred_data（这样命名是为了避免与 link 的数据混淆），它被传递给 slist_free_if，可能用于判断是否应该删除某个 link。

```cpp
typedef bool (*slist_pred_fn)(struct slist *link,
  void const *pred_data );
```

```cpp
size_t slist_free_if( struct slist *list,
  slist_pred_fn pred_fn,
  void const *pred_data ) {
```

```cpp
size_t free_count = 0;
  struct slink *pcurr = &list->head, *prev = NULL;
```

```cpp
for (;;) {
  auto const &curr = *pcurr;
  if (curr == nullptr)
    break;

  if (!pred_fn(curr, pred_data) ) {
    prev = curr;
    pcurr = &curr->next;
    continue;
  }

  if (curr == list->tail )
    list->tail = prev;
  *pcurr = &curr->next;
  free ( curr );
  ++free_count;
}

  return free_count;
}
```

# 列表 24.6: 单链表从中间删除函数

- 通常情况下，要删除的 link 是头部（head），这需要一个特殊处理；此函数通过使用指向第 8 行声明的当前 link pred 指针的指针（§6.6）体现了“良好的技巧”（good taste），消除了这种特殊情况。需要 prev 指针是因为 slist 有一个 tail 指针，且如果 tail 正好是要待删除的 link。
- 第 14 行调用谓词函数：如果它返回 false（不删除），则更新指针并继续迭代（第 15–17 行）；如果它返回 true，则要删除当前 link。
- 第 19–20 行处理更新 tail 的特殊情况。
- 第 21 行更新 *pcurr*（它可能是上一个 link 的 next，或者是 head）为当前 link 的 next 指针，从而有效地删除了当前 link。
- 为了提供信息，第 26 行返回被删除的 link 数量。

在字符串列表上配合 slist_free_if 使用的谓词函数示例，用于删除其数据（一个字符串）不包含 pred_data 给出的字符串的 link，如列表 24.7 所示。

> †The Mind Behind Linux, Linus Torvalds, TED Talk, Vancouver, BC, Feb. 2016; 21:20,
> https://www.ted.com/talks/linus_torvalds_the_mind_behind_linux

## 24.6 迭代

```cpp
bool slist_free_if_not_contains_str(struct slink *link,
    void const *pred_data) {
    return strstr(SLIST_DINT(link->data),
               pred_data) == nullptr;
}
```

# 列表 24.7: 单链表不包含字符串谓词函数

`strstr` 函数 (§B.2) 在字符串中搜索另一个字符串的出现情况。使用谓词函数删除字符串不包含 "error" 的 link 的示例（实际上是 grep(1)）如下：

```cpp
slist_free_if(list, slist_free_if_not_contains_str, "error");
```

## 25.1 哈希表

哈希表使用哈希函数 $h(k)$，该函数根据给定键 $k$ 的数据返回 $k$ 的哈希值，即一个固定大小的无符号整数，例如 64 位。技巧在于推导出一个“良好”的哈希函数，它需要满足：

- 速度快。
- 对于宽范围的数据或几乎相同的数据，返回在整个范围内均匀分布的整数。
- 冲突发生率低，即返回相同哈希值的不同 $k$ 值的数量很少。

如果你了解你的数据，就可以利用这些知识为它编写一个特定的哈希函数。包含如 ID、电子邮件地址或时间戳等唯一项的数据集更容易创建良好的哈希函数。但如果你不了解数据，那么你仍然需要使用一个满足这些标准的良好哈希函数。

一种满足这些标准并被常用的哈希函数是 25.1 所示的 "FNV-1a" 哈希函数。哈希值应初始化为 FNV1A_INIT。

```cpp
constexpr uint64_t FNV1A_INIT = 1649581039346650307UL;
constexpr uint64_t FNV1A_PRIME = 1099511628211UL;

uint64_t fnv1a_mem(uint64_t hash, const void *data, size_t n) {
  for (size_t i = 0; i < n; ++i) {
    hash ^= FNV1A_PRIME * ((uint8_t const*)data)[i]);
  }
  return hash;
}
```

# 列表 25.1：C 语言中的 FNV-1a 哈希函数

解释该函数以及它为什么好超出了本书的范围；它与 C 无关。网上有很多详细的解释。

一旦你得到了 $h(k)$，你就将其作为“桶”数组 $B$ 的索引，其中存储了 $k$ 及其关联的值 $v$。当然你不会直接使用 64 位整数作为索引；那将需要包含九百亿（$9 \times 10^{18}$）条目的数组；相反，你需要通过取模运算符 (§3.2) 对 $i$ 取模 $m$（数组的大小），以获得进入 $B$ 的实际索引 $i$，步骤如下：

> †The FNV 非加密哈希算法, Glenn Fowler, London Niall, and Kiem-Phong Vo, Comments to IEEE POSIX P103.2 Committee, Sep. 1991.
> ‡The FNV 非加密哈希算法, Glenn Fowler, London Niall, Kiem-Phong Vo, and Donald Eastlake, Engineering Task Force, Oct. 10, 2024.
> https://datatacker.ietf.org/doc/html/draft-eastlake-fnv-29

$k \rightarrow h(k) \ \& m \rightarrow i \rightarrow B[i] \rightarrow (k, v)$

为 $m$ 选择任何值都会增加冲突。当发生冲突时，你必须将 $k$ 与其他也哈希到 $B[i]$ 的键进行比较。因此，这是使用较大的 $m$（更多内存、更少冲突）与较小的 $m$（更少内存、更多冲突）之间的权衡。如果你知道 $n$（预期条目数，例如 2000），并且你可以接受这一点（例如由于冲突每个键最多有 3 次比较），那么 $m=[2000/3] = 667$。然而，$m$ 最好既是一个质数，又尽可能远离 2 的幂幂；因此，对于 2000 个条目来说，更好的 $m$ 值是 769。

- 同样地，如果 $m$ 不是质数且键集不是均匀分布的，解释为什么会这样：$h(k) \ \& m$ 会在 $m$ 的因数 $i$ 处产生更多冲突。如果 $m = 2^k$，则 $h(k)$ 的低 $k$ 位将被丢弃。

当插入一个键并发生冲突（$B[i]$ 不空）时，你会怎么做？通常有两种方法：

1. **开放法（Opening）**：有几种类型，包括线性探测，在线探测中你可以在 $B[i]+1, B[i]+2, ...$ 向前扫描，通常是在 $[i+1..m-1]$ 范围内的 $B[j]$ 中寻找条目 $B[j]$。当你找到时，将键和值放在那里。线性探测的优点包括：
   - 良好的缓存性能，因为条目直接在数组中并且在同一缓存行内 (§10.6)。
   线性探测的缺点包括：
   - 哈希表可能会由于填充 $B$ 的每个元素而满。
   - 删除条目涉及用特殊的“已删除”值标记它们（但随着删除条目的增加，性能会下降），或移动条目以替换被删除的。

2. **链法（Chaining）**：每个 $B[i]$ 都是一个包含所有冲突键及其值的**链表。链法的优点：
   - 哈希表永远不会满，因为新条目可以始终插入到链表中（但请参见第一个缺点）。
   - 删除条目只需更新几个指针。
   链法的缺点：尽管哈希表可能会满（从无法添加更多条目的意义上说），但随着链表长度的增加，性能从 $O(1)$ 退化到 $O(n)$。然而，你可以“扩容”，
   - 扩容哈表是非常耗时的。对于时间敏感的应用程序，你可能无法负担。（对于编译器可以。）
   - 缓存性能差，因为条目分散在内存中。
   - 由于 $B$ 中未使用的元素以及链表的额外空间导致空间浪费。

对于哈希表，有一个值被称为负载因子 $\alpha$，它定义为：

```
$\alpha = \frac{n}{m}$
```

即 $B$ 的填充百分比。随着 $n$ 的增加负载因子增大，哈希表的性能会下降，因为插入或查找条目的时间变长了。

## 25.2 类型

我们的哈希表类型如 25.2所示。
