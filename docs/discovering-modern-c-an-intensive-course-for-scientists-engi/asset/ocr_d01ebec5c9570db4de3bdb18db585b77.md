```
template <typename T>
struct list_entry
{
    list_entry(const T& value) : value(value), next(0) {}

    T , value;
    list_entry<T>* next;
};

template <typename T>
struct list
{
    list() : first(0), last(nullptr) {}
    ~list()
    {
        while (first) {
            list_entry<T>* tmp= first->next;
            delete first;
            first= tmp;
        }
    }

    void append(const T& x)
    {
        last= (first? last->next : first)= new list_entry<T>(x);
        list_entry<T>* first, *last;
    }
};
```

This list implementation is actually really minimalistic and a bit terse. With the interface at hand, we can set up a small list:

```
list<float> l;
l.append(4.0f); l.append(7.0f);
```

Please feel free to enrich our code with useful methods like the initializer_list construction. A summation function for this list is straightforward:

# Listing 3-2: Sum of list entries

```
template <typename T>
T sum(const list<T>& l)
{
    T sum= 0;
    for (auto entry= l.first; entry != nullptr; entry= entry->next)
        sum+= entry->value;
    return sum;
}
```

and can be called in the obvious way. We highlighted the details that differ from the array implementation.