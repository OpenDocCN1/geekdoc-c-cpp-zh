```
7. for (ch = 'A'; ch <= 'F'; ch++)
    if (ch == 'A')
        letterCount[ch] = 1;
    else
        letterCount[ch] = letterCount[ch - 1] + 1;
```

```
8. for (i = 0; i < n - 1; i++)
    for (j = 0; j < n - i - 1; j++)
        if (number[j] > number[j + 1])
        {
            temp = number[j];
            number[j] = number[j + 1];
            number[j + 1] = temp;
        }
```

For Exercises 9–14, write definitions of the given arrays in two ways: (a) without using typedef and (b) using typedef.

+   9. An array with capacity 10 in which each element is an integer.
+   10. An array whose indices are integers from 0 through 10 and in which each element is a real value.
+   11. An array with capacity 10 in which each element is an integer, all of which are initially 0.
+   12. An array that can store five strings.
+   13. An array that can store five characters and is initialized with the vowels a, e, i, o, and u.
+   14. An array that can store 100 values, each of which is either true or false.

For Exercises 15–18, write definitions and statements to construct the given array.

+   15. An array whose indices are the integers from 0 through 99 and in which the value stored in each element is the same as the index.
+   16. An array whose indices are the integers from 0 through 99 and in which the values stored in the elements are the indices in reverse order.
+   17. An array of capacity 50 in which the value stored in an element is true if the corresponding index is even and false otherwise.
+   18. An array whose indices are the decimal ASCII values (0-127), such that the value stored in an element is true if the index is that of a vowel, and false otherwise.