
cases, like iterator, the underlying type is not specified by the standard and is only described by its properties. You must then use the alias because you could not (portably) write the concrete type.

It is not always easy to apply the terms clearly here. For map, the term “value” is ambiguous, because it is often used like “it maps a key to a value”. But the `value_type` of map is actually defined together as `pair<key_type,mapped_type>`. Therefore, I prefer using the term “target” in that case. I strive to use the following clear terms in the book:

- *Value* or element of `value_type`
- *Key* of `key_type`
- *Target* of *target type* or *mapped type* for `mapped_type`

| Type Alias | Meaning | `vector<int>` | `set<int>` | `map<int, string>` |
|---|---|---|---|---|
| `value_type` | Elements of the container | `int` | `int` | `pair<const int, string>` |
| `key_type` | Key part of the elements | – | `int` | `int` |
| `mapped_type` | Mapped part of the elements | – | – | `string` |
| `size_type` | Size or index | `size_t` | `size_t` | `size_t` |
| `reference` | Reference to element | `int&` | `int&` | `pair<const int, string>&` |
| `iterator` | Iterator in the *modifiable* container | Yes | Yes | Yes |
| `const_iterator` | Iterator in the *immutable* container | Yes | Yes | Yes |
| `reverse_iterator` | Reverse iterator | Yes | Yes | Yes |

**Table 24.3** Overview of the most important type aliases of containers.

Even if you forgo `auto`, you can use these aliases to write code that looks the same for every container type or create your own templates.

```cpp
// https://godbolt.org/z/c97rq3M7
#include <vector>
#include <map>
#include <iostream>
using std::cout; using std::ostream;

template<typename K, typename T>
ostream& operator<<(ostream& os, std::pair<const K,T> value) {
    return os << '[' << value.first << ':' << value.second << ']';
}
int main() {
    {
        using Cont = std::vector<int>;
        Cont const cont{ 1, 2, 3, 4, 5, 6 };
        Cont::size_type sz = cont.size();
        cout << "size=" << sz << " content= ";
        for(Cont::const_iterator it = cont.begin(); it != cont.end(); ++it)
            cout << *it << ' ';
        cout << '\n';
    }
    {
        using Cont = std::map<int,char>;
        Cont const cont{ {1,'a'}, {2,'b'}, {3,'c'}, {4,'d'}, {5,'e'}, {6,'f'} };
        Cont::size_type sz = cont.size();
        cout << "size=" << sz << " content= ";
        for(Cont::const_iterator it = cont.begin(); it != cont.end(); ++it)
            cout << *it << ' ';
        cout << '\n';
    }
}
```

**Listing 24.11** Type aliases are sometimes clearer than the concrete types.

Here I use the aliases provided by the containers `size_type` and `const_iterator`. In this simple case, `auto` would have worked, but this demonstrates the aliases.

### Interlude: “pair” and “tuple”

As shown in Table 24.3, some containers internally use `pair`. As you progress through the chapter, you will encounter several methods that also return a `pair` as a return type. This is nothing more than bundling two data types and their values together—essentially:

```cpp
// https://godbolt.org/z/xcrbVMljz
struct PairInDouble {
    int first;
    double second;
};
int main() {
    PairInDouble p{ 2, 7.123 };
}
```

What I have done here specifically for `int` and `double` is possible with `std::pair` as a template class for any types. You can access the first element with `first` and the second with `second`.

A generalization of pair for any number of elements is tuple. For example, you use `get<3>(t)` to access the fourth element of `t`.

That should suffice for a discussion of pair and tuple for this chapter. A complete discussion of these two data types can be found in Chapter 28, Section 28.1.

## 24.6 The Sequential Container Classes

Let’s walk through the sequential container classes (see Table 24.4):

- **`array<ElementType,Size>`**
  A fixed number of elements is stored here. Adding and removing is only possible by overwriting. The elements are stored directly next to each other in memory. Therefore, array is suitable for both a few huge and many tiny element types, as it has virtually no memory overhead.

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_671_0.png)

  **Figure 24.2** An “array” can neither grow nor shrink, but it is compact.

