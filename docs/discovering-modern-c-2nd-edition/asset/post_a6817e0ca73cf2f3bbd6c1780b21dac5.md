
cout << "The first value in range is " << *it << '\n';
}

C++11. Or we create the predicate in place:

Click here to view code image

```
auto it = find_if(begin(seq), end(seq),
    [](int i) { return i > 4 && i < 7; } );
```

The searching and counting algorithms can be used similarly and the online manuals provide good documentation.

### 4.1.4.2 Modifying Sequence Operations

copy: The modifying operations have to be used with care because the modified sequence is usually only parameterized by the starting iterator. It is therefore our responsibility as programmers to make sure enough space is available. For instance, before we copy a container we can resize the target to the source's size:

Click here to view code image

```
vector<int> seq = {3, 4, 7, 9, 2, 5, 7, 8}, v;
v.resize(seq.size());
copy(begin(seq), end(seq), begin(v));
```

A nice demonstration of the iterators' flexibility is printing a sequence by means of copy:

Click here to view code image

```
copy(begin(seq), end(seq), ostream_iterator<int>(cout, ",
   "));
```

The ostream_iterator builds a minimalistic iterator interface for an output stream: the ++ and * operations are void, comparison is not needed here, and an assignment of a value sends it to the referred output stream together with the delimiter.

unique is a function that is quite useful in numeric software: it removes the duplicated entries in a sequence. As a precondition the sequence must be sorted. Then unique can be used to rearrange the entries such that unique values are at the front and the replications at the end. An iterator to the first repeated entry is returned and can be used to remove the duplicates:

Click here to view code image

```
std::vector<int> seq = {3, 4, 7, 9, 2, 5, 7, 8, 3, 4, 3, 9};
sort(begin(seq), end(seq));
auto it= unique(begin(seq), end(seq));
resize(distance(begin(seq), it));
```

If this is a frequent task, we can encapsulate the preceding operations in a generic function parameterized with a sequence/range:

Click here to view code image

```
template <typename Seq>
void make_unique_sequence(Seq& seq)
{
    using std::begin; using std::end; using std::distance;
    std::sort(begin(seq), end(seq));
    auto it= std::unique(begin(seq), end(seq));
    seq.resize(distance(begin(seq), it));
}
```

There are many more mutating sequence operations that follow the same principles.

### 4.1.4.3 Sorting Operations

The sorting functions in the standard library are quite powerful and flexible and can be used in almost all situations. Earlier implementations were based on quick sort with O(n log n) average but quadratic worst-case complexity.2 Recent versions use intro-sort whose worst-case complexity is O(n log n), too. In short, there is very little reason to bother with our own implementation. By default, sort uses operator< but we can customize the comparison, e.g., to sort sequences in descending order:

2. Lower worst-case complexity was already provided at that time by stable_sort and partial_sort.

Click here to view code image

```
vector<int> seq = {3, 4, 7, 9, 2, 5, 7, 8, 3, 4, 3, 9};
sort(begin(seq), end(seq), [](int x, int y){return x > y;});
```

Lambdas come in handy again. Sequences of complex numbers cannot be sorted unless we define a comparison, for instance, by magnitude:

Click here to view code image

```
using cf= complex<float>;
vector<cf> v = ({3, 4}, {7, 9}, {2, 5}, {7, 8});
sort(begin(v), end(v), [](cf x, cf y){return abs (x)
<abs (y);});
```

Although not particularly meaningful here, a lexicographic order is also quickly defined with a lambda:

Click here to view code image

```
auto lex= [](cf x, cf y){return real(x)<real(y)
|| real(x)==real(y)&&imag(x)
<imag(y);};
sort(begin(v), end(v), lex);
```

Many algorithms require a sorted sequence as a precondition as seen with unique. Set operations can also be performed on sorted sequences and don’t necessarily need a set type.

### 4.1.4.4 Numeric Operations

The numeric operations from STL are found in header/library <numeric>. iota generates a sequence starting with a given value successively incremented by 1 for all following entries. accumulate evaluates by default the sum of a sequence and performs an arbitrary reduction when a binary function is provided by the user. inner_product performs by default a dot product whereby the general form allows for specifying a binary function object substituting the addition and multiplication, respectively. partial_sum and adjacent_difference behave as their names suggest. The following little program shows some fundamental numeric functions:

Click here to view code image

