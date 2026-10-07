
```cpp
typedef int (*ht_cmp_fn)(const void*, const void*);
typedef uint64_t (*ht_hash_fn)(const void*);
typedef void (*ht_free_fn)(void*);

struct ht_entry {
  uint64_t hash;
  struct ht_entry *next;
  struct ht_entry *prev;
  alignas(size_t) char data[];
};

struct hash_table {
  ht_entry **buckets;
  ht_cmp_fn cmp_fn;
  ht_hash_fn hash_fn;
  ht_free_fn free_fn;
  double max_lf;
  unsigned size;
  unsigned prime_idx;
};
```

# 列表 25.2：哈希表类型

```cpp
struct key_val {
  char const *key;
  void *val;
};

ht_hash_val hash_key_val(const void *data) {
  struct key_val const *kv = data;
  return fnv1a_mem(FNV1A_INIT, kv->key, strlen(kv->key));
}
```

```cpp
static constexpr unsigned HT_PRIME[] = {
53, 97, 193, 389, 769,
1543, 3079, 6151, 12289, 24593,
49157, 98317, 196613, 393241, 786433,
1572869, 3143759, 6291469, 12582917, 25165843
};
```

**列表 25.3:** 用于桶数量的非 2 幂的素数

## 25.3 初始化与清理

第一个写的函数是初始化，如列表 25.4 所示。

```cpp
void ht_init(struct hash_table *ht, double max_lf,
unsigned est_size, ht_cmp_fn cmp_fn,
ht_hash_fn hash_fn ) {
  unsigned prime_idx = 0;
  for ( ; prime_idx < ARRAY_SIZE(HT_PRIME); ++prime_idx ) {
    if ( HT_PRIME[prime_idx ] * max_lf >= est_size )
      break;
  }
  *ht = (struct hash_table){
    .buckets = calloc(HT_PRIME[prime_idx ],
      sizeof(struct ht_entry )),
    .cmp_fn = cmp_fn,
    .hash_fn = hash_fn,
    .max_lf = max_lf,
    .prime_idx = prime_idx
  };
}
```

**列表 25.4:** 哈希表初始化函数

- 第 1-3 行声明了函数签名，其中我们允许用户指定 `α_max` 和估计的元素数量，用以确定初始桶的数量。
- 第 5-8 行遍历 `HT_PRIME`，寻找第一个乘以 `α_max ≥ est_size` 的素数，作为初始桶的数量。
- 第 10 行使用了标准的 `calloc` 函数，它与 `malloc` 类似，但你需要指定要分配的对象数量和每个对象的大小；`calloc` 还会将内存初始化为零或等同于我们这里需要的值，以便所有指针都是 `nullptr`。

下一个写的函数是清理，如列表 25.5 所示，逻辑非常直观。

```cpp
void ht_cleanup(struct hash_table *ht,
      ht_free_fn free_fn ) {
  if ( ht == nullptr)
    return;
  for ( unsigned b = 0; b < HT_PRIME[ht->prime_idx]; ++b) {
    for (struct ht_entry *entry = ht->buckets[b].next,
        *next;
        entry != nullptr; entry = next ) {
      if (free_fn != nullptr)
        free_fn(entry->data);
      next = entry->next;
      free (entry);
    }
  }
  free (ht->buckets);
  *ht = (struct hash_table){ };
}
```

**列表 25.5:** 哈希表清理函数

## 25.4 插入

当向哈希表插入键时，你可能会发现已经存在具有相同键的条目。在这种情况下，你应该返回该条目的指针，而不是创建一个新的。但现在你需要区分返回新条目还是现有条目，因此定义了如列表 25.6 所示的“插入返回值”结构体 `ht_insert_rv`。`ht_insert` 函数本身如列表 25.7 所示。

```cpp
struct ht_insert_rv {
  struct ht_entry *entry; // 找到或插入的条目
  bool inserted;
}
```

**列表 25.6:** 哈希表插入返回值结构体

