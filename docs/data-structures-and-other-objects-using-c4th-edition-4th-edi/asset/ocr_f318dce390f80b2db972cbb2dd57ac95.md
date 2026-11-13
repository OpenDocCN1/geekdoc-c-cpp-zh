# FIGURE 11.6 Top-Down Design for the insert Member Function

The insert function calls:

+   - loose_insert
+   - fix_excess

The loose_insert function is recursive and also calls:

+   - fix_excess
+   - various array functions

The fix_excess function calls:

+   - various array functions

# Employing Top-Down Design

As you work on the project, keep in mind the top-down design that we have employed. As shown in Figure 11.6, the original insert member function calls the private member function loose_insert. Both the ordinary insert and the loose insert functions call fix_excess. At several points in the design of fix_excess, you should propose and implement smaller functions to carry out the basic work of copying and shifting elements in an array. You might be able to use some functions from the <Algorithm> facility to do this array work (see Appendix G).

# Removing an Item from a B-Tree

The erase member function of the set removes an entry from the B-tree. Most of the work will be accomplished with a private member function, loose_erase, which performs a “loose removal” that is analogous to the loose insertion. The looseness in loose_erase occurs because it is allowed to leave a root that has one entry too few. In other words, it might leave the root of the whole tree with zero entries (which is not permitted unless there are also no children), or it might leave the root of an internal subtree with fewer than MINIMUM entries. The specification of loose_erase is given here:

```
template <class Item>
bool set<Item>::loose_erase(const Item& target);
// Precondition: The entire B-tree is valid.
// Postcondition: If target was not in the set, then the set is unchanged and
// the return value is false. Otherwise, the target has been removed, the
// return value is true, and the entire B-tree is still valid
// EXCEPT that the number of entries in the root of this set might be one
// less than the allowed minimum.
```

Our complete erase function will first call loose_erase. Afterwards, if necessary, we can fix a root that may have been left with zero entries and one child. Thus, the erase pseudocode has these steps:

pseudocode for removal

```
// Pseudocode for the public erase member function
if (!loose_erase(target))
    Return false since loose_erase did not remove an entry from the set.
if ((data_count == 0) && (child_count == 1))
    Fix the root of the entire set so that it no longer has zero entries.
Return true since an entry was removed from the set.
```