# Removing the Biggest Item from a B-Tree

Our final member function has this specification:

```
template <class Item>
void set<Item>::remove_biggest(Item& removed_entry);
// Precondition: data_count > 0 and the entire B-tree is valid.
// Postcondition: The largest item in the set has been removed, and a copy
// of this removed entry has been placed in removed_entry. The entire
// B-tree is still valid, EXCEPT that the number of entries in the root of this
// set may be one less than the allowed minimum.
```

The work of remove_biggest is easy if the root has no children. In this case,
we copy the last item of data into the reference parameter, removed_entry.
Then we subtract one from data_count. That's all! We might be left with a
node that has one less than the allowed minimum number of entries, but accord-
ing to the postcondition, that is okay.

What if the root has children? In this case, we make a recursive call to remove
the largest entry from the rightmost child. The recursive call is:

```
subset[child_count-1]->remove_biggest(removed_entry);
```

Notice the argument, removed_entry, that we use in the recursive call. This
argument will be set equal to the item that is removed from the subtree. This is
exactly what we need, and there is only one remaining problem. The recursive
call might leave the root of subset[child_count-1] with one entry too few.
How can we fix a child that has a shortage of entries? The fix_shortage func-
tion can fix such a node. So, after the recursive call, you should check the number
of entries in the root of subset[child_count-1]. If the number of entries is less
than MINIMUM, then call fix_shortage(child_count-1).

# PROGRAMMING TIP

# WRITE AND TEST SMALL PIECES

If you are implementing the entire set class, don't try to do the whole thing at once.
Instead, you should write and test functions one at a time. In this project, you
should also carry out a major testing after you have completed the insert and
count functions, and before you have started on any of the erasing machinery.

When you start the erasing functions, draw a diagram of the top-down design
that you are implementing.

Test pieces as soon as you can. This early testing can be aided by initially
implementing all of your planned functions with a single line that simply prints the
name of the function, indicating that the function has been activated. A single line
such as this is called a stub. With stubs in place, you can test any function as soon
as you have written the complete version. For example, as soon as you implement
the erase function, you can test it. You know that it should call the loose_erase
function, so you expect the loose_erase stub to print a message indicating that
loose_erase has been called.