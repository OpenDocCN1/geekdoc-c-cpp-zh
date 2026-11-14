
The searching and counting algorithms can be used similarly and the online manuals provide good documentation.

for_each: An STL function whose usefulness remains a mystery to us today is for_each. Its purpose is to apply a function on each element of a sequence. In C++03, we had to define a function object upfront or compose it with functors or pseudo-lambdas. A simple for-loop was easier to implement and much clearer to understand. Today we can create the function object on the fly with lambdas, but we also have a more concise range-based for-loop so the loop implementation is again simpler to write and to read. However, if you find for_each useful in some context, we do not want to discourage you. While for_each allows for modifying sequence elements according to the standard, it is still classified as non-mutable for historical reasons.

### 4.1.4.2 Modifying Sequence Operations

copy: The modifying operations have to be used with care because the modified sequence is usually only parameterized by the starting iterator. It is therefore our responsibility as programmers to make sure enough space is available. For instance, before we copy a container we can resize the target to the source's size:

```
vector<int> seq = { 3, 4, 7, 9, 2, 5, 7, 8 }, v;
v.resize(seq.size());
copy(seq.begin(), seq.end(), v.begin());
```

A nice demonstration of the iterators' flexibility is printing a sequence by means of copy:

```
copy(seq.begin(), seq.end(), ostream_iterator<int>(cout, " "));
```

The ostream_iterator builds a minimalistic iterator interface for an output stream: the ++ and * operations are void, comparison is not needed here, and an assignment of a value sends it to the referred output stream together with the delimiter.

unique is a function that is quite useful in numeric software: it removes the duplicated entries in a sequence. As a precondition the sequence must be sorted. Then unique can be used to rearrange the entries such that unique values are at the front and the replications at the end. An iterator to the first repeated entry is returned and can be used to remove the duplicates:

```
std::vector<int> seq = { 3, 4, 7, 9, 2, 5, 7, 8, 3, 4, 9 };
sort(seq.begin(), seq.end());
auto it = unique(seq.begin(), seq.end());
seq.resize(distance(seq.begin(), it));
```

If this is a frequent task, we can encapsulate the preceding operations in a generic function parameterized with a sequence/range:

```
template <typename Seq>
void make_unique_sequence(Seq& seq)
{
    using std::begin; using std::end; using std::distance;
    std::sort(begin(seq), end(seq));
    auto it = std::unique(begin(seq), end(seq));
    seq.resize(distance(begin(seq), it));
}
```

There are many more mutating sequence operations that follow the same principles.

### 4.1.4.3 Sorting Operations

The sorting functions in the standard library are quite powerful and flexible and can be used in almost all situations. Earlier implementations were based on quick sort with O(nlogn) average but quadratic worst-case complexity. Recent versions use intro-sort whose worst-case complexity is O(nlogn), too. In short, there is very little reason to bother with our own implementation.

By default, sort uses the < operator but we can customize the comparison, e.g., to sort sequences in descending order:

```
vector<int> seq = {3, 4, 7, 9, 2, 5, 7, 8, 3, 4, 3, 9};
sort(seq.begin(), seq.end(), [](int x, int y){return x > y;});
```

Lambdas come in handy again. Sequences of complex numbers cannot be sorted unless we define a comparison, for instance, by magnitude:

```
using cf = complex<float>;
vector<cf> v = {{3, 4}, {7, 9}, {2, 5}, {7, 8}};
sort(v.begin(), v.end(), [](cf x, cf y){return abs(x)<abs(y);});
```

Although not particularly meaningful here, a lexicographic order is also quickly defined with a lambda:

```
auto lex = [](cf x, cf y){return real(x)<real(y)
|| real(x)==real(y)&&imag(x)<imag(y);};
sort(v.begin(), v.end(), lex);
```

Many algorithms require a sorted sequence as a precondition as we have seen with unique. Set operations can also be performed on sorted sequences and do not necessarily need a set type.

### 4.1.4.4 Numeric Operation

The numeric operations from STL are found in header/library <numeric>. iota generates a sequence starting with a given value successively incremented by 1 for all following entries. accumulate evaluates by default the sum of a sequence and performs an arbitrary reduction when a binary function is provided by the user. inner_product by default a dot product whereby the general form allows for specifying a binary function object substituting the addition and multiplication respectively. partial_sum and adjacent_difference behave as their names suggest. The following little program shows all numeric functions at once:

```
vector<float> v = {3.1, 4.2, 7, 9.3, 2, 5, 7, 8, 3, 4},
w(10), x(10), y(10);
iota(w.begin(), w.end(), 12.1);
partial_sum(v.begin(), v.end(), x.begin());
adjacent_difference(v.begin(), v.end(), y.begin());

float alpha = inner_product(w.begin(), w.end(), v.begin(), 0.0f);
float sum_w = accumulate(w.begin(), w.end(), 0.0f);
float product_w = accumulate(w.begin(), w.end(), 1.0f,
    ([](float x, float y){return x * y;}));
```

The function iota was not part of C++03 but is integrated in the standard since C++11.

### 4.1.4.5 Complexity

Bjarne Stroustrup summarized the complexities of all STL algorithms in a concise table (Table 4-1) that we share with you.

## 4.1.5 Beyond Iterators

Iterators undoubtedly made an important contribution to modern programming in C++. Nonetheless, they are quite dangerous and lead to inelegant interfaces.

Let's start with the dangers. Iterators appear in pairs and only the programmer can assure that the two iterators used for the termination criterion really relate to each other.

This offers us an unattractive repertoire of failures:

- The end iterator comes first.
- The iterators are from different containers.
- The iterator makes larger steps (over multiple entries) and doesn't hit the end iterator.

In all these cases, the iteration can run over arbitrary memory and might only stop when the program leaves the accessible address space. A program crash is probably still our best option because we see where we failed. An execution that at some point stops the iteration has most likely already ruined a lot of data so the program can cause serious damage before ending in a crash or in an alleged success.

Similarly, STL functions on multiple containers only take a pair of iterators from one container and solely the beginning iterator from the other containers, e.g.:

```
copy(v.begin(), v.end(), w.begin());
```

### Table 4-1: Complexity of STL Algorithms

| Algorithmic Complexities | |
| :--- | :--- |
| O(1) | swap, iter_swap |
| O(log n) | lower_bound, upper_bound, equal_range, binary_search, push_heap, pop_heap |
| O(n log n) | inplace_merge, stable_partition, all sorting algorithms |
| O(n^2) | find_end, find_first_of, search, search_n |
| O(n) | All other algorithms |

From [43, page 931]

3. A pair of iterators does not necessarily represent an entire container. It can also refer to a part of a container or some more general abstraction. Considering entire containers only is already enough to demonstrate catastrophic consequences of even little errors.

Thus, it cannot be tested whether the target of the copy provides enough space and random memory can be overwritten.

Finally, the interface of iterator-based functions is not always elegant. Consider

```
x = inner_product(v.begin(), v.end(), w.begin());
```

versus

```
x = dot(v, w);
```

The example speaks for itself. Plus, the second notion allows us to check that v and w match in size.

C++17 may introduce Ranges. These are all types providing a begin() and an end function which return iterators. This includes all containers but is not limited to it. A range can also represent a sub-container, the reverse traversal of a container, or some transformed view. The ranges will trim the function interface nicely and will also allow size checks.

In the meantime, we do ourselves a favor by adding functions on top of those with an iterator interface. There is nothing wrong with using iterator-based functions on low or intermediate levels. They are excellent to provide the most general applicability. But in most cases we don't need this generality because we operate on complete containers, and size-checking functions with a concise interface allow us to write more elegant and more reliable applications. On the other hand, existing iterator-based functions can be called internally as we did for print_interval in Listing 4.2. Likewise, we could realize a concise dot function from inner_product. Thus:

### Iterator-Based Functions

If you write iterator-based functions, provide a user-friendly interface on top of them.

Final remark: This section only scratches the surface of STL and is intended as a mere appetizer.

## 4.2 Numerics

In this section we illustrate how the complex numbers and the random-number generators of C++ can be used. The header <cmath> contains a fair number of numeric functions whose usage is straightforward, not needing further illustration.

### 4.2.1 Complex Numbers

We already demonstrated how to implement a non-templated complex class in Chapter 2 and used the complex class template in Chapter 3. To not repeat the obvious again and again, we illustrate the usage with a graphical example.
