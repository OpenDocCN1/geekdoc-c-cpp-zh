4 In C++11, the return type has to be declared as -> decltype(makeTuple(get<Indices>(t)...)).

5 In C++11, the return type of splat() has to be declared as -> decltype(return-expression).

6 Note that the resulting order depends on the platform-specific size. For example, the size of a double might be less, the same, or greater than the size of a long long.

7 In C++11, the return type of sort() has to be declared as -> decltype(return-expression).

8 Another practical impact of this change is that the elements of the tuple will end up being stored in reverse order, because base classes are typically stored before members.

9 It would be more intuitive to simply use the index of the tuple element rather than its height. However, that information is not readily available in Tuple, because a given tuple may appear both as a standalone tuple and as the tail of another tuple. A given Tuple does know, however, how many elements are in its own tail.

10 Thanks to Louis Dionne for pointing out the features described in this section.

11 The prefix 0b for binary literals and the single quote character to separate digits are supported since C++14.