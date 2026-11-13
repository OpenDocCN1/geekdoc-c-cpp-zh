The operator +. This is an ordinary function (not a member function) with the prototype:

```
bag<Item> operator +(const bag& b1, const bag& b2);
```

The function is easy to implement by using the operator +=. Look back at the operator + from a previous bag implementation if you are uncertain.

# Time Analysis and an Iterator

With the descriptions that we've given, you can put together the implementation file for the new bag. We'll carry out a time analysis of the operations after we've seen a few more trees (see Section 11.3).

You might also want to add an iterator to the new bag, to allow a programmer to step through the items of the bag one at a time. One method for implementing an iterator is described in Programming Project 7 on page 535.

# Self-Test Exercises for Section 10.5

+   22. Why is it bad to insert nodes from smallest to largest in a binary search tree?

+   23. Build a binary search tree with the following words (inserted in this order): blueberry, peach, apricot, pear, cherry, mango, and papaya.

+   24. How many comparisons are needed to search for these words in the search tree you created in the previous exercise: pear, orange, blueberry?

+   25. Add a new member function to the bag. The function should print all items in the bag from smallest to largest. (Hint: Use a traversal.)

+   26. Write a bag friend function called join with this prototype:

```
template <class Item>
void join(
    bag<Item>& top,
    bag<Item>& left,
    bag<Item>& right
);
```

The precondition of the function requires that top has just one item, that everything in left is less than or equal to the item in top, and that everything in right is greater than the item in top. The postcondition requires that top now contains everything from left and right, and that left and right are now both empty. Your function should take constant time.

# CHAPTER SUMMARY

+   • Trees are a nonlinear structure, with many applications, including organizing information (such as taxonomy trees) and implementing an efficient version of the bag class (using binary search trees).

+   • Trees may be implemented with either fixed-sized arrays or dynamic data structures. An array is particularly appropriate for complete binary trees because of the conditions that require the nodes of a complete tree to occur in specific locations.