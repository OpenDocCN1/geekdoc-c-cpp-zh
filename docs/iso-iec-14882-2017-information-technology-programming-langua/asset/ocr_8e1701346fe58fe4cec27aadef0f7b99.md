# ISO/IEC 14882:2017(E)

# 27.5.2.5 Class template insert_iterator

```
namespace std {
    template <class Container>
    class insert_iterator {
    protected:
        Container+ container;
        typename Container::iterator iterator;

    public:
        using iterator_category = output_iterator_tag;
        using value_type = void;
        using difference_type = void;
        using pointer = void;
        using reference = void;
        using const_type = Container;

        insert_iterator(Container& x, typename Container::iterator i);
        insert_iterator& operator=(const typename Container::value_type& value);
        insert_iterator& operator+(typename Container::value_type& value);

        insert_iterator& operator*();
        insert_iterator& operator++();
        insert_iterator& operator++(int);
    };

template <class Container>
insert_iterator<Container> inserter(Container& x, typename Container::iterator i);
```

![](bbox=[0.768, 0.126, 0.881, 0.137])

# 27.5.2.6 insert_iterator operations

# 27.5.2.6.1 insert_iterator constructor

![](bbox=[0.768, 0.48, 0.881, 0.491])

insert_iterator(Container& x, typename Container::iterator i);

# 27.5.2.6.2 insert_iterator::operator=

![](bbox=[0.753, 0.544, 0.881, 0.555])

insert_iterator& operator=(const typename Container::value_type& value);

+   - Effects: Initializes container with addressof(x) and iter with i.

As if by:

+   - 1 iter = container->insert(iter, value);
- ++iter;

+   - Returns: *this.

insert_iterator& operator+(typename Container::value_type& value);

As if by:

+   - 3 iter = container->insert(iter, std::move(value));
- ++iter;

+   - Returns: *this.

# 27.5.2.6.3 insert_iterator::operator*

![](bbox=[0.763, 0.782, 0.881, 0.793])

insert_iterator& operator*();

+   - Returns: *this.