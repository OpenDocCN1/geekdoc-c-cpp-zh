```
```cpp
template<typename List, typename NodeElement, bool ...>

class PushBackList;

// recursive case

template<typename List, typename NodeElement>
class PushBackList<List, NodeElement, false>
{
    using Head = Front<List>;
    using Tail = PopFront<List>;
    using NewTail = typename PushBackList<Tail, NodeElement, ...>::Type;

public:
    using Type = PushFront<Head, NewTail>;
};

// basic case

template<typename List, typename NodeElement>
class PushBackList<List, NodeElement, true>
{
public:
    using Type = PushFront<List, NodeElement>;
};

// generic push-back operation

template<typename List, typename NodeElement>
class PushBack : public PushBackList<List, NodeElement>
{
};

template<typename List, typename NodeElement>
using PushBack = typename PushBack<List, NodeElement>::Type;
```
```

The PushBackType template manages the recursion. In the basic case, we use PushFront to add SelfElement to the empty list, because PushFront is equivalent to pushback on an empty list. The recursive case is far more interesting: It splits the list into its first element (Head) and a typelist continuing the remaining elements (Tail). Then we element is then appended to the end of the Tail, recursively, to produce NewTail. When the recursion is over, NewTail is pushed on to the front of list to form the final list.

Let's unwrap the recursion for a simple example!

**Click here to view code image**

`PushBack<TypeList<short, int>, long>`

In our outermost step, `Head` is short and `Tail` is `TypeList<int>`. We recurse to

**Click here to view code image**

`PushBack<TypeList<int>, long>`

where Head is int and Tail is TypeList<>.

We recurse again to compute

**Click here to view code image**

`PushBack<TypeList<>, long>`

which triggers the basic case and returns `PushFront<TypeList<>, long>`, which itself evaluates to `TypeList<long>`. The recursion then unwinds, pushing the previous Head on the front of the list:

**Click here to view code image**

`PushFront<int, TypeList<long>>`

This produces `TypeList<int, long>`, the recursion unwinds again, pushing the outermost `short` onto this list:

**Click here to view code image**

`PushFront<short, TypeList<int, long>>`

This produces the final result: