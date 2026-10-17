
```cpp
iterator insert(const iterator& pos, const T& x);

iterator insert(const iterator& pos, T&& x);

template <class... Args>

iterator emplace(const iterator& pos, Args&&... args);

iterator insert(const_iterator pos, const T& x);

iterator insert(const_iterator pos, T&& x);

template <class... Args>

iterator emplace(const_iterator pos, Args&&... args);

void insert(const_iterator pos, const T& x);

void insert(const_iterator pos, T&& x);

template <class... Args>

void emplace(const_iterator pos, Args&&... args);

void erase(size_type pos);

iterator erase(const iterator& pos);

iterator erase(const const_iterator& pos);

void erase(const_iterator first, const_iterator last);

void erase(const const_iterator first, const const_iterator last);

void clear() noexcept;

void swap(vector& other) noexcept;

void swap(const vector& other) noexcept;
```
};

# 23.3.6.2 vector 构造函数、拷贝和赋值

`vector(const Allocator& alloc = Allocator())`
- 1 影响：使用指定的分配器构造一个空 `vector`。
- 2 复杂度：常数级。

`vector(size_type n, const Allocator& alloc = Allocator())`
- 3 影响：使用指定的分配器构造一个具有 `n` 个默认插入元素的 `vector`。
- 4 要求：`T` 应该是可默认插入到 `*this*` 的。
- 5 复杂度：相对于 `n` 是线性的。

`vector(size_type n, const T& value, const Allocator& alloc = Allocator()) noexcept`
- 6 影响：使用指定的分配器构造一个包含 `n` 个 `value` 拷贝的 `vector`。
- 7 要求：`T` 应该是是拷贝插入到 `*this*` 的。
- 8 复杂度：相对于 `n` 是线性的。

`template <class InputIterator> vector(InputIterator first, InputIterator last, const Allocator& alloc = Allocator()) noexcept`
- 9 影响：使用指定的分配器构造一个等于范围 `[first, last)` 的 `vector`。
- 10 复杂度：如果迭代器 `first` 和 `last` 属于前向、双向或随机访问类别，则只调用 `N` 次 `T` 的构造函数（其中 `N` 是 `first` 和 `last` 之间的距离），且不进行重新分配。如果不是，则进行顺序 `N` 次 `T` 的构造函数调用和顺序 `log(N)` 次重新分配。它们

# ISO/IEC N4296

## 23.3.6.3 [vector.capacity]

`size_type capacity() const noexcept;`
- 1 返回：`vector` 在不需重新分配的情况下可以容的元素总数。

`reserve(size_type n);`
- 3 影响：一个指令，通知 `vector` 计划中的大小变化，以便其进行管理。
- 4 备注：如果 `n > capacity()`，则重新分配内存，使得容量至少能容纳 `n` 个元素。
- 5 复杂度：如果 `n > capacity()`，则为 $O(n)$；否则为 $O(1)$。
- 6 抛出：如果 `Allocator::allocate()` 抛出异常。

`void resize(size_type n);`
- 1 影响：如果 `n > size()`，则通过 `n - size()` 次值初始化构造新元素。
- 2 备注：如果 `n > capacity()`，则重新分配内存，使得容量至少能容纳 `n` 个元素。
- 3 复杂度：如果 `n > capacity()`，则为 $O(n)$；否则为 $O(1)$。
- 4 抛出：如果 `n > max_size()`，则抛出 `length_error`。

`void shrink_to_fit();`
- 1 影响：如果 `size() < capacity()`，则减少容量以恰好等于 `size()`。
- 2 复杂度：如果 `size() < capacity()`，则为 $O(n)$；否则为 $O(1)$。

## 23.3.6.4 vector data

[vector.data]

```cpp
T* data() noexcept;

const T* data() const noexcept;
```
- 1 返回：指向第一个元素的指针，使得 `[data(), data() + size())` 是有效范围。
- 2 复杂度：$O(1)$。

## 23.3.6.5 vector modifiers

[vector.modifiers]

```cpp
iterator insert(const_iterator position, const x);

iterator insert(const_iterator position, T&& x);

iterator insert(const_iterator position, size_type n, const T& x);

template<class InputIterator>

iterator insert(const_iterator position, InputIterator first, InputIterator last);

iterator insert(const_iterator position, initializer_list<T> it);
```

```cpp
template<class... Args>

void& emplace(Args&&... args);

template<class... Args>

void& emplace(const_iterator position, Args&&... args);

void push_back(const T& x);

void push_back(T&& x);
```
- 1 备注：如果大小大于容量，则发生重新分配。如果没有发生重新分配，则插入点之前的迭代器和引用保持有效。如果在在末尾插入单个元素时抛出异常，且 `T` 是可插入的或 `is_no_move_constructible<T>::value` 为真，则不产生影响。否则，如果非可插入的 `T` 的移动构造函数抛出异常，则影响不确定。

```cpp
iterator erase(const_iterator position);

iterator erase(const_iterator first, const_iterator last);
```
- 3 影响：失效删除点处或之后的迭代器和引用。
- 4 复杂度：被删除元素数量加上 `vector` 末尾距离的线性复杂度。
- 5 备注：`T` 的析构函数调用次数等于被删除元素的个数，但 `T` 的移动赋值运算符调用次数等于 `vector` 中被删除之后的元素个数。
- 6 抛出：除非 `T` 的拷贝构造函数、移动构造函数、赋值运算符或移动赋值运算符抛出异常，否则不抛出。

