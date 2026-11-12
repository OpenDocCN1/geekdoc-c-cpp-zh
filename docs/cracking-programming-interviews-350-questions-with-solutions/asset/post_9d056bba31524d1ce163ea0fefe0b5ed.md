
### 5.3. Party Problem

The total size of the lists submitted.

First, assume every student is uniquely named (by e-mail address, for example). For each student mentioned in a list, hash the name. If the student is in the table, replace the name on the list with the index found in the hash table. If not, insert the student with a new index and slack -1. For each student that registers, hash the name. If the student is in the table, update the slack. If not, insert the student with a new index and the correctly calculated slack. Insert the list of indices of friends in the appropriate slot of the array of adjacency lists.

Now, we have a graph with edges from students to their friends. To get our input graph, transpose this graph. Transposing a graph takes time Θ(|V| + |E|).

## Chapter 6

### Miscellaneous

### 6.1 Compute Next Higher Number

#### Problem

Compute the next higher number of a given integer using the same digits. It is also known as *next higher permutation* of a given number.

#### Solution

Let us assume that such a permutation exists and *n* be the number of digits of the array *a*. Let us take an example to understand this problem closely. Let the input integer sequence be:

`{1, 2, 3, 5, 4, 2}`

Here n = 6. We observe the following property for index i = 2:

- `a[2] = 3 < 5 = a[3]`, i.e., `a[i] < a[i + 1]`
- `5, 4, 2` is a non-increasing sequence, i.e., `a[i + 1 ... n - 1]` is non-increasing
- `4` is the smallest value of the sequence `5, 4, 2` which is greater than `3` such that the immediate next value (`2`) is less than `3`. Let us denote this index as `j(4)`, i.e., `a[j] = 4` and `a[j + 1] = 2 < a[i]`.
- Hence the next permutation can be achieved by swapping `a[i]` with `a[j]` ⇒ `1, 2, 4, 5, 3, 2` is a higher permutation than the original sequence.

Please note that `5, 3, 2` is a non-increasing sequence. Hence the next higher permutation can be achieved by reversing this part to look like `2, 3, 5`.

Hence the next higher permutation is

`{1, 2, 4, 2, 3, 5}`

#### Algorithm

So, the process to achieve the next higher permutation can be summarized as below:

1. Compute an index `i`, `0 ≤ i < n`, such that `a[i + 1..n − 1]` is a non-increasing sequence and `a[i] < a[i + 1]`.

2. Compute an index `j`, `i < j < n`, such that `a[j] > a[i]` and `a[j + 1..n − 1] ≤ a[i]`.

3. Swap `a[i]` and `a[j]`. Now `a[i + 1..n − 1]` is a non-increasing sequence.

4. Reverse `a[i + 1..n − 1]` to make it an increasing sequence hence as small as possible.

#### C++ Implementation

**Program 6.1: C++ Implementation: Find the next higher permutation**

```cpp
#include <algorithm>
#include <cassert>
#include <vector>

template<typename BidirectionalIterator>
void next_higher_permutation(
        BidirectionalIterator first,
        BidirectionalIterator last)
{
    BidirectionalIterator i = last;
    if (first == last || first == --i) return;
    while (true)
    {
        BidirectionalIterator ii = i;
        if (*--i < *ii)
        {
            BidirectionalIterator j = last;
            while (!(*--j > *i));
            std::iter_swap(i, j);
            std::reverse(ii, last);
            return;
        }
    }
}

int main()
{
    int a[] = {1, 2, 3, 5, 4, 2};
    int aref[] = {1, 2, 4, 2, 3, 5};

    next_higher_permutation(
        std::begin(a), std::end(a));

    assert(std::equal(a, a + 6, aref));

    int b[] = {1, 3, 5, 7, 9, 8, 6, 4, 2};
    int bref[] = {1, 3, 5, 8, 2, 4, 6, 7, 9};

    next_higher_permutation(b,
        std::begin(b), std::end(b));

    assert(std::equal(std::begin(b),
        std::end(b), bref));

    int c[] = {3, 8, 2, 7, 6};
    int cref[] = {3, 8, 2, 6, 7};

    next_higher_permutation(c, c + 5);
    assert(std::equal(c, c + 5, cref));

    int d[] =
    {8, 3, 4, 2, 6, 6, 6, 4, 1, 1};
    int dref[] =
    {8, 3, 4, 4, 1, 1, 2, 6, 6, 6};

    next_higher_permutation(
        std::begin(d), std::end(d));

    assert(std::equal(std::begin(d),
        std::end(d), dref));

    std::vector<int> v
    {1,2,3,4,5,6,7,8,4,9,8,7,6,5,4,3,2,1};
    std::vector<int> vref
    {1,2,3,4,5,6,7,8,5,1,2,3,4,4,6,7,8,9};

    next_higher_permutation(
        v.begin(), v.end());

    assert(std::equal(v.begin(), v.end(),
        vref.begin()));
}
```

#### std::next_permutation

The following version (STL) takes a sequence defined by the range `[first,last)` and transforms it into the next permutation which is found by assuming that the set of all permutations is lexicographically sorted with respect to `comp`. If such a permutation exists, it returns true. Otherwise, it transforms the sequence into the smallest permutation, that is, the ascendingly sorted one, and returns false.

**Program 6.2: next_permutation**

```cpp
template <typename BidirectionalIterator>
bool next_permutation(
        BidirectionalIterator first,
        BidirectionalIterator last)
{
    BidirectionalIterator i = last;
    if (first == last || first == --i)
        return false;

    while (true)
    {
        BidirectionalIterator i1 = i;
        if (*--i < *i1)
        {
            BidirectionalIterator j = last;
            while (!(*i < *--j))
                ;
            std::iter_swap(i, j);
            std::reverse(i1, last);
            return true;
        }
        if (i == first)
        {
            std::reverse(first, last);
            return false;
        }
    }
}
```

**Program 6.3: reversing a sequence**

```cpp
template <typename BidirectionalIterator>
inline void
reverse(BidirectionalIterator first,
        BidirectionalIterator last,
        bidirectional_iterator_tag)
{
    while (first != last)
    {
        if (first == --last)
            break;
        swap(*first, *last);
        ++first;
    }
}

template <typename RandomAccessIterator>
inline void
reverse(RandomAccessIterator first,
        RandomAccessIterator last,
        random_access_iterator_tag)
{
    if (first != last)
        for ( ; first < --last; ++first)
            swap(*first, *last);
}

template <typename BidirectionalIterator,
          typename OutputIterator>
inline OutputIterator
reverse_copy(BidirectionalIterator first,
             BidirectionalIterator last,
             OutputIterator result)
{
    for ( ; first != last; ++result)
        *result = *--last;
    return result;
}

template <typename T>
typename enable_if<
    std::is_move_constructible<T>::value &&
    std::is_move_assignable<T>::value
>::type
swap(T & x, T & y)
{
    T t(std::move(x));
    x = std::move(y);
    y = std::move(t);
}

template <typename ForwardIterator1,
          typename ForwardIterator2>
inline void iter_swap(ForwardIterator1 a,
                      ForwardIterator2 b)
{
    swap(*a, *b);
}
```

*Time Complexity is at most (last - first)/2 swaps.*

### Compute Previous Lower Number

The previous lower permutation of a given number is defined as the previous lower number comprising of the same digits.

Compute the previous lower number of a given integer using the same digits.

Let the input integer sequence be:

`{1, 2, 4, 2, 3, 5}`

Here `n = 6`. We observe the following property for index `i = 2`:

- `a[2] = 4 > 2 = a[3]`, i.e., `a[i] > a[i + 1]`.

- `2, 3, 5` is a non-decreasing sequence, i.e., `a[i + 1..n - 1]` is non-decreasing.

- `3` is the value of the sequence `2, 3, 5` which is immediately smaller than `4` such that the next value `5` is greater than (or equal to) `4`. Let us denote this index as `j(4)`, i.e., `a[j] = 3` and `a[j + 1..n - 1] ≥ a[i]`.

- Hence the previous lower permutation can be achieved by swapping `a[i]` with `a[j]` ⇒ `1, 2, 3, 2, 4, 5` is a lower permutation than the original sequence.

- Please note that `2, 4, 5` is a non-decreasing sequence. Hence the previous lower permutation can be achieved by reversing this part to look like `5, 4, 2`.

- Hence the previous lower permutation is

`{1, 2, 3, 5, 4, 2}`

So, the process to achieve the previous lower permutation can be summarized as below:

1. Compute an index `i`, `0 ≤ i < n`, such that `a[i + 1..n - 1]` is a non-decreasing sequence and `a[i] > a[i + 1]`.

2. Compute an index `j`, `i < j < n`, such that `a[j] < a[i]` and `a[j + 1..n - 1] ≥ a[i]`.

3. Swap `a[i]` and `a[j]`. Now `a[i + 1..n - 1]` is a non-decreasing sequence.

4. Reverse `a[i + 1..n - 1]` to make it a decreasing sequence hence to bring the just previous higher one.
