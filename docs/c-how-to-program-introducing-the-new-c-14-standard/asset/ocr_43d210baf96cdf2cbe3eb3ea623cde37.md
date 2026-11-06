# `C++11: any_of` *Algorithm*

Line 81 uses the `any_of` algorithm to determine whether the *unary predicate function* (the lambda stored in `isGreaterThan10`) returns `true` for *at least one* of the elements in the range from `a.cbegin()` up to, but *not including*, `a.cend()`. Algorithm `any_of` requires its two iterator arguments to be at least *input iterators*.

# `C++11: none_of` *Algorithm*

Line 89 uses the `none_of` algorithm to determine whether the *unary predicate function* (the lambda stored in `isGreaterThan10`) returns `false` for *all* of the elements in the range from `a.cbegin()` up to, but *not including*, `a.cend()`. Algorithm `none_of` requires its two iterator arguments to be at least *input iterators*.

# `C++11: find_if_not` *Algorithm*