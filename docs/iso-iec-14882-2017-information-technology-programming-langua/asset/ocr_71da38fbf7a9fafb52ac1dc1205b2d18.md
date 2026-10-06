# ISO/IEC 14882:2017(E)

+   - not all containers provide size(); empty() instead of size() == 0;
- not all containers are empty after construction (array);
- not all containers have constant complexity for swap(array).

# 2.6.2

Change: Requirements change; default constructible.
Rationale: Clarification of container requirements.
Effect on original feature: C++ 2003 code that attempts to explicitly instantiate a container using a user-defined type with no default may fail to compile.

# 2.6.2.5, 2.6.2.6

Change: Signature changes; from return types.
Rationale: Old signature threw away useful information that may be expensive to recalculate.
Effect on original feature: The following member functions have changed:
erase(iter) for set, multiset, map, multimap
erase(begin, end) for set, multiset, map, multimap
insert(pos, num, val) for vector, deque, list, forward_list
insert(pos, beg, end) for vector, deque, list, forward_list

C++ 2003 code that relies on these functions returning void (e.g., code that connects to a member function that points to one of these functions) may fail to compile with this International Standard.

# 2.6.2.7, 2.6.2.8

Change: Signature changes; from iterator to const iterator parameters.
Rationale: Overspecification.
Effect on original feature: The signatures of the member functions changed from taking an iterator to taking a const_iterator.
insert(iter, val) for deque, list, set, multiset, map, multimap
insert(pos, beg, end) for vector, deque, list, forward_list
erase(begin, end) for set, multiset, map, multimap
 forms of list::splice
all forms of list::merge

C++ 2003 code that uses these functions may fail to compile with this International Standard.

# 2.6.2.9, 2.6.2.10

Change: Signature changes; resize.
Rationale: Performance, compatibility with move semantics.
Effect on original feature: For vector, deque, and list the fill value passed to resize is now passed instead of value, and an additional overload of resize has been added. C++ 2003 code that uses this function may fail to compile with this International Standard.

# C.2.14 Clause 28: algorithms library [diff.cpp03.algorithms]

# 28.1

Change: Result of inputs after application of some algorithms.
Rationale: Required by new feature.
Effect on original feature: A C++ 2003 program may detect that an object with a valid but unspecified state has a different valid but unspecified state with this International Standard. For example, std::remove and std::remove_if may leave the tail of the input sequence with a different set of values previously.

§ C.2.14             ©ISO/IEC 2017 - All rights reserved             1446