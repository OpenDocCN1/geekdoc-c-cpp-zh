```
struct msg {
  char *p1;
  char *p2;
}
```

```
myptrs.p1 = "Teach Yourself C In One Hour a Day";
myptrs.p2 = "By SAMS Publishing";
```

Figure 11.4 illustrates the result of executing these statements. Each pointer member of the structure points to the first byte of a string, stored elsewhere in memory. Contrast this with Figure 11.3, which shows how data is stored in a structure that contains arrays of type char.

# FIGURE 11.4
A structure that contains pointers to type char.

![](bbox=[0.278, 0.355, 0.745, 0.603])

You can use pointer structure members anywhere a pointer can be used. For example, to print the pointer-to-strings, you would write
printf("%s %s", myptrs.p1, myptrs.p2);

What's the difference between using an array of type char as a structure member and using a pointer to type char? Both are methods for “storing” a string in a structure, as shown here in the structure msg, which uses both methods:

```
struct msg {
  char *p1[30];
  char *p2;      /* caution: uninitialized */
} myptrs;
```

Recall that an array name without brackets is not a pointer to the first element. Therefore, you can use these two structure members in similar fashion. (Note that p2 should be initialized before you copy a value to it.)