# Consider the following example:

```
// https://godbolt.org/z/PeG4K7Edc
vararray v {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12};
vararray<int> r1(v(slice(0, 4, 3))); // Start at 0, 4 elements, step size 3
cout << r1; // Output: 1 4 7
vararray<int> r2(v > 6); // addressed by vararray<bool>
cout << r2;; // Output: 7 8 9 10 11 12
const vararray<size_t> indirect{2, 3, 6}; // duplicates allowed
vararray<int> r5(v(indirect)); // addressed by vararray<size_t>
cout << r5; // Output: 3 4 7
```

# 24.12.6 Specialty: Manipulate All There are a handful of useful

methods for information or manipulation over all data in the vararray:

+   - sum, min, and max
Calculate the sum, the minimum, and the maximum over all values. With a normal container, you would instead use, for example, accumulate or max_element from <algorithm>.

+   - shift and cshift
Shift and rotate the values around the entire vararray. shift rotates; cshift fills with zeros.

+   - apply
This calls a function for each element in the vararray. The function must take a T as an argument and return a T. You cannot modify the element. Overall, you get a new vararray back from apply. With normal containers, you would probably use for_each.