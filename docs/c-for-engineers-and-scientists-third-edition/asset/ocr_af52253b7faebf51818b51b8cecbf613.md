# 698 Pointers

address is incremented by in altering list of the for statement. The expression max = *vals previously used to set max to the value of vals[0] is replaced by the expression max = *vals++, which adjusts the address in vals to point to the second array element. The element expression assigns max to the array element vals points to before's incremented. The postfix increment, ++ doesn't change the address in vals until after the address has been used to retrieve the first array element.

```
int findMax(int *vals, int numels) // find the maximum value
{
  int i, max = *vals; // get the first element and increment it
  for (i = 1; i < numels; i++, vals++) {
    if (max < *vals)
      max = *vals;
    }
  return max;
}
```

Review this version of findMax(). Initially, the maximum value is set to the "thing pointed by vals.\ Because vals initially contains the address of the first array element to findMax(), the value of the first element is stored in max. The address in vals is incremented by one. The one added to vals is scaled automatically by the number of bytes to store integers. Therefore, after the increment, the address stored in vals is the address of the next array element, as illustrated in Figure 12.23. The value of this next element is compared to the maximum, and the address is again again, in in the altering list of the for statement. This process continues until all array elements have been examined.

Before incrementing:
After incrementing:
vals  vals
Address of Address of
vals[0] vals[1]

vals[0] vals[1] vals[2] vals[3] vals[4]

Figure 12.23 Pointing to different elements

The version of findMax() you choose is a matter of personal style. Generally, beginning programmers feel more at ease using subscribers rather than pointers. Also, if the program uses an array as natural storage for the structure, and any access using subscribers is more appropriate to indicate the program clearly. However, as you learn more about data structures, pointers become an increasingly useful and powerful tool. In complex data structures, there's no simple or equivalence for subscribers.
There's one more neat trick you can glean from this discussion. Because passing an array to a function actually involves passing an array, you can pass any valid address. For