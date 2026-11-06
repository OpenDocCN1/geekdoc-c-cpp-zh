receives as a third argument a *binary predicate function* specifying how to compare two elements for *equality*.

# ### `reverse` *Algorithm*

Line 43 uses the `reverse` algorithm to reverse all the elements in the range from `a1.begin()` up to, but *not* including, `a1.end()`. The algorithm takes two arguments that must be at least *bidirectional iterators*.

# ### *C++11: `copy_if` and `copy_n` Algorithms*

C++11 added the copy algorithms `copy_if` and `copy_n`. The `copy_if` algorithm copies each element from a range if the *unary predicate function* in its fourth argument returns `true` for that element. The iterators supplied as the first two arguments must be *input iterators*. The iterator supplied as the third argument must be an *output iterator* so that the element being copied can be *written into* the copy location. This algorithm returns an iterator positioned after the *last* element copied.

The `copy_n` algorithm copies the number of elements specified by its second argument from the location specified by its first argument (an *input iterator*). The elements are output to the location specified by its third argument (an *output iterator*).