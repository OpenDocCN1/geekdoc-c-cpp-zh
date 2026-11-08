```
timeStuff("unordered_multiset same         ", um, &same);
timeStuff("unordered_multiset scatter       ", um, &scatter);
std::unordered_multiset<int,BadHash> umb{};
timeStuff("unordered_multiset same badHash", umb, &same);
timeStuff("unordered_multiset scatter badHash", umb, &scatter);
}
```

# **Listing 24.75** Never operate unordered associative containers with a bad hash function.

The output from the preceding listing on my computer is, for example, as follows:

```
multiset                 same          ... 72 ms
multiset                 scatter       ... 66 ms
set                      same          ... 8 ms
set                      scatter       ... 74 ms
unordered_multiset       same          ... 27 ms
unordered_multiset       scatter       ... 29 ms
unordered_multiset       same badHash  ... 24 ms
unordered_multiset       scatter badHash... 255419 ms
```

I have timeStuff exemplarily provided with C++20 concepts. For Gen it is required that gen must be a function that can be called with a size_t and whose return must be an int. For Cont, the value_type must be an int.

You can make the following observations:

+   - The multiset almost doesn't care whether the elements are same or scattered.
+   - set is naturally ultrafast with same because it ignores duplicates and thus constantly holds only one element.
+   - With a reasonable hash function, it doesn't matter to unordered_multiset whether the values are the same or scattered.
+   - Only with a poor hash function like badHash does the performance catastrophically degrade when different elements are sorted into the same bucket.

Performance also heavily depends on the implementation of the compiler and the associated standard library. Here is the same program on the same machine, but compiled with a different compiler (Clang++ 9.0.0):

```
multiset                 same          ... 57 ms
multiset                 scatter       ... 49 ms
set                      same          ... 6 ms
set                      scatter       ... 71 ms
unordered_multiset       same          ... 112802 ms
```