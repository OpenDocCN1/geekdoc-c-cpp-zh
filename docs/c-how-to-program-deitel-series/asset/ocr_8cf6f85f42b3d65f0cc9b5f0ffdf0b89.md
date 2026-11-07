The expression

```
```cpp
b.none()
```
```

returns true if one of the bits is set in bitset b.

The expressions

```
```cpp
b &= b1;
b != b1
```
```

compare the two bitsets for equality and inequality, respectively.

Each of the bitwise assignment operators &=, |= and ^= (discussed in detail in Section 22.5) can be used to combine bitsets. For example,

```
```cpp
b &= b1;
```
```

performs a bit-by-bit logical AND between bitsets b and b1. The result is stored in b. Bitwise logical OR and bitwise logical XOR are performed by

```
```cpp
b |= b1;
b ^= b2;
```
```

The expression

```
```cpp
b >>= n;
```
```

shifts the bits in bitset b right by n positions.

The expression

```
```cpp
b <<= n;
```
```

shifts the bits in bitset b left by n positions.

The expressions

```
```cpp
b.to_string()
b.to_ulong()
```
```

convert bitset b to a string and an unsigned long, respectively.

# 15.9 Wrap-Up

In this chapter, we introduced three key components of the Standard Library—containers, iterators and algorithms. You learned about the linear sequence containers, array (Chapter 7), vector, deque, forward_list and list, which all represent linear data structures. We discussed the nonlinear associative containers, set, multiset, map and multimap and their unordered versions. You also saw that the container adapters stack, queue and priority_queue can be used to restrict the operations of the sequence containers vector, deque and list for the purpose of implementing the specialized data structures represented by the container adapters. You learned the categories of iterators and that each algorithm can be used with any container that supports the minimum iterator functionality that the algorithm requires. You also learned class bitset, which makes it easy to create and manipulate bit sets as a container.

The next chapter continues our discussion of the Standard Library’s containers, iterators and algorithms with a detailed treatment of algorithms. You’ll also learn about function pointers, function objects and C++11’s new lambda expressions.