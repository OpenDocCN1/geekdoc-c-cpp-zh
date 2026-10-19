

## 22.3.9.3 迭代器 [forwardlist.iter]

```
iterator before_begin() noexcept;
const_iterator before_begin() const noexcept;
const_iterator cbefore_begin() const noexcept;
```

返回：一个不可解引用的迭代器，其递增后等于 begin() 返回的迭代器。

效果：cbefore_begin() 等价于 const_cast<forward_list const&>(*this).before_begin()。

说明：before_begin() == end() 必须等于 false。

## 22.3.9.4 元素访问 [forwardlist.access]

```
reference front();
const_reference front() const;
```

返回：*begin()

## 22.3.9.5 修改器 [forwardlist.modifiers]

insert_after 的所有重载都不应影响迭代器和引用的有效性，而 erase_after 仅使指向被删除元素的迭代器和引用失效。如果 insert_after 在执行过程中抛出异常，则不应产生任何效果。将 n 个元素插入到 forward_list 中是关于 n 的线性操作，且对 T 的拷贝或移动构造函数的调用次数恰好等于 n。从 forward_list 中删除 n 个元素是关于 n 的线性操作，且对类型 T 的析构函数的调用次数恰好等于 n。

```
template<class... Args> reference emplace_front(Args&&... args);
```

效果：在列表开头插入一个使用 value_type(std::forward<Args>(args)...) 构造的 value_type 类型的对象。

```
void push_front(const T& x);
void push_front(T&& x);
```

效果：在列表开头插入 x 的拷贝。

```
void pop_front();
```

效果：如同执行 erase_after(before_begin())。

```
iterator insert_after(const_iterator position, const T& x);
iterator insert_after(const_iterator position, T&& x);
```

前提条件：position 是 before_begin() 或是 [begin(), end()] 范围内的可解引用迭代器。

效果：在 position 之后插入 x 的拷贝。

返回：指向 x 的拷贝的迭代器。

效果：使用指定的分配器构造一个包含 n 个默认插入元素的 forward_list 对象。

复杂度：关于 n 的线性。

```
forward_list(size_type n, const T& value, const Allocator& = Allocator());
```

前提条件：T 可在 *this 中进行 Cpp17CopyInsertable 操作。

效果：使用指定的分配器构造一个包含 n 个 value 的拷贝的 forward_list 对象。

复杂度：关于 n 的线性。

```
template<class InputIterator>
forward_list(InputIterator first, InputIterator last, const Allocator& = Allocator());
```

效果：构造一个等于范围 [first, last) 的 forward_list 对象。

复杂度：关于 distance(first, last) 的线性。

## 22.3.9.6 操作 [forwardlist.ops]

1 在本小节中，名为 Predicate 或 BinaryPredicate 的模板参数的实参应满足 25.2 中的相应要求。对于 merge 和 sort，适用 25.8 中的定义和要求。

```
void splice_after(const_iterator position, forward_list& x);
void splice_after(const_iterator position, forward_list&& x);
```

2 前提条件：position 是 before_begin() 或是 [begin(), end()] 范围内的可解引用迭代器。get_allocator() == x.get_allocator() 为 true。addressof(x) != this 为 true。

3 效果：将 x 的内容插入到 position 之后，且 x 变为空。指向 x 的移动元素的指针和引用现在引用这些相同的元素，但作为 *this 的成员。引用移动元素的迭代器将继续引用其元素，但现在表现为指向 *this 而非 x 的迭代器。

4 抛出：无。

5 复杂度：𝒪(distance(x.begin(), x.end()))

```
void splice_after(const_iterator position, forward_list& x, const_iterator i);
void splice_after(const_iterator position, forward_list&& x, const_iterator i);
```

6 前提条件：position 是 before_begin() 或是 [begin(), end()] 范围内的可解引用迭代器。i 之后的迭代器在 x 中是可解引用的。get_allocator() == x.get_allocator() 为 true。

7 效果：将 i 之后的元素插入到 *this 中，位于 position 之后，并从 x 中移除之。若 position == i 或 position == ++i，则结果不变。指向 *++i 的指针和引用继续引用同一元素，但作为 *this 的成员。指向 *++i 的迭代器继续引用同一元素，但现在表现为指向 *this 而非 x 的迭代器。

