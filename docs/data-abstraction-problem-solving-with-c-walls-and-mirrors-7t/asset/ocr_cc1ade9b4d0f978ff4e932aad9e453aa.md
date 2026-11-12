# 1.5.1 Identifying Behaviors

Since a bag contains a finite number of objects, reporting how many objects it contains could be one of a bag's behaviors:

+   - Get the number of items currently in the bag.

A related behavior detects if a bag is empty:

+   - See whether the bag is empty.

We should be able to add and remove objects:

+   - Add a given object to the bag.
+   - Remove an occurrence of a specific object from the bag, if possible.
+   - Remove all objects from the bag.

Note that the add operation does not indicate where in the bag an object should go. Remember that a bag does not order its contents. The remove operation looks for a particular item in the bag. If it finds it, it takes it out. If the bag contains several objects equal to the removed one, they remain in the bag. If the operation can't find the specific object in the bag, it can't remove it, and just says so. Finally, the second remove operation simply empties the bag of all objects.

What is in a particular bag? The answer to this question can be answered by the following operations:

+   - Count the number of times a certain object occurs in the bag.
+   - Test whether the bag contains a particular object.
+   - Look at all objects that are in the bag.

We have enough behaviors for now. At this point, we would have written all the behaviors on a piece of paper or, as Appendix C suggests, on the **class-responsibility-collaboration (CRC) card** pictured in Figure 1-6.

# FIGURE 1-6 A CRC card for a Class Bag

| Responsibilities | Bag |
|---|---|
| Get the number of items currently in the bag | |
| See whether the bag is empty | |
| Add a given object to the bag | |
| Remove an occurrence of a specific object from the bag | |
| Remove all objects from the bag | |
| Count the number of times a certain object occurs in the bag | |
| Test whether the bag contains a particular object | |
| Look at all objects that are in the bag | |
| Collaborations | |
| The class of objects that the bag can contain | |