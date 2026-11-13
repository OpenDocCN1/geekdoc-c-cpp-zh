implementing erase_one

The code for the erase_one function, shown in Figure 3.3, follows these three steps. The only item added is a check that the target is actually in the bag. If we discover that the target is not in the bag, then we do not need to remove anything (and the function returns false). Also note that our function works correctly for the boundary values of removing the first or last item in the array. Before we continue, we want to point out some programming techniques. Look at the following while-loop from Figure 3.3:

```
index = 0;
while ((index < used) && (data[index] != target))
    ++index;
```

To begin, the index is set to zero. The boolean expression indicates that the loop continues as long as index is still a location in the used part of the array (i.e., index < used) and we have not yet found the target (i.e., data[index] != target). Each time through the loop, the index is incremented by one

# FIGURE 3.3 Implementation of the Member Function to Remove an Item

# A Member Function Implementation

```
bool bag::erase_one(const value_type& target)
// Postcondition: If target was in the bag, then one copy has been removed;
// otherwise the bag is unchanged. A true return value indicates that one
// copy was removed; false indicates that nothing was removed.
{
    size_type index; // The location of target in the data array

    // First, set index to the location of target in the data array, which could be as small as
    // 0 or as large as used-1. If target is not in the array, then index will be set equal to
    // used.
    index = 0;
    while ((index < used) && (data[index] != target))
        ++index;

    if (index == used)
        return false; // target isn't in the bag, so no work to do.

    // When execution reaches here, target is in the bag at data[index].
    // So, reduce used by 1 and copy the last item onto data[index].
    --used;
    data[index] = data[used]; <-- See Self-Test Exercise 13 for an
    alternative approach to this step.
    return true;
}
```