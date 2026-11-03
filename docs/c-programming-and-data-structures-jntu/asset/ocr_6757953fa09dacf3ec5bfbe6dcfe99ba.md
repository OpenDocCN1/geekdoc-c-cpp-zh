(a) 1 2 3 3 5 5 7 8
(b) 1 2 3 4 5 6 7 8
(c) 8 7 6 5 4 3 2 1
(d) 1 2 3 5 4 6 7 8

5. The order in which actual parameters are evaluated in a function call
(a) is from the left
(b) is from the right
(c) is compiler dependent
(d) none of the above

6. The default parameter passing mechanism is
(a) call by value
(b) call by reference
(c) call by value result
(d) none

7. C does no automatic array bound checking. This is
(a) true
(b) false
(c) C’s asset
(d) C’s shortcoming

8. If a two-dimensional array is used as a formal parameter, then
(a) both the subscripts may be left empty
(b) the first(row) subscript may be left empty
(c) the first subscript must be left empty
(d) both the subscripts must be left empty

9. If storage class is missing in the array definition, by default it will be taken to be
(a) automatic
(b) external
(c) static
(d) either automatic or external depending on the place of occurrence

10. Consider the declaration
static char hello[]="hello"; The output of printf("%s\n",hello);
will be the same as that of
(a) puts("hello");
(b) puts(hello);
(c) printf("%s\n","hello");
(d) puts("hello\n");

11. The array name can be a pointer to
(a) another array
(b) another variable
(c) to that array only
(d) none

12. An array of pointers to a table of strings saves
(a) time
(b) memory
(c) CPU utilization
(d) none of the above

```
main()
{
inc(); inc(); inc();
}
inc()
{
static int x;
printf("%d",++x);
}
```

13. The following program
prints
(a) 0 1 2
(b) 1 2 3
(c) 3 consecutive, but unpredictable numbers
(d) 1 1 1