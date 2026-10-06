```
return 0;
}
```

# Program 18.1. Output

```
dataArray:
two
three
four
dArray2:
two
three
four
dataArray:
two
three
four
dataArray2:
three
four
```

The program defines the mutable array object dataArray and sets its elements to the string objects @"one", @"two", @"three", and @"four". As weve discussed, the assignment

```
dataArray2 = dataArray;
```

simply creates another reference to the same array object in memory. When you remove the first object from dataArray2 and subsequently print the elements from both array objects, it's no surprise that the first element (the string @"one") is gone from both array object references.