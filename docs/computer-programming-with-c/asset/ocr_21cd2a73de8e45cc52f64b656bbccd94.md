```
```cpp
{
    cout<<*temp<<" ";
}
}
```
```

# **Output**

Sorted list
10 9 8 7 6 5 4 3 2 1

The statement

```
```cpp
ll.sort(compareLogic);
```
```

invokes the sort() function to sort linked list ll. Note that we have passed the function name customLogic to the sort() function as an argument. This informs the sort() algorithm to apply comparison of elements as specified in the user-defined function. The sort() algorithm will change the position of elements if the user-defined function compareLogic returns 0 (false) and keep the two elements intact if compareLogic returns 1 (true). Thereby, arranging the linked list ll in descending order as seen in the output of the code.

# **16.4.2  Difference between vector and linked list**

vector is very similar to linked list with two major differences:

+   1. Internally, vector is implemented as an array, and hence elements inside vector are stored in adjacent memory location. Whereas linked list is created using different node objects linked to each other using pointers. Hence nodes of linked list are not guaranteed to be in adjacent memory locations.
+   2. Vector supports random iterator which linked list does not. For example, if temp is an iterator object, then following statements are valid in vector but not in linked list.

| Iterator expression | Description |
|---|---|
| `temp=v1.begin()+5` | Makes the iterator `temp` point to 5th element from the beginning in vector named as `v1` |
| `temp=temp+8` | Moves iterator `temp` 8 steps ahead relative to its current location. So, for example, if `temp` is pointing to the 3rd element in the vector currently, the execution of this statement will make `temp` point to 11th position in the vector |
| `temp=temp-3` | Moves the iterator 3 steps behind. For example, if `temp` is currently pointing to 4th element of the vector after execution of this statement `temp` will start pointing to 1st element of the vector |

It is not possible to have these random movements of iterator in the linked list because linked list only supports two types of iterators:

+   1. Forward iterator
+   2. Backward iterator