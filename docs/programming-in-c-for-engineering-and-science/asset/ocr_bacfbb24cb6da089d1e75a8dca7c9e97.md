```
10. while (v < number)
{
    v.erase(v.begin());
    number.erase(number.begin());
}
```

For Exercises 11–15 write a declaration for a vector<T> having the given properties.

+   11. Can store long int values.
+   12. Capacity 10 and each element is a long int.
+   13. Capacity 10 and each element is a long int, all of which are initially 0.
+   14. Capacity 5, size 5, and each element contains a string, initially "xxx".
+   15. Capacity 100 and each element is either true or false.

For Exercises 16–18, write definitions and statements to construct a vector<T> with the required properties.

+   16. Stores the sequence of integers from 0 through 99.
+   17. Stores the sequence of integers from 0 through 99 in reverse order.
+   18. Has capacity 50, and the value stored in an element is true if the corresponding index is even and is false otherwise.

Exercises 19–25 ask you to write functions to do various things. To test these functions, you should write driver programs as instructed in Programming Problems 1–3 of Section 12.6.

+   19. Returns true if the values stored in a vector<double> are in ascending order and false otherwise.
+   20. Finds the range of values stored in a vector<double>, that is, the difference between the largest value and the smallest value.

Exercises 21–25 deal with operations on n-dimensional vectors, which are sequences of n real numbers and which are studied and used in many areas of mathematics and science. They can obviously be modeled in C++ by vector<double>s of capacity n. In the description of each operation, A and B are assumed to be n-dimensional vectors:

A = (a₁, a₂, ..., aₙ)
B = (b₁, b₂, ..., bₙ)