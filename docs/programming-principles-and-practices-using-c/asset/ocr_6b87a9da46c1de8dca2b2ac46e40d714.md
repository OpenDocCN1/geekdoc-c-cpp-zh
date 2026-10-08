# ## 21.9 Container algorithms

So, we define standard library algorithms in terms of sequences of elements specified by iterators. An input sequence is defined as a pair of iterators [b:e) where **b** points to the first element of the sequence and **e** to the one-past-the-end element of the sequence (§20.3). An output sequence is specified as simply an iterator to its first element. For example:

```
```cpp
void test(vector<int> & v)
{
    sort(v.begin(),v.end());   // sort v's element from v.begin() to v.end()
}
```
```

This is nice and general. For example, we can sort half a **vector**:

```
```cpp
void test(vector<int> & v)
{
    sort(v.begin(),v.begin()+v.size()/2);   // sort first half of v's elements
    sort(v.begin()+v.size()/2,v.end());      // sort second half of v's elements
}
```
```

However, specifying the range of elements is a bit verbose, and most of the time, we sort all of a **vector** and not just half. So, most of the time, we want to write

```
```cpp
void test(vector<int> & v)
{
    sort(v);     // sort v
}
```
```

That variant of sort() is not provided by the standard library, but we can define it for ourselves:

```
```cpp
template<typename C>   // requires Container<C>()
void sort(C& c)
{
    std::sort(c.begin(),c.end());
}
```
```

In fact, we found it so useful that we added it to std_lib_facilities.h.