```
vector<float> v= {3.1, 4.2, 7, 9.3, 2, 5, 7, 8, 3, 4},
w(10), x(10), y(10);
iota(begin(w), end(w), 12.1);
partial_sum (begin (v), end(v), begin(x));
adjacent_difference(begin(v), end(v), begin(y));
float alpha= inner_product(begin(w), end(w), begin(v), 0.0f);
float sum_w= accumulate(begin(w), end(w), 0.0f),
product_w= accumulate(begin(w), end(w), 1.0f,
[] (float x, float y){return x *
y});
```

The function iota was not part of C++03 but is integrated in the standard since C++11.

### 4.1.4.5 Complexity

Bjarne Stroustrup summarized the complexities of all STL algorithms in a concise table (Table 4–1) that he graciously allowed us to share.

### Table 4–1: Complexity of STL Algorithms

| Complexity | Algorithms |
| :--- | :--- |
| O(1) | swap, iter_swap |
| O(log n) | lower_bound, upper_bound, equal_range, binary_search, push_heap, pop_heap |
| O(n log n) | inplace_merge, stable_partition, all sorting algorithms |
| O(n²) | find_end, find_first_of, search, search_n |
| O(n) | All other algorithms |

From [62, page 931]

## 4.1.5 Ranges

### 4.1.5.1 Risks and Limitations of Iterators

C++20 Iterators undoubtedly made an important contribution to modern programming in C++. Nonetheless, they can be quite dangerous and lead to inelegant interfaces. Let's start with the dangers. Iterators often appear in pairs and only the programmer can assure that the two iterators really relate to each other. This offers us an unattractive repertoire of mistakes:

- The end iterator comes first.
- The iterators are from different containers.
- The iterator makes larger steps (over multiple entries) and doesn’t hit the end iterator.

In all these cases, the iteration can run over arbitrary memory and might only stop when the program leaves the accessible address space. A program crash is probably still our best option because we see where we failed. An execution that at some point stops the iteration has most likely already ruined a lot of data so the program can cause serious damage before ending in a crash or in an alleged success.

Similarly, most STL functions on multiple containers only take a pair of iterators from one container³ and solely the beginning iterator from the other containers, e.g.:

3. A pair of iterators does not necessarily represent an entire container. It can also refer to a part of a container or some more general abstraction. Considering entire containers only is already enough to demonstrate catastrophic consequences of even little errors.

Click here to view code image

```
copy(begin(v), end(v), begin(w));
```

Thus, it cannot be tested whether the target of the copy provides enough space and random memory can be overwritten. Finally, the interface of iterator-based functions is not always elegant. Compare:

Click here to view code image

```
x = inner_product(begin(v), end(v), begin(w));
```

with:

```
x = dot(v, w);
```

The example speaks for itself. Plus, the second notion allows us to check that v and w match in size. For these reasons we recommend:

### Iterator-Based Functions

If you write iterator-based functions, provide a user-friendly interface on top of them.

How? This will be explained in the following.

### 4.1.5.2 New Function Interfaces

=> c++20/ranges_copy.cpp

C++20 has introduced Ranges. Unfortunately, the compiler support at the time of writing wasn’t satisfactory. Therefore, we investigated this interesting feature partly with Eric Niebler’s prototype library. On GitHub you’ll for most examples find both the standard and the prototype versions. Our sources contain a lot of explicit namespace qualification due to ambiguities with std. We are optimistic that this will be less of a burden when ranges are fully integrated into the compilers’ standard libraries. When trying the following snippets with standard ranges, you should add using namespace std::ranges; to your programs. Despite these details, we hope that this section helps you to get started with this really useful feature.

Loosely spoken: ranges are all types that we can iterate over with a begin and an end function. This allows us to reduce the number of arguments in many functions by using ranges instead of iterators. We can, for instance, reduce the number of arguments in the previously mentioned copy function:

Click here to view code image

```
vector<int> u{3, 2, 6, 7, 4}, v(5), w;
ranges::copy(u, begin(v));
```

The source is passed directly as the first argument and from the target we take the begin iterator. The interface is apparently more concise than before. It is also less prone to the errors from the preceding section. The iterator-based interface is only preferable when the source’s starting and terminating iterators are separately provided in the according context. But this is quite rare; in most cases they are given by calling begin and end on the same container (or other range) so that the new interface covers the vast majority of applications.

One risk still exists with this new interface: writing past the end of available space in the target. Better would be a call like:

```
copy(u, w);
```
