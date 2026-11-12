
a list. However, you can write a set of axioms that completely describes the behavior of the list operations. For example,

> A newly created list is empty

is an axiom because it is true for all newly created lists. You can state this axiom succinctly in terms of the ADT list operations as follows:

```
(new List()).isEmpty() = true
```

The statement

> If you insert an item x into the i<sup>th</sup> position of a list, retrieving the i<sup>th</sup> item will result in x

is true for all lists, and so it is an axiom. You can state this axiom in terms of the ADT list operations as follows:

```
(alist.insert(i, x)).getEntry(i) = x
```

That is, getEntry returns the item x that insert has put at position i of aList.

The following axioms formally define the ADT list:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_284_0.png)

A set of axioms does not make the preconditions and postconditions for an ADT's operations unnecessary. For example, the previous axioms do not describe insert's behavior when you try to insert an item into position 50 of a list of two items. One way to handle this situation is to include the restriction

```
1 <= position <= getLength() + 1
```

in insert's precondition. Another way—which we used in our previous specifications of the ADT list—does not restrict position, but rather has the method return false if position is outside the previous range. Thus, you need both a set of axioms and a set of preconditions and postconditions to define the behavior of an ADT's operations completely.

Use axioms to determine the effect of a sequence of ADT operations

You can use axioms to determine the outcome of a sequence of ADT operations. For example, if alist is a list of strings and s and t are strings, how does the sequence of operations

```
alist.insert(1, t)
alist.insert(1, s)
```

affect aList? We will show that s is the first item in this list and t is the second item by using getEntry to look at these items.

You can write the previous sequence of operations in another way as

```
(alist.insert(1, t)).insert(1, s)
```

or

```
tempList = alist.insert(1, t)
tempList.insert(1, s)
```

Now get the first and second items in the list tempList.insert(1, s), as follows:

```
(tempList.insert(1, s)).getEntry(1) = s      by axiom 9
and
(tempList.insert(1, s)).getEntry(2)
= tempList.getEntry(1)
= (alist.insert(1, t)).getEntry(1)   by definition of tempList
= t                                      by axiom 9
```

Thus, s is the first item in the list and t is the second item.

## 8.2 Using the List Operations

We now consider some simple examples of how you can use the operations of the ADT list. Recall that exploring such uses is a way to confirm your understanding of an ADT's specifications and gives you an opportunity to change your mind about your design choices prior to implementing the ADT. You can write client functions in terms of the operations that define the ADT list, even though you do not know how the list's data is stored.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_285_0.png)

Displaying the items on a list. Suppose that you want to display the items on a list. Since this task is not an ADT list operation, we write pseudocode for a client function displayList that uses the ADT operations as follows:

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_285_1.png)

// Displays the items on the list alist.
displayList(alist)
for (position = 1 through alist.getLength())
{
   dataItem = alist.getEntry(position)
   Display dataItem
}

Notice that as long as the ADT list is implemented correctly, the displayList function will perform its task. In this case, getEntry successfully retrieves each list item, because position's value is always valid.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_285_2.png)

Replacing an item. Now suppose that we did not include the operation setEntry in our specification of the ADT list. To replace the entry at a given position in the list with a new one, we would need to write a client function. The following pseudocode defines such a function replace:

// Replaces the ith entry in the list aList with newEntry.
// Returns true if the replacement was successful; otherwise return false.
replace(aList, i, newEntry)
   success = aList.remove(i)
   if (success)
      success = aList.insert(i, newItem)
   return success

If removal is successful, it sets success to true. By testing success, replace will attempt the insertion only if the deletion actually occurred. Then insert sets success, which replace returns to the function that called it. If remove is unsuccessful for any reason, including an incorrect value of i, it sets success to false. The replace function then ignores the insertion and returns success.

> Note: Notice that the two previous algorithms depend only on the specifications of the list operations and not on their implementations. The algorithms do not depend on how you implement the list. They will work regardless of whether you use an array or some other data structure to store the list’s data. This feature is a definite advantage of abstract data types. In addition, by thinking in terms of the available ADT operations, you will not be distracted by implementation details.

Creating a list of names in alphabetical order. Let’s create a list of our friends’ names as we think of them. Moreover, let’s place the names on the list in alphabetical order. It is up to us to place each name into its correct position in the list. The ADT list does not choose the order of its entries.

The following pseudocode statements place the names Amy, Ellen, Bob, Drew, Aaron, and Carol in an alphabetical list. The comment at the end of each statement shows the list after the statement executes.

```
alphaList = a new empty list
alphaList.insert(1, "Amy")    // Amy
alphaList.insert(2, "Ellen")  // Amy Ellen
alphaList.insert(2, "Bob")    // Amy Bob Ellen
alphaList.insert(3, "Drew")   // Amy Bob Drew Ellen
alphaList.insert(1, "Aaron")  // Aaron Amy Bob Drew Ellen
alphaList.insert(4, "Carol")  // Aaron Amy Bob Carol Drew Ellen
```

After initially placing Amy at the beginning of the list and Ellen at the end of the list (at position 2), we insert

- Bob between Amy and Ellen at position 2
- Drew between Bob and Ellen at position 3
- Aaron before Amy at position 1
- Carol between Bob and Drew at position 4

Later in Chapter 11, you will learn that this way of inserting each name into a collection of alphabetized names is called an insertion sort.

If we now remove the entry at position 4—Carol—by writing

```
alphaList.remove(4)
```
Drew and Ellen will be at positions 4 and 5, respectively. Thus, aList.getEntry(4) would return Drew.

Finally, suppose that we want to replace a name in this list. We cannot replace a name with just any name and expect that the list will remain in alphabetical order. Replacing Bob with Ben by writing

```
aList.setEntry(3, "Ben");
```

would maintain alphabetical order, but replacing Bob with Nancy would not. The list's alphabetical order resulted from our original decisions about where to place names on the list. The order did not come about automatically as a result of list operations. That is, the client, not the list, maintains the order. We could, however, design an ADT that maintains its data in alphabetical order. You will see an example of such an ADT in Chapter 12.

![](img/4e46b89c20760dcd4e6d1b7d0bde2b6b_287_0.png)

Question 3 Write a pseudocode function swap(aList, i, j) that interchanges the items currently in positions i and j of a list. Define the function in terms of the ADT list operations, so that it is independent of any particular implementation of the list. Assume that the list, in fact, has items at positions i and j. What impact does this assumption have on your solution? (See Exercise 2 at the end of this chapter.)

Question 4 What grocery list results from the following sequence of ADT list operations?

```
aList = a new empty list
aList.insert(1, "butter")
aList.insert(1, "eggs")
aList.insert(1, "milk")
```

Question 5 Suppose that myList is a list that contains the five objects a b c d e.

- a. What does myList contain after executing myList.insert(5, w)?
- b. Starting with the original five entries, what does myList contain after executing myList.insert(6, w)?
- c. Which of the operations in parts a and b of this question require entries in the array to shift?

## 8.3 An Interface Template for the ADT List

We now will formalize our specification of the ADT list by writing a C++ interface, which is given in Listing 8-1.

### LISTING 8-1 A C++ interface for lists

```
/** Interface for the ADT list
@file List_Interface.h */
#ifndef _LIST_INTERFACE
#define _LIST_INTERFACE
template<class ItemType>
class ListInterface
```
