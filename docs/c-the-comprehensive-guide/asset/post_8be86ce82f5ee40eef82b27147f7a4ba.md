
your data. And if it does something harmful, such as consuming too much memory or running too long, this case must also be described in the documentation.

If you need to solve a problem that is already solved or can be easily solved with `<algorithm>` or `<numeric>` or `<ranges>`, then you should use them:

- The functions and classes are tested by many programmers and are continuously maintained.
- The algorithms and range adapters are building blocks that you can assemble into complex tasks.
- It is therefore easier to write code with building blocks.
- Code made from building blocks is easier to debug.
- Code made from modules is especially easy to verify later and better to revise.

I would like to illustrate the last three points with an example.

```cpp
// https://godbolt.org/z/jCWvTh3a
std::vector v{0,1,3,5,7,9,2,4,6,8};
bool flag = true;
for(size_t i=1; (i < v.size()) && flag; ++i) {
    flag = false;
    for(size_t j=0; (j < v.size()-i); ++j) {
        if(v[j+1] < v[j]) {
            std::swap(v[j+1], v[j]);
            flag = true;
        }
    }
}
for(int i: v) std::cout << i << ' ';
```

Listing 25.1 Something is done with the input vector—but what?

```cpp
// https://godbolt.org/z/EJT7nPPv7
std::vector v{0,1,3,5,7,9,2,4,6,8};
std::sort(v.begin(), v.end());
for(int i: v) std::cout << i << ' ';
std::cout << '\n';
// or with a range:
std::ranges::sort(v);
for(int i: v) std::cout << i << ' ';
std::cout << '\n';
```

Listing 25.2 This input vector will be sorted!

If you look at Listing 25.1 you might eventually say: “That probably implements Bubblesort.” But for Listing 25.2, you can immediately say: “That sorts.” And that’s not all: How long does it take for you to be able to say that both listings are correct? Why does Listing 25.1 sometimes have the loop `i=1; (i < v.size())` and other times `j=0; (j < v.size()-i)`? What happens with an empty vector or one with only a single element? Let me tell you: the listing is correct, and—yes—it actually implements Bubblesort. But you surely understand what I mean. It took either more time (or/and experience) to gain this certainty with Listing 25.1, or my assurance that it is a correct Bubblesort.

### 25.2 Iterators and Ranges

A detailed introduction to iterators can be found in Chapter 24, Section 24.2. How ranges and views work is detailed in Chapter 24, Section 24.1.7. Here I will summarize the essential things that are important for working with algorithms.

Every algorithm and every range adapter imposes certain requirements on the iterators or ranges it receives as parameters. Before C++20, iterator categories were important; now they have been replaced by actual concepts. Categories and iterator concepts build on each other. The rule of thumb is this: the higher the category, the more requirements for the iterator; it must support more operations.

The iterators of each container type are associated with a corresponding category. This allows you to see which containers are compatible with an algorithm. Don't forget that streams also offer iterators and can therefore work with many algorithms.

I will show you the hierarchy of iterator categories. In C++20, the names of the categories have been given the prefix *Legacy*, which I will omit here. If an algorithm requires, for example, that the iterators begin and end follow the *ForwardIterator* category, it means there may be multiple assignments `it = begin`, increment with `++it`, and read with `*it`:

- *Iterator*: only increment required; only traversed once
- *OutputIterator*: like *Iterator* and must support writing
- *InputIterator*: like *Iterator* and must support reading
- *ForwardIterator*: like *InputIterator* and must also be traversable multiple times
- *BidirectionalIterator*: like *ForwardIterator* and must be traversable backward
- *RandomAccessIterator*: like *BidirectionalIterator* and also random access
- *ContiguousIterator*: like *RandomAccessIterator* and also the elements must be contiguous in memory

Since C++20, these have been replaced by actual concepts. These also build on each other, but there are about twice as many concepts as for iterators. The most important ones correspond to the categories. For example, there is an `input_iterator` concept, which corresponds to the *InputIterator* category. I will spare you an explicit listing.

Much more important are the range concepts. These also align with the iterator categories. So there is—you guessed it—a `ranges::input_range`, which states that the range is built with an `input_iterator`. It's that simple. Almost. Because there are a handful of other range concepts that go beyond the iterator categories:

- **view**：The range is a view, so unlike containers, it can be copied efficiently.
- **borrowed_range**：The range provides iterators that remain valid even if the range becomes invalid. Note that the container to which these iterators refer must still be valid.
- **sized_range**：Can specify the number of elements.
- **common_range**：The sentinel is an iterator, begin() and end() thus have the same type. This is true for all containers and many views, but not, for example, for the take_view, drop_view, or iota_view view.
- **viewable_range**：Can be converted into a view with views::all.
- **constant_range**：The elements are not modified, similar to const_iterator.

When I list the algorithms later, I use the terms from Table 25.1. You can see which iterator requirement demands which operations. The table also provides examples of containers that meet the requirements. For example, you can see that the requirements for bidirectional iterators are met by vec, list, and set, but not by unordered_set. I have abbreviated vector as vec and unordered_set as u-set and mentioned both only as examples.

| Requirement | Abbr. | Possible Parameters | vec | list | set | u-set |
| --- | --- | --- | --- | --- | --- | --- |
| Input | in | in, fw, bi, ra, ct | Yes | Yes | Yes | Yes |
| Output | out | out, fw, bi, ra, ct | Yes | Yes | Yes | Yes |
| Forward | fw | fw, bi, ra, ct | Yes | Yes | Yes | Yes |
| Bidirectional | bi | bi, ra, ct | Yes | Yes | Yes | – |
| Random access | ra | ra, ct | Yes | – | – | – |
| Contiguous | ct | ct | Yes | – | – | – |

Table 25.1 Iterator requirements and their compatibility with example containers.

### 25.3 Iterator Adapter

Iterators are a central part of the standard library and primarily a concept. Through further abstractions, the behavior of algorithms can be modified surprisingly often using *iterator adapters* without disturbing the idea. Many of these adapters can be found in `<iterator>`. I cannot cover all possible combinations in the explanatory list about algorithms, but to give your imagination some stimulus, here are some examples:

- With a `move_iterator`, you can convert all copy operations of an algorithm into move operations.
- With `back_inserter`, you do not need a preexisting target range; instead, each copy is converted into a `push_back`.
- The same is done by `front_inserter`, but it calls `push_front`.
- Even more flexible is `inserter`, which successively calls `insert` at a specific position.
- An `ostream_iterator` makes a copy to an output in a stream.
- The same is done by `istream_iterator`, but it copies values from a stream into a container.
- `reverse_iterator` converts every `++` operation into a `--`.

### 25.4 Algorithms of the Standard Library

All algorithms, ranges, and views in the context of this chapter are function templates or classes from the `<algorithm>` and `<ranges>` headers. Some come from `<numeric>`, which I will mention separately. Typically, algorithms work together with *containers* and use *iterators* or *ranges* as means. This, in turn, results in algorithms also working with *streams*, as they also offer iterators.

The fact that all algorithms are implemented as templates means that the code of the algorithm can automatically be used by the compiler as `inline` on the spot. Unlike with object hierarchies with potentially virtual methods that prevent inlining, this provides as much performance as one can possibly get. For the algorithms of the standard library, maximum speed within the scope of their general implementation is one of the top design principles.

![](img/74416a2c3cfc2d60ea17cab4deeb9a13_798_0.png)

**Figure 25.1** The containers do not work directly with the algorithms but “communicate” with them through iterators.
