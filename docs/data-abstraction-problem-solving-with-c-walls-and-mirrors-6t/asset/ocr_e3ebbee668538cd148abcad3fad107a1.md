# FIGURE 9-2 Shifting items for insertion: (a) the list before the insertion; (b) copy items to produce room at position 3; (c) the result.

![](bbox=[0.06, 0.15, 0.92, 0.48])

We can begin testing these methods once we write stubs for the remaining methods. To thoroughly test insert, however, we need the method getEntry, which we define next.

**Question 1** Given a nonempty list that is an instance of ArrayList, at what position does an insertion of a new entry require the fewest operations? Explain.

**Question 2** Describe an implementation of the method insert for ArrayList that places the entry in position 1 in the last element of the array, the entry in position 2 in the next-to-last element, and so on.

**Question 3** How does the original version of insert given previously compare with the one described in Question 2 with respect to the number of operations required?

**The method getEntry.** This method simply needs to return the value in items[position], but we decided to enforce the method's precondition by throwing an exception if position is out of bounds. For the purpose of testing the method insert, you could write a temporary version of getEntry that does not throw an exception but just returns the desired list entry. You would then complete its definition as follows:

```
template<class ItemType>
ItemType ArrayList<ItemType>::getEntry(int position) const
throw(PrecondViolatedExcep)
```