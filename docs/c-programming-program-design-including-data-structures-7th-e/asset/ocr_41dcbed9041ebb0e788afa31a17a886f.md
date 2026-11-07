```
cout << "Line 37: resultList after rotating and "
     << "copying:\n"
     << "        ";                                      //Line 37
copy(resultList.begin(), resultList.end(), screen); //Line 38
cout << endl;                                       //Line 39

return 0;
}
```

# Sample Run:

```
Line 6: intList: 1 3 5 7 9 0 2 4 6 8
Line 10: intList after reversal: 8 6 4 2 0 9 7 5 3 1
Line 14: resultList: 1 3 5 7 9 0 2 4 6 8
Line 20: intList before rotating: 8 6 4 2 0 9 7 5 3 1
Line 24: intList after rotating: 4 2 0 9 7 5 3 1 8 6
Line 29: intList after rotating and copying:
             4 2 0 9 7 5 3 1 8 6
Line 32: resultList after rotating and copying:
             0 9 7 5 3 1 8 6 4 2
Line 37: resultList after rotating and copying:
             6 4 2 0 9 7 5 3 1 8
```

# The Functions count, count_if, max, max_element,
min, min_element, and random_shuffle

The algorithm count counts the occurrences of a given value in a given range. The prototype of the function implementing this algorithm is:

```
template <class InputItr, class type>
iterator_traits<InputItr>::difference_type
        count(InputItr first, InputItr last, const Type& value);
```

The function count returns the number of times the value specified by the parameter value occurs in the range first...last-1.

The algorithm count_if counts the occurrences of a given value in a given range, satisfying a certain criterion. The prototype of the function implementing this algorithm is:

```
template <class InputItr, class unaryPredicate>
iterator_traits<InputItr>::difference_type
        count_if(InputItr first, InputItr last, unaryPredicate op);
```

The function count_if returns the number of elements in the range first...last-1 for which op(elemRange) is true.