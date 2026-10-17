
```cpp
namespace std {
template <class Container>
class back_insert_iterator : output_iterator_tag,void,void,void> {
protected:
    Container* container;
public:
    typedef Container container_type;
    explicit back_insert_iterator(Container& x);
    back_insert_iterator<Container>&
    operator=(const Container::value_type&);
    back_insert_iterator<Container>&
    operator=(typename Container::value_type&&);

    back_insert_iterator<Container>& operator*();
    back_insert_iterator<Container>& operator++();
    back_insert_iterator<Container> operator++(int);
};
template <class Container>
back_insert_iterator(Container& x) {
}
```

## 24.5.2.2 back_insert_iterator 操作

### 24.5.2.2.1 back_insert_iterator 构造函数

`explicit back_insert_iterator(Container& x);`

Effects: 初始化容器为 x。

### 24.5.2.2.2 back_insert_iterator::operator=

```
back_insert_iterator<Container>&
operator=(const Container::value_type& value);
Effects: container->push_back(value));
Returns: *this.
```

### 24.5.2.2.3 back_insert_iterator::operator*

```
back_insert_iterator<Container>& operator*();
```

### 24.5.2.2.4 back_insert_iterator::operator++

```
back_insert_iterator<Container>& operator++();
back_insert_iterator<Container> operator++(int);
Returns: *this.
```

### 24.5.2.2.5 back_inserter

```
template <class Container>
back_insert_iterator<Container> back_inserter(Container& x);
Returns: back_insert_iterator<Container>(x).
```

## 24.5.2.3 模板类 front_insert_iterator

```cpp
namespace std {
template<class Container>
class front_insert_iterator : 
public: front_insert_output_iterator_tag,void,void,void> {
protected:
    Container* c;
public:
    typedef Container::container_type;
    explicit front_insert_iterator(Container& x);
    front_insert_iterator<Container>&
    operator=(const Container::value_type& value);
    front_insert_iterator<Container>&
    operator=(typename Container::value_type& value);
front_insert_iterator<Container>& operator++();
front_insert_iterator<Container>& operator++();
front_insert_iterator<Container> operator++(int);
}
```

```
template<class Container>
front_insert_iterator<Container> front_inserter(Container& x);
```

## 24.5.2.4 front_insert_iterator 操作

### 24.5.2.4.1 front_insert_iterator 构造函数

`explicit front_insert_iterator(Container& x);`

Effects: 初始化容器为 x。

### 24.5.2.4.2 front_insert_iterator::operator=

```
front_insert_iterator<Container>&
operator=(const Container::value_type& value);
Effects: container->push_front(value);
Returns: *this.
```

```
front_insert_iterator<Container>&
operator=(typename Container::value_type&& value);
Effects: container->push_front(std::move(value));
Returns: *this.
```

### 24.5.2.4.3 front_insert_iterator::operator*

```
front_insert_iterator<Container>& operator=();
Returns: *this. 
```

### 24.5.2.4.4 front_insert_iterator::operator++

```
front_insert_iterator<Container>& operator++();

front_insert_iterator<Container> operator++(int);

Returns: *this.

```

### 24.5.2.4.5 front_inserter

```
template <class Container>

front_insert_iterator<Container> front_inserter(Container& x);

Returns: front_insert_iterator<Container>(x).

```

## 24.5.2.5 模板类 insert_iterator

[insert.iterator]

```
namespace std {

ntemplate <class Container>

class insert_iterator : public iterator_traits<std::output_iterator_tag,void,void,void,void> {

protected:

Container* container;

typename Container::iterator iter;

public:

    type_of Container container_type;

insert_iterator(Container& x, typename Container::iterator i);

insert_iterator<Container>&

operator=(typename Container::value_type&& value);

insert_iterator<Container>&

operator=(typename Container::value_type&& value);

insert_iterator<Container>* operator*();

insert_iterator<Container>& operator++();

insert_iterator<Container> operator++(int);

};

template <class Container>

insert_iterator<Container> inserter(Container& x, typename Container::iterator i);

}; // namespace std

```

