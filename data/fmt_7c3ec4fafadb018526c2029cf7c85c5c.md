
`using container_node_type = unspecified;`

`using allocator_traits = allocator<container_node_type>;`

public:

`node_handle() noexcept = ptr_(), alloc_() {}`

`typename node_handle::rebind_traits<container_node_type>::pointer ptr;`

`optional<allocator_type> alloc_ = alloc_,`

public:

`const value_type value() const noexcept;` // 不用于 map 容器

`const key_type key() const noexcept;` // 不用于 set 容器

`const mapped_type mapped() const noexcept;` // 不用于 set 容器

`allocator_type get_allocator() const;`

`explicit operator bool() const noexcept;`

`bool empty() const noexcept;`

`void swap(node_handle& other) noexcept(allocator_traits::propagate_on_container_swap::value || allocator_traits::is_always_equal==value);`

`friend void swap(node_handle x, node_handle y) noexcept(noexcept(x.swap(y))) { x.swap(y); }`

};

## 26.2.4.2 node_handle 构造函数、拷贝和赋值 [container.node.cons]

```cpp
node_handle(node_handle&& nh) noexcept;
```

- 效果：构造一个 `node_handle` 对象，使用 `nh.ptr_` 初始化 `ptr_`。使用 `nh.alloc_` 初始化 `alloc_`。将 `nullptr` 赋值给 `nh.ptr_` 并将 `nullptr` 赋值给 `nh.alloc_`.

```cpp
node_handle& operator=(node_handle&&);
```

- 要求：`alloc_`，或者 `allocator_traits::propagate_on_container_move_assignment` 为 `true`，或者 `alloc_ == nh.alloc_`；
- 效果：
    - 如果 `ptr_ != nullptr`，销毁 `ptr_` 指向的 `container_type` 对象中的 `value_type` 子对象，调用 `allocator_traits::destroy`，然后通过调用 `allocator_traits::rebind_traits<container_node_type>` 释放 `ptr_`。
    - 将 `nh.ptr_` 赋值给 `ptr_`
    - 如果 `alloc_`，或者 `allocator_traits::propagate_on_container_move_assignment` 为 `true`，将 `nh.alloc_` 赋值给 `alloc_`
    - 将 `nullptr` 赋值给 `nh.ptr_` 并将 `nullptr` 赋值给 `nh.alloc_`
    - 返回 `*this`。
    - 抛异常：无。

## 26.2.4.3 node_handle 析构函数 [container.node.dt]

```cpp
~node_handle();
```

- 效果：如果 `ptr_ != nullptr`，销毁 `ptr_` 指向的 `container_type` 对象中的 `value_type` 子对象，调用 `allocator_traits::destroy`，然后通过调用 `allocator_traits::rebind_traits<container_node_type>` 释放 `ptr_`。

## 26.2.4.4 node_handle 观察者 [container.node.observers]

```cpp
value_type& value() const;
```

- 要求：`empty() == false`。
- 返回 `ptr_` 指向的 `container_type` 对象中的 `value_type` 引用。
- 抛异常：无。

```cpp
key_type& key() const;
```

- 要求：`empty() == false`。
- 返回 `ptr_` 指向的 `container_type` 对象中的 `key_type` 引用。
- 抛异常：无。
- 备注：允许通过返回的引用进行修改。

```cpp
mapped_type& mapped() const;
```

- 要求：`empty() == false`。
- 返回 `ptr_` 指向的 `container_type` 对象中的 `mapped_type` 引用。
- 抛异常：无。

```cpp
allocator_type get_allocator() const;
```

- 要求：`empty() == false`。
- 返回 `*alloc_`。
- 抛异常：无。

```cpp
explicit operator bool() const noexcept;
```

- 返回 `ptr_ != nullptr`。

```cpp
bool empty() const noexcept;
```

- 返回 `ptr_ == nullptr`。

## 26.2.4 node_handle 修改器 [container.node.modifiers]

```cpp
void swap(node_handle h) noexcept(allocator_traits::propagate_on_container_swap == value || allocator_traits::is_always_equal==value);
```

- 要求：`allocator_traits::propagate_on_container_swap == value || allocator_traits::is_always_equal==value;`
- 1 如果 `allocator_traits::propagate_on_container_swap == value || allocator_traits::is_always_equal==value`，交换内容。
- 2 如果 `allocator_traits::propagate_on_container_swap == value || allocator_traits::is_always_equal==value`，交换内容。

## 26.2.4.5 插入 [container.node.insert]

- 1 关联容器返回一个包含指向插入元素的迭代器和布尔值的对（`pair`）。

```cpp
template<class Iterator, class bool>
struct insert_result {
  Iterator it;
  bool inserted;
};
```