```cpp
void swap(vector& x);
```
- 1 影响：交换 `this` 的内容与 `x` 的内容。
- 2 复杂度：$O(1)$。

```cpp
void resize(size_type n, const T& x);
```
- 1 影响：如果 `n > size()`，则通过 `n - size()` 次值初始化构造新元素。
- 2 备注：如果 `n > capacity()`，则重新分配内存，使得容量至少能容纳 `n` 个元素。
- 3 复杂度：如果 `n > capacity()`，则为 $O(n)$；否则为 $O(1)$。
- 4 抛出：如果 `n > max_size()`，则抛出 `length_error`。

```cpp
void resize(size_type n);
```
- 1 影响：如果 `n < size()`，则通过 `size() - n` 次析构处理多余元素。
- 2 备注：如果 `n > capacity()`，则重新分配内存，使得容量至少能容纳 `n` 个元素。
- 3 复杂度：如果 `n > capacity()`，则为 $O(n)$；否则为 $O(1)$。

## 23.3.6.6 vector specialized algorithms

[vector.specialized]

```cpp
template<class T, class Allocator = Allocator<T>>

class vector {
    // ...之前的成员 ...
```

## 23.3.6.7 vector<bool>

为了优化空间，提供了针对 `bool` 的 `vector` 特殊化版本：

```cpp
namespace std {
template<class Allocator = Allocator<bool>>

class vector<bool, Allocator> {
    // ... 特殊化细节 ...
};
```

# ISO/IEC
# N4296

2 除非另有说明，所有操作的要求和语义都与主向量模板相同，但处理值类型的操作将映射到常量容器存储中的位值，且不使用 `allocator_traits::construct` (20.7.8.2) 来构造这些值。

3 不要求数据必须存储为 `bool` 值的连续分配。相反，建议使用空间优化的位表示。

4 `reference` 是一个类，模拟 `vector<bool>` 中单个位引用的行为。转换运算符在位被设置时返回 `true`，否则返回 `false`。赋值运算符在参数为（可转换为）`true` 时设置该位，否则清除该位。`flip` 反反转该位的状态。

```cpp
void flip() noexcept;
```
- 5 效果：将容器中的每个元素替换为它的

```cpp
static void swap(reference& x, reference& y) noexcept;
```
- 6 效果：交换 `x` 和 `y` 的内容，仿佛

```cpp
bool b = x;

y = b;
```

```cpp
template <class Allocator> struct hash<vector<bool>, Allocator>;
```
7 模板特化应满足类模板 `hash` (20.9.13)的要求。

## 23.4 关联容器 [associative]

### 23.4.1 通用 [associative.general]

1 头文件 `<map>` 定义了类模板 `map` 和 `multimap`；头文件 `<set>` 定义了类 `set` 和 `multiset`。

### 23.4.2 Header <map> 摘要 [associative.map.syn]

```cpp
template <class Key, class T, class Compare = less<Key>
  class Allocator = allocator<pair<const Key, T>>
class map {
  template <class Key, class T, class Compare, class Allocator>
    bool operator=(const map<const Key,T,Compare, Allocator>& x,
                   const map<const Key,T,Compare, Allocator>& y);
    template <class Key, class T, class Compare, class Allocator>
    bool operator=(const map<const Key,T,Compare, Allocator>& x,
                   const map<const Key,T,Compare, Allocator>& y);
    template <class Key, class T, class Compare, class Allocator>
    bool operator!=(const map<const Key,T,Compare, Allocator>& x,
                   const map<const Key,T,Compare, Allocator>& y);
    template <class Key, class T, class Compare, class Allocator>
    bool operator>=(const map<const Key,T,Compare, Allocator>& x,
                   const map<const Key,T,Compare, Allocator>& y);
    template <class Key, class T, class Compare, class Allocator>
    bool operator<=(const map<const Key,T,Compare, Allocator>& x,
                   const map<const Key,T,Compare, Allocator>& y);
    template <class Key, class T, class Compare, class Allocator>
    bool operator<(const mapKey<T,Compare,Allocator>& x,
                 const mapKey<T,Compare,Allocator>& y);
    template <class Key, class T, class Compare, class Allocator>
    void swap(mapKey<T,Compare,Allocator>& x,
           mapKey<T,Compare,Allocator>& y)
           noexcept(noexcept(x.swap(y)));
template <class Key, class T, class Compare, class Allocator>
class Allocator = allocator<pair<const Key, T>> >
class map:
  template <class Key, class T, class Compare, class Allocator>
    bool operator+=(const mapKey<T,Compare,Allocator>& x,
           const mapKey<T,Compare,Allocator>& y);
  template <class Key, class T, class Compare, class Allocator>
    bool operator=(const mapKey<T,Compare,Allocator>& x,
           const mapKey<T,Compare,Allocator>& y);
  template <class Key, class T, class Compare, class Allocator>
    bool operator<(const mapKey<T,Compare,Allocator>& x,
           const mapKey<T,Compare,Allocator>& y);
  template <class Key, class T, class Compare, class Allocator>
    bool operator<=(const mapKey<T,Compare,Allocator>& x,
           const mapKey<T,Compare,Allocator>& y);
  template <class Key, class T, class Compare, class Allocator>
    bool operator>(const mapKey<T,Compare,Allocator>& x,
           const mapKey<T,Compare,Allocator>& y);
  template <class Key, class T, class Compare, class Allocator>
```
