
I go into the details of the ranges library in Chapter 25.

![](img/290cf954dfcaad53865de6b98cca8e6f_1100_0.png)

**Figure 24.1** Containers and views are ranges, adapters generate views from them that can be further processed.

## 24.1.8 Algorithms

The original STL also includes the algorithms that operate on the containers. These are a collection of functions that are there to support the methods of the containers. However, as parameters, they do not receive a container, but always *pairs of iterators*. Since C++20, many algorithms are also defined in std::ranges and operate on ranges. This achieves two effects:

- Algorithms always work on *subranges* of containers.
- Algorithms work almost independently of the container type on iterators of all containers.

The latter is only true in principle. There are often constraining conditions. For example, you can apply sort(begin, end) to an iterator pair of a vector, but sort() does not work on list iterators. They do not allow random access. To distinguish, containers and iterators are divided into groups. If you want to work with a free function for iterators, check the following section using Table 24.2 to see if the category of the iterator matches.

## 24.2 Iterator Basics

Iterators fall into different categories regarding the operations they support. This is a simple linear hierarchy: the higher the category in this hierarchy, the more operations that iterators of that category support.

The exception is the output iterators, which require additional properties but do not necessarily bring any of the other categories with them.

| Iterator Category | Provider |
| --- | --- |
| Contiguous | vector, string, array |
| Random access | deque |
| Bidirectional | list, [multi]set, multiset, [multi]map |
| Forward | forward_list, unordered_[multi]{map|set} |
| Output | ostream, inserter |
| Input | istream |

**Table 24.2** Which containers and streams provide iterators of which category?

There are some distinctions to make between different categories of iterators, as follows:

- *All iterators*: All iterators can be copied and assigned, meaning you can do it(other) and it = other. Every iterator also can be incremented with ++.

- *Output iterators*: These allow you to assign to their dereferenced element with *it = ... .

- *Input iterators*: These support comparison with it == ij and it != ij and can return the value of the dereferenced element with *it and it->, ...

- *Forward iterators*: These are input iterators that in addition guarantee that you can traverse a sequence multiple times if the underlying container does not change. This is the multipass guarantee. What means becomes clear when you consider what happens with iterators that input iterators but not forward iterators. This is the case, for example, when an iterator reads from cin—which changes the state of cin upon input and is therefore certainly not multipass capable.

- *Bidirectional iterators*: These are forward iterators, but can also be decremented with --it and it--.

- *Random access iterators*: Random access iterators are bidirectional and support addition +=/-= with integers, as well as comparisons with >, <, >=, <=. The combination of addition and dereferencing also implies that dereferencing with an offset it[...] is supported.

- *Contiguous iterators*: Contiguous iterators are random access and guarantee that the elements are arranged contiguously in memory. For example, you can pass a block of elements to a C function by memory address.

In Table 24.2, you can see which iterator categories are provided by which containers or streams.

In the ranges library, there is a corresponding concept for each of these iterator categories. The forward_iterator corresponds to the ranges::forward_range range concept and so on.

### 24.2.1 Iterators from Containers

Each container has two different iterator types that you can obtain using various methods:

- *Iterator*: This allows you to modify the value in the container upon dereferencing—for example, *it = 12;

- *const_iterator*: This allows read-only access to the container.

Depending on what you intend to do with the iterator, there are two variants of begin() and end(). For the container, they would look like:

```cpp
struct Container {
    iterator begin();
    iterator end();
    const_iterator begin() const;
    const_iterator end() const;
};
```

If you use the free functions begin() and end(), you will get a `const_iterator` if the container is const, and an `iterator` if it is mutable. Thanks to auto, you don't need to type it. For example, data.begin() + 2 refers to the 3rd element.

## 24.2.2 More Functionality with Iterators

Many standard algorithms take an index as a parameter. For example, in the next listing, see how you can use an ostream_iterator output iterator to out the contents of any container to cout.

```cpp
#include <vector>
#include <iostream>
#include <iterator>
#include <algorithm>

int main() {
    std::vector<int> data = { 1, 2, 3, 7, 9, 10 };
    std::copy(data.begin(), data.end(), std::ostream_iterator<int>(std::cout, " "));
    return 0;
}
```
