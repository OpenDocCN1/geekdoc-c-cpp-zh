```
```cpp
int a[] = {8, 1, 6, 4, 0, 3, 9, 5};
quicksort(a, a + 7);

std::cout << "Array after sorting"
          << std::endl;

for (auto e : a)
  std::cout << e << " ";

std::cout << std::endl;
}
```
```

# Quicksort using std::partition

# Program 6.13: Implementing quicksort

```
```cpp
#include <algorithm>
#include <iterator>

template <typename RandomaccessIterator>
void quicksort(RandomaccessIterator begin,
               RandomaccessIterator end)
{
    if (begin != end)
    {
        RandomaccessIterator pivot =
            std::partition(begin, end, bind2nd(
                std::less<typename iterator_traits<
                T>::value_type>(), *begin));

        quicksort(begin, pivot);
        RandomaccessIterator new_pivot = begin;
        quicksort(++new_pivot, end);
    }
}
```
```

# Randomized Quicksort

So far we have assumed that all input permutations are equally likely, which is true always, hence we add randomization to quicksort. We could randomly shuffle input sequence, but randomized quicksort employs random sampling, i.e. choosing element at random, to achieve this. So instead of picking the last element of a[l] as pivot, it is picked up randomly from the sequence.

**Algorithm 71 Randomized-Partition Algorithm**

| Line | Pseudocode |
|---:|---|
| 1 | `function RANDOMIZED-PARTITION(a, l, r)` |
| 2 | `i ← random(l, r)` |
| 3 | `swap(a[p], a[l])` |
| 4 | `return PARTITION(a, l, r)` |
| 5 | `end function` |