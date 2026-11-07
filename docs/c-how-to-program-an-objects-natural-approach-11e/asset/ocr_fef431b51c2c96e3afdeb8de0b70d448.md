# ### Creating a list Object

Line 23 creates a list object capable of storing ints. Lines 26–27 use its member function push_front to insert integers at the beginning of values. This member function is specific to classes forward_list, list and deque. Lines 28–29 use push_back to append integers to values. Function push_back is common to all sequence containers except array and forward_list. Lines 31–32 show the current contents of values.

```
```cpp
22  int main() {
23    std::list<int> values{}; // create list of ints
24
25    // insert items in values
26    values.push_front(1);
27    values.push_front(2);
28    values.push_back(4);
29    values.push_back(3);
30
31    std::cout << "values contains: ";
32    printList(values);
33
```
```

```
```text
values contains: 2 1 4 3
```
```

# ### list Member Function sort

Line 34 uses list member function sort to arrange the elements in ascending order. A second version of sort allows you to supply a binary predicate function that takes two arguments (values in the list), performs a comparison and returns a bool value indicating whether the first argument should come before the second in the sorted contents. This function determines the order in which the elements are sorted. This version is useful for sorting a list in descending order or customizing how elements are compared to determine the sort order.

```
```cpp
34    values.sort(); // sort values
35    std::cout << "\nvalues after sorting contains: ";
36    printList(values);
37
```
```

```
```text
values after sorting contains: 1 2 3 4
```
```

# ### list Member Function splice

Line 46 uses list member function splice to remove the elements in otherValues and insert them into values before the iterator position specified as the first argument. Function splice with three arguments allows one element to be removed from the container specified as the second argument from the location specified by the iterator in the third argument. Function splice with four arguments uses the last two arguments to specify a common range to remove from the list in the second argument and insert at the location specified in the first argument. A forward_list provides a similar member function named splice_after.