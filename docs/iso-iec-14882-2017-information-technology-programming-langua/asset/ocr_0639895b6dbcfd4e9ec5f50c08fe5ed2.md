# ISO/IEC 14882:2017(E)

using container_type = Container;

```
explicit back_insert_iterator operator=(const Container& x);
back_insert_iterator& operator=(const typename Container::value_type& value);
back_insert_iterator& operator=(const typename Container::value_type& value);
back_insert_iterator operator++();
back_insert_iterator operator++();
back_insert_iterator operator++(int);
```

```
template <class Container>
back_insert_iterator<Container> back_inserter(Container& x);
```

# 27.5.2.2 back_insert_iterator operations

# 27.5.2.2.1 back_insert_iterator constructor

```
explicit back_insert_iterator(Container& x);
```

> Effects: initializes container with address(x).

# 27.5.2.2.2 back_insert_iterator::operator=

```
back_insert_iterator& operator=(const typename Container::value_type& value);
```

> Effects: As if: container->push_back(value);

```
back_insert_iterator& operator=(const typename Container::value_type&& value);
```

> Effects: As if: container->push_back(std::move(value));

# 27.5.2.2.3 back_insert_iterator::operator*

```
back_insert_iterator& operator();
```

> Returns: *this.

# 27.5.2.2.4 back_insert_iterator::operator++

```
back_insert_iterator& operator++();
back_insert_iterator operator++(int);
```

> Returns: *this.

# 27.5.2.2.5 back_inserter

```
template <class Container>
back_insert_iterator<Container> back_inserter(Container& x);
```

> Returns: back_insert_iterator<Container>(x).

# 27.5.2.3 Class template front_insert_iterator

```
namespace std {
    template <class Container>
    class front_insert_iterator {
    protected:
        Container container;
```

§ 27.5.2.3

©ISO/IEC 2017 – All rights reserved

970