- 第 4–7 行计算哈希值、`n_buckets`（桶的数量，$m$）、`b`（桶的索引），并设置 `head` 指向桶链表的第一个条目。
- 第 9–14 行遍历链表寻找与 `key` 匹配的现有键：如果找到，则返回带有该条目的 `ht_insert_rv`。
- 否则，第 16 行为新条目分配内存，包括 `data_size`。
- 第 17–21 行初始化条目并更新桶以指向它。
- 第 23–25 行计算负载因子 `α`：如果它 `≥ max_lf`，则调用 `ht_grow` 通过增加 $m$ 并重新哈希所有条目来“增长”哈希表，如列表 25.8 所示。
- 第 27 行返回一个指向新条目的 `ht_insert_rv`。

注意 `ht_insert` 仅插入 `ht_entry`，而不插入数据本身。要访问数据，我们需要类似于在 `slist`（第 327 页）中用到的宏：

```cpp
struct ht_insert_rv ht_insert(struct hash_table *ht,
    void const key,
    size_t data_size ) {
    auto const hash = (*ht->hash_fn)( key );
    auto const n_buckets = HT_PRIME[ht->prime_idx];
    auto const b = hash % n_buckets;
    struct ht_entry *head = &ht->buckets[b];

    for (struct ht_entry *entry = head->next; entry != nullptr;
        entry = entry->next ) {
        if ((*ht->cmp_fn)( key, entry->data ) == 0 ) {
            return (struct ht_insert_rv){
                .entry, .inserted = false };
        }
    }

    struct ht_entry *entry = malloc(sizeof(struct ht_entry) + data_size);
    entry->next = head->next;
    entry->prev = head;
    if ( head->next != nullptr)
        head->next->prev = entry;
    head->next = entry;

    auto const lf = ++ht->size / (double)n_buckets;
    if ( lf > ht->max_lf)
        ht_grow( ht);

    return (struct ht_insert_rv){ entry, .inserted = true };
}
```

**列表 25.7:** 哈希表插入函数

```cpp
#define HT_DINT(ENTRY) ( (void*)(ENTRY)->data )
#define HT_DTR(ENTRY) ( (void*)(ENTRY)->prev )
```

基于此，你可以进行如下操作：

```cpp
struct ht_insert_rv rv = ht_insert(ht, "hello", sizeof(int));
if (rv.inserted) {
    HT_DINT(rv.entry) = "world";
}
```

## 25.5 增长

提到，`ht_grow` 函数通过增加 $m$ 并重新哈希所有条目来“增长”哈希表，如列表 25.8 所示。

```cpp
static void ht_grow(struct hash_table *ht) {
  unsigned new_buckets = HT_PRIME[++ht->prime_idx];
  struct ht_entry *new_buckets_ptr = calloc(new_buckets, sizeof(struct ht_entry));

  for (unsigned b = 0; b < HT_PRIME[ht->prime_idx-1]; ++b) {
    for (struct ht_entry *entry = ht->buckets[b].next,
        *next;
        entry != nullptr; entry = next ) {
      unsigned const hash = (*ht->hash_fn)( entry->data ) % new_buckets;
      struct ht_entry *head = &new_buckets_ptr[hash];

      entry->next = head->next;
      entry->prev = head;
      if ( head->next != nullptr)
        head->next->prev = entry;
      head->next = entry;
    }
  }
  free (ht->buckets);
  ht->buckets = new_buckets_ptr;
}
```

**列表 25.8:** 哈希表增长函数

## 25.6 查找

下一个写的函数是 `ht_find`，如列表 25.9 所示，逻辑非常直观。

```cpp
struct ht_entry* ht_find(struct hash_table *ht,
    void const key ) {
  unsigned const b = (*ht->hash_fn)( key ) % HT_PRIME[ht->prime_idx];
  for ( struct ht_entry *entry = ht->buckets[b].next; entry != nullptr;
      entry = entry->next ) {
    if ((*ht->cmp_fn)( key, entry->data ) == 0 )
      return entry;
  }
  return nullptr;
}
```

**列表 25.9:** 哈希表查找函数

## 25.7 删除

下一个写的函数是 `ht_delete`，如列表 25.10 所示。

```cpp
void ht_delete(struct hash_table *ht,
    struct ht_entry *entry ) {
  entry->prev->next = entry->next;
  if ( entry->next != nullptr )
    entry->next->prev = entry->prev;
  free(entry);
  --ht->size;
}
```

