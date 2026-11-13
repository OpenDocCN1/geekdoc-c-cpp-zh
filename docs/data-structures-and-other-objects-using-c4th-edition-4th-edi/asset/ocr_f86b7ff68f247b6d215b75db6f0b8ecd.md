+   a. Transfer data[i-1] down to the end of subset[i-1]->data. This actually removes the item from the root, so shift data[i], data[i+1], and so on, leftward to fill in the gap. Also remember to subtract one from data_count, and add one to subset[i-1]->data_count.
+   b. Transfer all the items and children from subset[i] to the end of subset[i-1]. Remember to update the values of subset[i-1]->data_count and subset[i-1]->child_count. Also set subset[i]->data_count and subset[i]->child_count to zero.
+   c. Delete the node subset[i], and shift subset[i+1], subset[i+2], and so on, leftward to fill in the gap. Also reduce child_count by one.

For example, let's call fix_shortage(2) for this tree (with MINIMUM set to 2):

![](bbox=[0.17, 0.35, 0.83, 0.45])

In this example, subset[2] is merged with its sibling to the left. During the merge, the 28 also is passed down from the root to become a left entry of the merged nodes. The result is the following tree:

![](bbox=[0.17, 0.53, 0.83, 0.63])

As you can see, this tree has too few entries in its own root, but that is okay because the postcondition of fix_shortage allows the root of the resulting tree to have one less than the required number of entries.

# Case 4 for fix_shortage: Combine subset[j] with subset[i+1].

Our fourth case is to combine the problem subset with subset[i+1]. The work is similar to what you have just seen for combining with subset[i-1].

You now have enough information to write the fix_shortage member function. You should emphasize a clear logical structure to determine which of the four cases are appropriate. Your implementation will be cleaner if you provide four new private member functions to do the actual work in each of the four cases.