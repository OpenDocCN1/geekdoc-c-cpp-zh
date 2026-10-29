8. There is an index out of range. When index is equal to 9, index + 1 is equal to 10, so a[index + 1], which is the same as a[10], has an illegal index. The loop should stop with one fewer iteration. To correct the code, change the first line of the for loop to

```
for (int index = 0; index < 9; index++)
```

9. int i, a[20];
cout << "Enter 20 numbers:\n";
for (i = 0; i < 20; i++)
    cin >> a[i];

10. The array will consume 14 bytes of memory. The address of the indexed variable yourArray[3] is 1006.

11. The following function calls are acceptable:

```
tripler(a[2]);
tripler(a[number]);
tripler(number);
```

The following function calls are incorrect:

```
tripler(a[3]);
tripler(a);
```

The first one has an illegal index. The second has no indexed expression at all. You cannot use an entire array as an argument to tripler, as in the second call. The section Entire Arrays as Function Arguments discusses a different situation in which you can use an entire array as an argument.

12. The loop steps through indexed variables b[1] through b[5], but 5 is an illegal index for the array b. The indexes are 0, 1, 2, 3, and 4. The correct version of the code is given below:

```
int b[5] = {1, 2, 3, 4, 5};
for (int i = 0; i < 5; i++)
    tripler(b[i]);
```

13. void oneMore(int a[], int size)
//Precondition: size is the declared size of the array a.
//a[0] through a[size-1] have been given values.
//Postcondition: a[index] has been increased by 1
//for all indexed variables of a.
{
    for (int index = 0; index < size; index++)
        a[index] = a[index] + 1;
}

14. The following function calls are all acceptable: