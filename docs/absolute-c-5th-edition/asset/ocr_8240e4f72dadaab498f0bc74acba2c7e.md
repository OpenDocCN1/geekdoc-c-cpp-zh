# Linked List Applications 785

EXAMPLE: (continued)

The code implementing a generic set of elements appears in Displays 17.28 and 17.29. The Set class uses the linked list tools from Display 17.14. The add function simply adds a node to the front of the linked list, but only if the item is not already in the set. The contains function uses the search function from the linked list library. We simply loop through every item in the list looking for the target.

The union function combines the elements in the calling objects with the elements from the input argument, otherSet. To union these sets we create a new empty set object. Next, we iterate through both the calling object's set and otherSet's. All elements are added to the new set. The add function enforces uniqueness so we do not have to check for duplicate elements in the union function.

The intersection function is similar to the union function in that it also creates a new, empty set object. In this case, we populate the set with items that are common to both the calling object's set and otherSet's set. This is accomplished by iterating through every item in the calling object's set. For each item, we invoke the contains function for otherSet. If contains returns true, the item is in both sets and can be added to the new set.

A short demonstration program is in Display 17.30.

Display 17.27 Set Implementation Using Linked Lists

![](bbox=[0.125, 0.593, 0.857, 0.696])

> Set
A set is an unordered collection of data elements.