```
// replace contents of values with elements of otherValues
values.assign(otherValues.cbegin(), otherValues.cend());
cout << "\nAfter assign, values contains: ";
printList(values);

// remove otherValues elements and insert into values in sorted order
values.merge(otherValues);
cout << "\nAfter merge, values contains: ";
printList(values);

values.remove(4); // remove all 4s
cout << "\nAfter remove(4), values contains: ";
printList(values);
cout << endl;
}

// printList function template definition; uses
// ostream_iterator and copy algorithm to output list elements
template <typename T> void printList(const list<T>& listRef) {
    if (listRef.empty()) { // list is empty
        cout << "List is empty";
    }
    else {
        ostream_iterator<T> output(cout, " ");
        copy(listRef.cbegin(), listRef.cend(), output);
    }
}
```

```
values contains: 2 1 4 3
values after sorting contains: 1 2 3 4
After insert, otherValues contains: 2 6 4 8
After splice, values contains: 1 2 3 4 2 6 4 8
After sort, values contains: 1 2 2 3 4 4 6 8
After insert and sort, otherValues contains: 2 4 6 8
After merge:
    values contains: 1 2 2 2 3 4 4 4 6 6 8 8
    otherValues contains: List is empty
After pop_front and pop_back:
    values contains: 2 2 2 3 4 4 4 6 6 8
After unique, values contains: 2 3 4 6 8
After swap:
    values contains: List is empty
    otherValues contains: 2 3 4 6 8
After assign, values contains: 2 3 4 6 8
After merge, values contains: 2 2 3 3 4 4 6 6 8 8
After remove(4), values contains: 2 2 3 3 6 6 8 8
```

Fig. 15.13 Standard Library `list` class template.