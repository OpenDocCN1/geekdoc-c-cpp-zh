# (FIGURE 4.11 continued)

```
void bag::insert(const value_type& entry)
{
    if (used == capacity)
    {
        reserve(used+1);
        data[used] = entry;
        ++used;
    }
}
```

The first action of the insert function is to ensure that there is room for a new item.

```
void bag::operator +=(const bag& addend)
// Library facilities used: algorithm
{
    if (used + addend.used > capacity)
        reserve(used + addend.used);
    copy(addend.data, addend.data + addend.used, data + used);
    used += addend.used;
}
```

The += operator starts by ensuring that there is enough room for the new items.

```
void bag::operator =(const bag& source)
||
See the implementation in Figure 4.10 on page 190.
```

```
bag::size_type bag::count(const value_type& target) const
||
No change from the original bag: See the implementation in Figure 3.6 on page 119.
```

```
bag operator +(const bag& b1, const bag& b2)
{
    bag answer(b1.size( ) + b2.size( ));
    answer += b1;
    answer += b2;
    return answer;
}
```

The function declares a bag of sufficient size.

# Self-Test Exercises for Section 4.3

+   16. Describe the difference between a dynamic data structure and a static data structure.
+   
+   17. Why does a programmer need to be concerned with the initial capacity of a container if dynamic memory can be allocated as needed?
+   
+   18. Suppose that you declare a bag like this: `bag exercise;`. What is the initial capacity? What will happen if you try to put 31 items in the bag?