```
```cpp
namesMultiSet.insert("Goofy");                         //Line 49
namesMultiSet.insert("Donny");                         //Line 50

cout << "Line 51: namesMultiSet: ";
copy(namesMultiSet.begin(), namesMultiSet.end(),
     pScreen);                                           //Line 52
cout << endl;                                            //Line 53

}
return 0;
```
```

# Sample Run:

```
Line 9: intSet: 3 8 16 20
Line 19: intSetA: 238 156 84 59 39 36 30
Line 23: After removing 59, intSetA: 238 156 84 39 36 30
Line 31: After removing the fourth element
          intSetA: 238 156 84 36 30
Line 35: intSetA: 238 156 84 36 30
Line 39: After removing all the elements,
          intSetB:
Line 51: namesMultiSet: Zippy Hungry Goofy Goofy Donny Donny
```

The statement in Line 1 declares intSet to be a set container. The statement in Line 2 declares intSetA to be a set container whose elements are to be arranged in descending order. The statement in Line 3 declares intGtIt to be a set iterator. The iterator intGtIt can process the elements of any set container whose elements are of type int and are arranged in descending order. The statement in Line 4 declares screen to be an ostream iterator that outputs the elements of any container whose elements are of type int.

The statements in Lines 5 through 8 insert 16, 8, 20, and 3 into intSet, and the statement in Line 10 outputs the elements in intSet. In the output, see the line marked Line 9; it contains the output of the statements in Lines 9 through 11.

The statements in Lines 12 through 18 insert 36, 84, 30, 39, 59, 238, and 156 into intSetA, and the statement in Line 20 outputs the elements of intSetA. In the output, see the line marked Line 19. It contains the output of the statements in Lines 19 through 21. Notice that the elements of intSetA appear in descending order.

The statement in Line 22 removes 59 from intSetA. After the statement in Line 26 executes, intGtIt points to the first element of intSetA. The statement in Line 27 advances intGtIt to the next element of intSetA. After the statement in Line 29 executes, intGtIt points to the fourth element of intSetA. The statement in Line 30 removes the element of intSetA pointed to by intGtIt. The meanings of the statements in Lines 34 through 41 are similar.

The statement in Line 42 declares namesMultiSet to be a container of type multiset. The elements in namesMultiSet are of type string and are arranged in descending order. The statement in Line 43 declares iter to be a multiset iterator.