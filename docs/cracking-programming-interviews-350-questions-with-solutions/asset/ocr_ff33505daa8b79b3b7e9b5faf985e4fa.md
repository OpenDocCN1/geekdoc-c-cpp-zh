```
```cpp
int main()
{
    int a[] = {8, 1, 6, 4, 0, 3, 9, 5};

    int *p = partition(a, a + 7);

    std::cout << "Array after partition"
              << std::endl;

    for (auto e : a)
        std::cout << e << " ";

    std::cout << std::endl;

    std::cout << "partition index: "
              << std::distance(std::begin(a), p) << ","
              << " partitioning element: " << *p
              << std::endl;
}
```
```

This prints:

```
```text
Array after partition
1 4 0 3 5 8 9 6
partition index: 4, partitioning element: 5
```
```

# std::partition

STL also provides a version of partition algorithm which looks like:

# Program 6.10: std::partition

```
```cpp
template <typename BidirectionalIterator,
          typename Predicate>
BidirectionalIterator
partition(BidirectionalIterator first,
          BidirectionalIterator last,
          Predicate pred)
{
    while (true)
    {
        while (true)
        {
            if (first == last)
                return first;
            if (!pred(*first))
                break;
            ++first;
        }
        do
        {
            if (first == last)
                return first;
```
```