- **`vector<ElementType>`**
  This all-rounder grows automatically. You can insert anywhere, but efficiently only at the back end.

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_671_1.png)

  **Figure 24.3** Schematic representation of a “vector”.

  Reading the elements is done sequentially forwards, backward, or randomly by index. Also, vector stores its elements directly next to each other in memory, making it practical for both a few large and many tiny elements. Optimally used, it has virtually no memory overhead; in nonoptimal cases, it is still acceptable as it does not fragment memory.

- **`deque<ElementType>`**
  You can easily add elements to the end of a vector, but less easily to the beginning, as all existing elements must be shifted one place to the right. The *double-ended queue* deque is suitable for quickly adding elements at both ends. As a disadvantage, it does not store its elements directly next to each other, but still usually more compactly than list. If possible, prefer vector.

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_672_0.png)

  **Figure 24.4** A “deque” can be extended at both ends, but the elements are not contiguous in memory.

- **`list<ElementType>`**
  The list is simpler than a vector and is very well suited for frequent insertions in the middle. However, the elements are not contiguous in memory but are internally linked. You do not have index access available. If you want to iterate over ranges, it is fast.

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_672_1.png)

  **Figure 24.5** A “list” can be traversed forwards and backward. Insertion is easy.

- **`forward_list<ElementType>`**
  This exotic type mimics the fundamental structure of a linked list from C and therefore requires minimal additional resources. However, it has a slightly different interface than all other containers. Even insertion works somewhat differently. You can only iterate forwards. Both list and forward_list are specialists in *splicing*—that is, transferring some consecutive or all elements from one list to another.

  ![](img/74416a2c3cfc2d60ea17cab4deeb9a13_672_2.png)

  **Figure 24.6** Elements of the “forward_list” only know their successor.

You use `array` when you know at compile time how many elements the container should hold, `vector`, on the other hand, has a dynamic size; you can add elements to it or remove them.

Table 24.5 lists the main properties that distinguish the sequence-based containers from each other. The following notes apply to the entries marked with an asterisk *:

- **Key type**
  You can only use a `size_t` for operator `[]` and `at`. `Key` is not quite the right term here, because shifting elements changes the association of the keys to the container elements. However, I include this property here to compare it with associative containers.

- **Overhead per element of vector**
  In the optimal case, vector has virtually no additional memory consumption other than that of the elements it manages. If you know in advance that you will store 1,000 elements, you can prepare the vector to exactly this size with `reserve(1000)` and then add elements. You will achieve optimal performance in terms of time and memory consumption. If you do not reserve a size in advance, the vector will be slightly larger than needed, and new space will have to be allocated from time to time when adding elements. However, the internal algorithms ensure that, on average, you spend at most twice as much time or memory as without the advance reservation.

- **Efficient insertion into the `forward_list`**
  Unlike all other containers, when you insert into the `forward_list`, you do not insert at the position you indicate, but rather one element after. Why this is the case will be shown later in an example. For this reason, this container, unlike any other (except array), does not have `insert` but instead has `insert_after`. This inconvenience is due to the desire to use as little memory per element as possible.

- **Splicing of list and `forward_list`**
  These two containers have the unique property compared to all others that you can merge two containers of the same type extremely quickly. Making one out of two does not cost a single copy operation of the elements contained within these two, and the administrative information to be changed is independent of the number of elements in the lists.

- **Memory layout**
  On many occasions, the elements of the container need to be packed closely together to work with them optimally. For example, when writing to the hard drive, it is advantageous to pass all the data to be written to the operating system as one large block. And other C functions also struggle with complex C++ data structures. They require a starting point in memory and a length (hello, `span`!). Of all the containers, only array and vector store their elements in such a way that this type of data exchange works, with array being the only container that can use only the stack and does not need to request heap space with `new`.
