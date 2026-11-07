```
```cpp
namesMultiSet.insert("Goofy");                         //Line 58
namesMultiSet.insert("Donny");                         //Line 59

cout << "Line 60: namesMultiSet: ";                    //Line 60
copy(namesMultiSet.begin(), namesMultiSet.end(),        //Line 61
     pScreen);
cout << endl;                                             //Line 62

return 0;                                                //Line 63
}                                                        //Line 64
```
```

# Sample Run:

```
Line 18: intSet: 3 8 16 20
Line 28: intSetA: 238 156 84 59 39 36 30
Line 32: After removing 59, intSetA: 238 156 84 39 36 30
Line 40: After removing the fourth element,
         intSetA: 238 156 84 36 30
Line 44: intSetB: 238 156 84 36 30
Line 48: After removing all elements,
         intSetB:
Line 60: namesMultiSet: Zippy Hungry Goofy Goofy Donny Donny
```

The statement in Line 10 declares intSet to be a set container. The statement in Line 11 declares intSetA to be a set container whose elements are to be arranged in descending order. The statement in Line 12 declares intGtIt to be a set iterator. The iterator intGtIt can process the elements of any set container whose elements are of type int and are arranged in descending order. The statement in Line 13 declares screen to be an ostream iterator that outputs the elements of any container whose elements are of type int.

The statements in Lines 14 through 17 insert 16, 8, 20, and 3 into intSet, and the statement in Line 19 outputs the elements of intSet. In the output, see the line marked Line 18; it contains the output of the statements in Lines 18 through 20.

The statements in Lines 21 through 27 insert 36, 84, 30, 39, 59, 238, and 156 into intSetA, and the statement in Line 29 outputs the elements of intSetA. In the output, see the line marked Line 28. It contains the output of the statements in Lines 28 through 30. Notice that the elements of intSetA appear in descending order.

The statement in Line 31 removes 59 from intSetA. After the statement in Line 35 executes, intGtIt points to the first element of intSetA. The statement in Line 36 advances intGtIt to the next element of intSetA. After the statement in Line 38 executes, intGtIt points to the fourth element of intSetA. The statement in Line 39 removes the element of intSetA pointed to by intGtIt. The meanings of the statements in Lines 43 through 50 are similar.

The statement in Line 51 declares namesMultiSet to be a container of type multiset. The elements in namesMultiSet are of type string and are arranged in descending order. The statement in Line 52 declares iterator to be a multiset iterator.