**列表 25.10:** 哈希表删除函数

## 25.8 迭代

如果不是顺序的，有时遍历整个哈希表是有用的，用于调试。迭代器类型和初始化函数如列表 25.11 所示。

```cpp
struct iter {
  unsigned bucket_idx;
  struct ht_entry *entry;
};

struct iter ht_begin(struct hash_table *ht) {
  return (struct iter){ .bucket_idx = (unsigned)-1, .entry = nullptr };
}

struct iter ht_next(struct hash_table *ht, iter *it) {
  if (it->entry != nullptr) {
    it->entry = it->entry->next;
    return *it;
  }
  do {
    it->bucket_idx++;
    if (it->bucket_idx >= HT_PRIME[ht->prime_idx]) {
      it->bucket_idx = 0;
    }
    it->entry = ht->buckets[it->bucket_idx].next;
  } while (it->entry == nullptr && it->bucket_idx != (unsigned)ht->prime_idx-1);
  return *it;
}
```

## 25.9 结语

```cpp
struct ht_iter {
    struct hash_table *ht;
    struct ht_entry *next;
    unsigned bucket_idx;
    unsigned n_buckets;
};

void ht_iter_init(struct ht_iter *it,
                   struct hash_table * ht ) {
    *it = (struct ht_iter){
        .ht = ht,
        .bucket_idx = (unsigned)-1,
        .n_buckets = HT_PRIME[ht->prime_idx]
    };
};
```

**列表 25.11:** 哈希表迭代器 `ht_next` 和初始化函数

```cpp
for (;;) {
    assert(it->n_buckets == HT_PRIME[it->prime_idx]);
    if (it->next != nullptr) {
        auto const entry = it->next;
        it->next = it->next->next;
        return entry;
    }
    if (++it->bucket_idx == it->n_buckets) {
        it->next = it->buckets[it->bucket_idx].next;
        return nullptr;
    }
}
```

**列表 25.12:** 哈希表迭代器 next 函数

无效。不检查此项会导致第 11 行出现未定义行为（§s15），因为尝试访问 `it->ht->buckets`，而这可能是一个悬空指针。

对于剩余代码，有三种情况：

- 1. 第 4-8 行处理当前桶的链表中有新条目的情况。
- 2. 第 9-10 行处理当前桶的链表中不再有条目，且没有更多桶的情况。
- 3. 第 11 行处理当前桶的链表中不再有条目，但至少还有一个桶的情况。

## 25.9 结语

正如在本章开头所暗示的，实现 map 有许多选择：

- *二叉树还是哈希表？*
- 对于二叉树，是哪种类型？AA、AVL、B、红黑树、splay 还是其他的？每种都有其权衡。
- 对于哈希表，是哪种函数？开放寻址法还是链地址法？对于链地址法，单链表还是双向链表？

某些选择取决于你的具体情况：

- *你的键是可比较的吗？也就是说，你能否写一个函数 `c(k_i, k_j)`，当键 `k_i < k_j`、`= k_j` 或 `> k_j` 时分别返回小于 `0`、`0` 或大于 `0` 的整数？这个函数快吗？*
- 你的键只能检查相等性吗？
- 你是否发现大多数时间只是偶尔进行*插入*操作？
- 你的键的迭代顺序重要吗？
- 你能付得起在扩展哈希表时解析所有内容的代价？
- 你需要删除键吗？

详细介绍所有选择可能会填满一整个学期的计算机科学课程。本章的选择仅触及表面，但希望已让你一窥某一种实现的内部细节。

## 习题

- 1. 编写列表 25.1（第334页）中 `fnvla64_mem` 的变体，用于哈希字符串的字符（终止符除外），其签名如下：

```c
uint64_t fnvla64_str( uint64_t hash, char const *s );
```

- 2. 目前，由于 §25.2 中提到的原因使用了双向链表。将实现更改为使用单链表。这需要：
  - a. 删除 `ht_entry->prev` 和 `ht_bucket->hash_val`。
  - b. 在 `ht_grow`（列表 25.8，第34页）中重新计算 `hash_val`。
  - c. 重新计算 `hash_val` 在 `ht_grow` 中（第11行）。