8 抛出：无。

9 复杂度：𝒪(1)

```
void splice_after(const_iterator position, forward_list& x,
    const_iterator first, const_iterator last);
void splice_after(const_iterator position, forward_list&& x,
    const_iterator first, const_iterator last);
```

10 前提条件：position 是 before_begin() 或是 [begin(), end()] 范围内的可解引用迭代器。(first, last) 是 x 中的有效范围，且范围 (first, last) 中的所有迭代器均可解引用。position 不是范围 (first, last) 中的迭代器。get_allocator() == x.get_allocator() 为 true。

11 效果：将范围 (first, last) 中的元素插入到 position 之后并从 x 中移除。指向 x 的移动元素的指针和引用现在引用这些相同的元素，但作为 *this 的成员。引用移动元素的迭代器将继续引用其元素，但现在表现为指向 *this 而非 x 的迭代器。

12 复杂度：𝒪(distance(first, last))

```
size_type remove(const T& value);
template<class Predicate> size_type remove_if(Predicate pred);
```

13 效果：删除列表中由列表迭代器 i 引用的所有元素，对于这些元素满足以下条件：*i == value（对于 remove()），pred(*i) 为 true（对于 remove_if()）。仅使指向被删除元素的迭代器和引用失效。

14 返回：被删除的元素数量。

15 抛出：除非相等比较或谓词抛出异常，否则不抛出。

16 说明：稳定（16.4.6.8）。

17 复杂度：对相应谓词的恰好 distance(begin(), end()) 次应用。

```
size_type unique();
template<class BinaryPredicate> size_type unique(BinaryPredicate pred);
```

18 效果：从范围 [first + 1, last) 中由迭代器 i 引用的每个相邻相等元素组中删除除第一个元素之外的所有元素，对于 *i == *(i-1)（对于无参数版本的情况

```
```cpp
size_type size() const noexcept;
size_type max_size() const noexcept;
void resize(size_type sz);
void resize(size_type sz, const T& c);

// element access
reference       front();
const_reference front() const;
reference       back();
const_reference back() const;

// 22.3.10.4, modifiers
template<class... Args> reference emplace_front(Args&&... args);
template<class... Args> reference emplace_back(Args&&... args);
void push_front(const T& x);
void push_front(T&& x);
void pop_front();
void push_back(const T& x);
void push_back(T&& x);
void pop_back();

template<class... Args> iterator emplace(const_iterator position, Args&&... args);
iterator insert(const_iterator position, const T& x);
iterator insert(const_iterator position, T&& x);
iterator insert(const_iterator position, size_type n, const T& x);
template<class InputIterator>
  iterator insert(const_iterator position, InputIterator first, InputIterator last);
iterator insert(const_iterator position, initializer_list<T> il);

iterator erase(const_iterator position);
iterator erase(const_iterator position, const_iterator last);
void     swap(list& x) noexcept(allocator_traits<Allocator>::is_always_equal::value);
void     clear() noexcept;

// 22.3.10.5, list operations
void splice(const_iterator position, list& x);
void splice(const_iterator position, list&& x);
void splice(const_iterator position, list& x, const_iterator i);
void splice(const_iterator position, list&& x, const_iterator i);
void splice(const_iterator position, list& x, const_iterator first, const_iterator last);
void splice(const_iterator position, list&& x, const_iterator first, const_iterator last);

size_type remove(const T& value);
template<class Predicate> size_type remove_if(Predicate pred);

size_type unique();
template<class BinaryPredicate>
  size_type unique(BinaryPredicate binary_pred);

void merge(list& x);
void merge(list&& x);
template<class Compare> void merge(list& x, Compare comp);
template<class Compare> void merge(list&& x, Compare comp);

void sort();
template<class Compare> void sort(Compare comp);

void reverse() noexcept;
};

template<class InputIterator, class Allocator = allocator<iter-value-type<InputIterator>>>
list(InputIterator, InputIterator, Allocator = Allocator())
  -> list<iter-value-type<InputIterator>, Allocator>;
```
```
