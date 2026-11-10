profit to your company from shipping these items minus any penalty for exceeding the capacity of this shipping bin.

If a maturation operator is used, its goal would be to either remove the penalty or increase the profit of the goods. If the selected items exceed the capacity of the bin, the maturation operator could simply look down the list of items to be shipped in order of increasing profit, and remove the first one that places the user under the limit. If no single item can be found, remove the item that yields the least profit and check the others again. If, on the other hand, the selected items do not completely fill the bin, the maturation operator could look through the list of unselected items in order of decreasing profit and add the first one that does not cause the bin capacity to be exceeded. Once this item is added to the list of packed items (the 0 at its position in the solution array is changed to a 1), the remaining items can be checked to see if another can be added.

For the QSAR/QSPR problem type, it is generally desirable to keep the number of nonzero elements in the solution array fixed to the number of descriptors required in the solution. This means that the user can randomly choose a selected descriptor and a non-selected one and change the values of the elements at these positions. This is shown in the following example.

```
(1,0,0,0,1,0,1,0) Parent solution
      | |      Selected solutions
(1,0,1,0,0,0,1,0) offspring solution
```

An additional mutation operator can be used if the elements of the solution array can have values different than 0 and 1 to represent different functional forms of the descriptors. For example, if the allowed values range from 0 to 4, this mutation operator can randomly choose a descriptor that is to be included and randomly change the value of its array element to any allowed, nonzero value (1, 2, 3, or 4). Conversely, a maturation operator can be employed that examines each selected descriptor and sequentially uses all allowed, nonzero values while keeping the other elements of the array fixed. The value of this element would then be set to the value that yields the best result. Once this is done for all chosen descriptors, this process can be repeated until no nonzero element is changed.

Finally, in a QSPR examination it was found that if the COST of the solution contained a term that added a penalty for having the wrong number of descriptors, better results were obtained when an extra descriptor is added first and then a descriptor is removed in a later generation. Care had to be taken during this study to ensure that the penalty was not too large to prohibit any extra terms from being added, and not too small to allow the program to use too many descriptors. The