§ 24.5.2.5

# ISO/IEC 14882:2011(E)

## 24.5.2.6 insert_iterator_operations

### 24.5.2.6.1 insert_iterator_constructor

[insert.iter.ops]

```
insert_iterator(Container& x, typename Container::iterator i);
```

影响：使用 &x 初始化容器，使用 i 初始化迭代器。

### 24.5.2.6.2 insert_iterator::operator=

[insert.iter.op=]

```
insert_iterator<Container>&
operator=(const typename Container::value_type& value);
```

影响：

```
iter = container->insert(iter, value);
++iter;
```

返回：*this.*

```
insert_iterator<Container>&
operator=(typename Container::value_type&& value);
```

影响：

```
iter = container->insert(iter, std::move(value));
++iter;
```

返回：*this.*

### 24.5.2.6.3 insert_iterator::operator*

[insert.iter.op*]

```
insert_iterator<Container>& operator*();
返回：*this.
```

### 24.5.2.6.4 insert_iterator::operator++

[insert.iter.op++]

```
insert_iterator<Container>& operator++();
insert_iterator<Container>& operator++(int);
返回：*this.
```

### 24.5.2.6.5 inserter

[inserter]

```
template <class Container>
insert_iterator<Container> inserter(Container& x, typename Container::iterator i);
返回：insert_iterator<Container>(x, i).
```

## 24.5.3 Move iterators

[move_iterators]

- 类模板 `move_iterator` 是一种迭代器适配器，其行为与底层迭代器相同，但其解引用运算符隐式地将底层迭代器解引用运算符返回的值转换为右值引用（rvalue reference）。可以使用 `move_iterator` 调用某些泛型算法，用移动代替拷贝。

[示例]:

```
list<string> s;
// 填充列表 s
vector<string> v1(s.begin(), s.end()); // 将字符串拷贝到 v1
vector<string> v2(move_iterator(s.begin()),
    make_move_iterator(s.end())); // 将字符串移动到 v2
```

- 示例结束

### 24.5.3.1 Class template move_iterator

[move_iterator]

```
namespace std {
template <class Iterator>
class move_iterator {
public:
    typedef Iterator::iterator_type iterator_type;
    typedef iterator_traits<Iterator>::difference_type difference_type;
    typedef Iterator::pointer pointer;
    typedef iterator_traits<Iterator>::value_type value_type;
    typedef iterator_traits<Iterator>::iterator_category iterator_category;
    typedef Iterator::value_type& reference;
    move_iterator()= default;
    explicit move_iterator(Iterator i);
    template <class U> move_iterator(const move_iterator<U>& u);
    template <class U> move_iterator& operator=(const move_iterator<U>& u);
    iterator_type base() const;
    reference operator*() const;
    pointer operator->() const;
    move_iterator& operator++();
    move_iterator operator++(int);
    move_iterator& operator--();
    move_iterator operator--(int);
    move_iterator operator+(difference_type n) const;
    move_iterator& operator+=(difference_type n);
    move_iterator operator-(difference_type n) const;
    move_iterator& operator-=(difference_type n);
    unspecified_type operator[](difference_type n) const;
    friend bool const operator==(const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
private:
    Iterator current; // 仅供说明
};
template <class Iterator1, class Iterator2>
bool operator==(const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator<(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator>(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator>==(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator>!(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <class Iterator1, class Iterator2>
bool operator>=(
    const move_iterator<Iterator1>& x, const move_iterator<Iterator2>& y);
template <Iterator>
auto operator++(
    const move_iterator<Iterator>& y) -> decltype(y.base()) {y.base()};
template <Iterator>
move_iterator<Iterator> operator+(
    difference_type n, const move_iterator<Iterator>& x);
template <Iterator>
move_iterator<Iterator> make_move_iterator(const Iterator& i);
```
