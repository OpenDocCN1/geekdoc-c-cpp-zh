# 12.7. EXERCISES

+   - Permutations
- More permutations

# 12.7 Exercises

1. Complete the function that reorders the contents of a vector so that the even values are reversed from their original order. For example, a vector containing the elements 2, 6, 2, 5, 0, 1, 2, 3 would be transformed into 3, 2, 1, 0, 5, 2, 6. Note that your function must physically rearrange the elements within the vector, not just print the elements in reverse.

```
void reverse(vector<int>& v) {
    // Add your code...
}
```

2. Complete the function that reorders the contents of a vector so that all the even numbers appear before any odd number. The even numbers are also sorted in ascending order with respect to themselves, and the odd numbers are also sorted in ascending order with respect to themselves. For example, a vector containing the elements 2, 1, 10, 4, 3, 6, 7, 8, 5 would be transformed into 2, 4, 6, 8, 1, 3, 5, 7, 9. Note that your function must physically rearrange the elements within the vector, not just print the elements in reverse order.

```
void special_sort(vector<int>& v) {
    // Add your code...
}
```

3. Complete the function that shifts all elements of a vector back one position. The last element that shifted off the end of the vector is copied into the first (0th) position. For example, if a vector containing the elements 2, 1, 10, 4, 3, 6, 7, 9, 8 is passed to the function, it would be transformed into 8, 2, 1, 10, 4, 3, 6, 7, 9. Note that your function must physically rearrange the elements within the vector, not just print the elements in the shifted order.

```
void rotate(vector<int>& v) {
    // Add your code...
}
```

4. Complete the function that determines if the number of even and odd values in a vector is the same. The function return true if the vector contains 5, 1, 0, 2 (two evens and two odds), but would return false for the vector containing 5, 1, 0, 21 (too many odds). The function return true if the vector is empty, an empty vector contains the same number of evens and odds (0). The function does not affect the contents of the vector.

```
bool balanced(const vector<int>& v) {
    // Add your code...
}
```

5. Complete the function that returns true if all elements in a vector are unique. It returns false if any element appears more than once; the vector 2, 3, 2, 1, 9 contains duplicates (2 appears more than once), but the vector 2, 1, 0, 3, 8, 4 does not (none of the elements appear more than once).

An empty vector has duplicates.
The function does not affect the contents of the vector.