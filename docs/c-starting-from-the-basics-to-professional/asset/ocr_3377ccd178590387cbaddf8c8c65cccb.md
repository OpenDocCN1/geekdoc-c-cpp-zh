Valid ranges include containers, statically-sized arrays, strings, string views, `std::span` (see Chapter 9), and so on—basically anything that supports `begin()` and `end()`. Internally, range-based algorithms still work with iterators, but you, as the user of the library, are no longer constantly exposed to it. Which is as it should be: A good, easy-to-use API hides implementation details (such as iterators).

In §20.11A, §20.12A, §20.13B, §20.14A, and §20.15A, you can find all earlier algorithm examples, but this time expressed using range-based algorithms instead of iterator pair-based algorithms.

And frankly, if this were all ranges had to offer in C++20, we would have been over the moon already. But there is much, much more: The `<ranges>` module offers an entirely new and very powerful kind of ranges called views. Before we move on to views, though, first a quick word on an additional nice feature of many range-based algorithms, called *projection*.

> **Note**  Just like with iterators (see earlier), you have different kinds of ranges: forward ranges, bidirectional ranges, random-access ranges, and so on. Their classification mostly mirrors that of the underlying iterators. This distinction only becomes important when reading the specifications of range-based algorithms, though. `std::ranges::sort()`, for instance, only works for random-access ranges. You therefore cannot apply this range-based algorithm to, say, a `std::list`.

# Projection

Unlike their counterparts in the std namespace, many if not most `std::ranges` algorithms support an extra feature called *projection*. Suppose that you want to sort a sequence of Boxes, and that you want to sort them not by their volume but by their height. In C++17 you could accomplish this as follows:

```
std::sort(begin(boxes), end(boxes),
    [](const Box& one, const Box& other) { return one.getHeight() < other.getHeight(); });
```

In C++20, however, you can replace this with the following:

```
std::ranges::sort(boxes, std::less{}, [](const Box& box) { return box.getHeight(); });
```

Before an element is passed to the comparison function, it is first passed through a projection function. In this case, the projection function transforms all Boxes into their heights before handing them off to the generic `std::less{}` functor. The `std::less{}` functor, in other words, always receives two values of type double, blissfully unaware that we are actually sorting Boxes and not doubles.

The optional projection parameter can even be a pointer to a (parameterless) member function, or to a (public) member variable. The sheer elegance of this is best illustrated with an example:

```
std::ranges::sort(boxes, std::less{}, &Box::getHeight);
// Or std::ranges::sort(boxes, std::less{}, &Box::m_height); should m_height be public
```

Projection then happens either by invoking the given member function on each object, or by reading the value of the given member variable from each object.

² Linked list containers do provide `sort()` member functions that you can use instead.