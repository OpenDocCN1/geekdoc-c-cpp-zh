```
```cpp
cout << "Line 43: resultList after rotating and "
     << "copying:\n"
     << "            ";                         // line 43
copy(resultList.begin(), resultList.end(),
     screen);                                   // line 44
cout << endl;                                   // line 45

return 0;                                       // line 46
}                                               // line 47
```
```

# Sample Run:

```
```text
Line 12: intList: 1 3 5 7 9 0 2 4 6 8
Line 16: intList after reversal: 8 6 4 2 0 9 7 5 3 1
Line 20: intList: 1 3 5 7 9 0 2 4 6 8
Line 26: intList before rotating: 8 6 4 2 0 9 7 5 3 1
Line 30: intList after rotating: 4 2 0 9 7 5 3 1 8 6
Line 35: intList after rotating and copying:
         4 2 0 9 7 5 3 1 8 6
Line 38: resultList after rotating and copying:
         0 9 7 5 3 1 8 6 4 2
Line 43: resultList after rotating and copying:
         6 4 2 0 9 7 5 3 1 8
```
```

# The Functions `count`, `count_if`, `max`, `max_element`, `min`, `min_element`, and `random_shuffle`

The algorithm count counts the occurrences of a given value in a given range. The prototype of the function implementing this algorithm is as follows:

```
```cpp
template <class InputItr, class T>
iterator_traits<InputItr>::difference_type
        count(InputItr first, InputItr last, const T& value);
```
```

The function count returns the number of times the value specified by the parameter `value` occurs in the range `first...last-1`.

The algorithm `count_if` counts the occurrences of a given value in a given range, satisfying a certain criterion. The prototype of the function implementing this algorithm is as follows:

```
```cpp
template <class InputItr, class UnaryPredicate>
iterator_traits<InputItr>::difference_type
        count_if(InputItr first, InputItr last, UnaryPredicate Op);
```
```

The function count_if returns the number of elements in the range `first...last-1` for which `op(elemRange)` is true.