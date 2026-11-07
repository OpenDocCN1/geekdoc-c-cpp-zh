```
```cpp
int main() {
    std::array a1{1, 3, 5, 7, 9, 1, 3, 5, 7, 9};
    std::ostream_iterator<int> output(std::cout, " ");

    std::cout << "array a1 contains: ";
    std::ranges::copy(a1, output);
}
```
```

```
```text
array a1 contains: 1 3 5 7 9 1 3 5 7 9
```
```

**Fig. 14.10** | Algorithms inplace_merge, unique_copy and reverse_copy. (Part 2 of 2.)

# inplace_merge Algorithm

Line 18 calls the C++20 `std::ranges::inplace_merge` algorithm to merge two sorted ranges of elements in its **bidirectional_range** argument. This example processes the range a1 (the first argument), merging the elements from a1.begin() up to, but not including, a1.begin() + 5 (the second argument) with the elements starting from a1.begin() + 5 (the second argument) up to, but not including, the end of the range. You also can pass a **binary predicate function** that compares elements in the two subranges and returns true if the first should be considered less than the second.

```
```cpp
// merge first half of a1 with second half of a1 such that
// a1 contains sorted set of elements after merge
std::ranges::inplace_merge(a1, a1.begin() + 5);
std::cout << "\nAfter inplace_merge, a1 contains: ";
std::ranges::copy(a1, output);
```
```

```
```text
After inplace_merge, a1 contains: 1 1 3 3 5 5 7 7 9 9
```
```

# unique_copy Algorithm

Line 24 calls the C++20 `std::ranges::unique_copy` algorithm to copy the unique elements in its first argument’s sorted **input_range**—duplicates are ignored. The output iterator supplied as the second argument specifies where to place the copied elements—in this case, the **back_inserter** adds new elements in the vector results1, growing it as necessary. You also can pass a **binary predicate function** specifying how to compare elements for equality.

```
```cpp
// copy only unique elements of a1 into results1
std::vector<int> results1{};
std::ranges::unique_copy(a1, std::back_inserter(results1));
std::cout << "\nAfter unique_copy, results1 contains: ";
std::ranges::copy(results1, output);
```
```

```
```text
After unique_copy results1 contains: 1 3 5 7 9
```
```