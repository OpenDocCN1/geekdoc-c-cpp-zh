```
for (int i = 0; i < 4; i++) {
    printf("%d: %s\n", a[i].leg_count, a[i].name);
}
```

As long as you give sort() a function that can compare two items that you have in your array to be sorted, it can sort anything. And it does this without needing to have the types of the items hardcoded in there anywhere.
qsort() just rearranges blocks of bytes based on the results of the compar() function you passed in.