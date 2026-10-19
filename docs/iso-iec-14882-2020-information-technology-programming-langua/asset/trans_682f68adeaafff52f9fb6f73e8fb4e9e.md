

namespace std {
    template<class Key, class T, class Compare = less<Key>,
            class Allocator = allocator<pair<const Key, T>>>
    class multimap {
    public:
        // types
        using key_type            = Key;
        using mapped_type         = T;
        using value_type          = pair<const Key, T>;
        using key_compare         = Compare;
        using allocator_type      = Allocator;
        using pointer             = typename allocator_traits<Allocator>::pointer;
        using const_pointer       = typename allocator_traits<Allocator>::const_pointer;
        using reference           = value_type&;
        using const_reference     = const value_type&;
        using size_type           = implementation-defined; // see 22.2
        using difference_type     = implementation-defined; // see 22.2
        using iterator            = implementation-defined; // see 22.2
        using const_iterator      = implementation-defined; // see 22.2
        using reverse_iterator    = std::reverse_iterator<iterator>;
        using const_reverse_iterator = std::reverse_iterator<const_iterator>;
        using node_type           = unspecified;

        class value_compare {
            friend class multimap;
        protected:
            Compare comp;
            value_compare(Compare c) : comp(c) { }
        public:
            bool operator()(const value_type& x, const value_type& y) const {
                return comp(x.first, y.first);
            }
        };

        // 22.4.5.2, construct/copy/destroy
        multimap() : multimap(Compare()) { }
        explicit multimap(const Compare& comp, const Allocator& = Allocator());
        template<class InputIterator>
            multimap(InputIterator first, InputIterator last,
                     const Compare& comp = Compare(),
                     const Allocator& = Allocator());
        multimap(const multimap& x);
        multimap(multimap&& x);
        explicit multimap(const Allocator&);
        multimap(const multimap&, const Allocator&);
        multimap(multimap&&, const Allocator&);
        multimap(initializer_list<value_type>,
                 const Compare& = Compare(),
                 const Allocator& = Allocator());
        template<class InputIterator>
            multimap(InputIterator first, InputIterator last, const Allocator& a)
            : multimap(first, last, Compare(), a) { }
        multimap(initializer_list<value_type> il, const Allocator& a)
            : multimap(il, Compare(), a) { }
        ~multimap();
        multimap& operator=(const multimap& x);
        multimap& operator=(multimap&& x)
            noexcept(allocator_traits<Allocator>::is_always_equal::value &&
                     is_nothrow_move_assignable_v<Compare>);
        multimap& operator=(initializer_list<value_type>);
        allocator_type get_allocator() const noexcept;

