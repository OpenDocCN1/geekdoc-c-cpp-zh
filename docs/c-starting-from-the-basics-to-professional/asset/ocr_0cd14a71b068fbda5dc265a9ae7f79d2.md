# Views

Verbosity is not the only downside of the classical iterator-pair-based algorithms. They also do not compose well. Suppose that you are given a container of Boxes called boxes and that you want to obtain pointers to all boxes in boxes that are large enough to hold some volume, required_volume. Because the output should consist of Box* pointers rather than copies of Boxes, you cannot use copy_if() as in Ex20_13. So you consult your Standard Library reference and learn that the std::transform() algorithm can convert a range of elements of one type (Box) into a range of elements of another type (Box*). But much to your surprise, you cannot find a transform_if() algorithm to transform only a subset of elements. In C++17 you therefore always needed at least two steps to accomplish such a task. Here is one option:

```
```cpp
std::vector<Box*> box_pointers;
std::transform(begin(boxes), end(boxes), back_inserter(box_pointers),
    [](Box& box) { return &box; });
std::vector<Box*> large_boxes;
std::copy_if(begin(box_pointers), end(box_pointers), back_inserter(large_boxes),
    [=](const Box* box) { return *box >= required_volume; });
```
```

You first transform all Boxes into Box* pointers, and then you copy only those that point to a Box that is large enough. Clearly this is an excessive amount of code for such a simple task. An excessive amount of code that is moreover not as performant as it should be:

+   - If most Boxes cannot hold required_volume, collecting all Box* pointers in a temporary vector first is clearly wasteful.
+   - Even though taking the address of a Box is still cheap, in general the transformation function could be arbitrarily expensive. Applying it to all elements may be inefficient then.

To address these issues, you may want to first filter out irrelevant objects, and only then transform only the few Boxes that pass the muster. To accomplish this in C++17 with algorithms, you had to resort to more advanced intermediate containers such as std::vector<std::reference_wrapper<Box>>. We won't go there now, but our point should be clear: composing algorithms quickly becomes verbose and awkward.
And these types of problems, where several algorithmic steps have to be composed, occur surprisingly often. With the range-based algorithms of C++20, you can solve them very effectively, often even in a number of different ways. The key innovation that facilitates this is a powerful new concept called views.

> **Caution** Before we introduce views it is worth noting that, contrary to what you might think at first (or at least, contrary to what we thought at first), you cannot readily solve our gather-all-pointers-to-large-enough-Boxes challenge using the projection feature of std::ranges::copy_if(). While the following expression may look perfectly reasonable, it does not compile:

```
```cpp
std::ranges::copy_if(
    boxes,
    back_inserter(large_boxes),
    [](const Box* box) { return *box >= required_volume; }, // Condition for copy_if()
    [](Box& box) { return &box; } // Projection functor
);
```
```