R1 and R2 are the types of the ranges passed to `mismatch`. Based on the declarations of a1 and a3, the algorithm’s return type in line 33 is

```
std::ranges::mismatch_result<borrowed_iterator_t<array<int, 10>>,
                             borrowed_iterator_t<array<int, 10>>>
```

As you can see, it’s much more convenient to simply say `auto` and let the compiler determine this complex declaration for you. Class-template argument deduction (CTAD) also could be used to infer the type arguments. So, we could declare the variable’s type simply as `std::ranges::mismatch_result`.

# lexicographical_compare Algorithm

The C++20 `std::ranges::lexicographical_compare` algorithm (lines 41–42) compares the contents of two input_ranges—in this case, strings. Like containers, strings have iterators that enable them to be treated as C++20 ranges. While iterating through the ranges, if there is a mismatch between their corresponding elements and the element in the first range is less than the corresponding element in the second range, the algorithm returns true. Otherwise, the algorithm returns false. This algorithm can be used to arrange sequences lexicographically. It also can receive a binary predicate function that returns true if its first argument should be considered less than its second. Of course, strings are comparable with the relational and equality operators, so line 42’s call to function lexicographical_compare could be replaced with s1 < s2. This algorithm is primarily intended for use with ranges that cannot be compared directly with one another, such as two std::spans.

```
37        std::string s1{"HELLO"};
38        std::string s2{"BYE BYE"};

40        // compare lexicographical comparison of s1 and s2
41        std::cout << std::format("{} < {}: {}\n", s1, s2,
42             std::ranges::lexicographical_compare(s1, s2));
43    }
```

```
"HELLO" < "BYE BYE": false
```

# 14.4.3 remove, remove_if, remove_copy and remove_copy_if

Figure 14.4 demonstrates removing values from a sequence with algorithms `remove`, `remove_if`, `remove_copy` and `remove_copy_if` from C++20’s `std::ranges` namespace. Line 9 creates a `vector<int>` that we’ll use to initialize other vectors in this example.