        // iterators
        iterator        begin() noexcept;

## ISO/IEC 14882:2020(E)

复杂度：如果范围 [first, last) 已使用 comp 排序，则为 N 的线性，否则为 N log N，其中 N 为 last - first。

## 22.4.5.3 Modifiers [multimap.modifiers]

```
template<class P> iterator insert(P&& x);
template<class P> iterator insert(const_iterator position, P&& x);
```

约束：is_constructible_v<value_type, P&&> 为 true。

效果：第一种形式等价于 return emplace(std::forward<P>(x))。第二种形式等价于 return emplace_hint(position, std::forward<P>(x))。

## 22.4.5.4 Erasure [multimap.erasure]

```
template<class Key, class T, class Compare, class Allocator, class Predicate>
typename multimap<Key, T, Compare, Allocator>::size_type
erase_if(multimap<Key, T, Compare, Allocator>& c, Predicate pred);
```

效果：等价于：

```
auto original_size = c.size();
for (auto i = c.begin(), last = c.end(); i != last; ) {
  if (pred(*i)) {
    i = c.erase(i);
  } else {
    ++i;
  }
}
return original_size - c.size();
```

## 22.4.6 Class template set [set]

## 22.4.6.1 Overview [set.overview]

1 set 是一个关联容器，支持唯一键（每个键值最多包含一个）并提供快速检索键本身。set 类支持双向迭代器。

2 set 满足容器、双向容器（22.2）、关联容器（22.2.6）和分配器感知容器（表 76）的所有要求。set 还提供了 22.2.6 中针对唯一键描述的大多数操作。这意味着 set 支持 22.2.6 中的 a_uniq 操作，但不支持 a_eq 操作。对于 set<Key>，key_type 和 value_type 均为 Key。这里仅对 set 上未在这些表中描述的操作以及存在额外语义信息的操作提供说明。

```
namespace std {
  template<class Key, class Compare = less<Key>,
    class Allocator = allocator<Key>>
  class set {
  public:
    // types
    using key_type = Key;
    using key_compare = Compare;
    using value_type = Key;
    using value_compare = Compare;
    using allocator_type = Allocator;
    using pointer = typename allocator_traits<Allocator>::pointer;
    using const_pointer = typename allocator_traits<Allocator>::const_pointer;
    using reference = value_type&;
    using const_reference = const value_type&;
    using size_type = implementation-defined; // see 22.2
    using difference_type = implementation-defined; // see 22.2
    using iterator = implementation-defined; // see 22.2
    using const_iterator = implementation-defined; // see 22.2
    using reverse_iterator = std::reverse_iterator<iterator>;
    using const_reverse_iterator = std::reverse_iterator<const_iterator>;
    using node_type = unspecified;
    using insert_return_type = insert-return-type<iterator, node_type>;
```

```
// 22.4.6.2, construct/copy/destroy
set() : set(Compare()) { }
explicit set(const Compare& comp, const Allocator& = Allocator());
template<class InputIterator>
    set(InputIterator first, InputIterator last,
        const Compare& comp = Compare(), const Allocator& = Allocator());
set(const set& x);
set(set&& x);
explicit set(const Allocator&);
set(const set&, const Allocator&);
set(set&&, const Allocator&);
set(initializer_list<value_type>, const Compare& = Compare(),
    const Allocator& = Allocator());
template<class InputIterator>
    set(InputIterator first, InputIterator last, const Allocator& a)
        : set(first, last, Compare(), a) { }
set(initializer_list<value_type> il, const Allocator& a)
    : set(il, Compare(), a) { }
~set();
set& operator=(const set& x);
set& operator=(set&& x)
    noexcept(allocator_traits<Allocator>::is_always_equal::value &&
             is_nothrow_move_assignable_v<Compare>);
set& operator=(initializer_list<value_type>);
allocator_type get_allocator() const noexcept;

// iterators
iterator            begin() noexcept;
const_iterator      begin() const noexcept;
iterator            end() noexcept;
const_iterator      end() const noexcept;

reverse_iterator    rbegin() noexcept;
const_reverse_iterator rbegin() const noexcept;
reverse_iterator    rend() noexcept;
const_reverse_iterator rend() const noexcept;

const_iterator      cbegin() const noexcept;
const_iterator      cend() const noexcept;
const_reverse_iterator crbegin() const noexcept;
const_reverse_iterator crend() const noexcept;

// capacity
[[nodiscard]] bool empty() const noexcept;
size_type size() const noexcept;
size_type max_size() const noexcept;

// modifiers
template<class... Args> pair<iterator, bool> emplace(Args&&... args);
template<class... Args> iterator emplace_hint(const_iterator position, Args&&... args);
pair<iterator,bool> insert(const value_type& x);
pair<iterator,bool> insert(value_type&& x);
iterator insert(const_iterator position, const value_type& x);
iterator insert(const_iterator position, value_type&& x);
template<class InputIterator>
    void insert(InputIterator first, InputIterator last);
void insert(initializer_list<value_type>);

node_type extract(const_iterator position);
node_type extract(const key_type& x);
insert_return_type insert(node_type&& nh);
iterator            insert(const_iterator hint, node_type&& nh);
```

