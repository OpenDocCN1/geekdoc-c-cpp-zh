# Algorithm Case Analysis

Depending on the input sequence given to an algorithm, we can evaluate how much time and space are required to execute an operation. Based on this, following three types of cases are possible for an algorithm:

+   - **Worst Case**—Results in the worst possible running time to execute an algorithm. It depends on the input sequence and deals with the worst input case possible. Therefore, we can say that it represents the upper bound of the running time of an algorithm for any input. To describe this situation, let's take an example of sequential search, where the key is matched with every single element of a sequence until the match is found. Therefore, if the input sequence is such that the key value does not exist or the key value lies at the end of the sequence, then it is considered as the worst case behavior because the search operation needs to search every single element of the sequence.
+   - **Best Case**—Results in the best possible running time to execute an algorithm. It deals with the best input case possible. Therefore, we can say that it is the lower bound of the running time of an algorithm for any input. If we consider the example of sequential search again, then in the best case behavior, the key value lies at the first position of the sequence so that after one comparison, the match will be found and the search process will be over.
+   - **Average Case**—Results in the average running time to execute an algorithm. In this case, the input sequence is drawn randomly from a given distribution of elements. Its behavior lies between the best case behavior and the worst case behavior of an algorithm. In case of sequential search, average case is considered to be the one, where the key value lies in the middle of the sequence. Therefore, in the average case, it is often assumed that all the inputs in a given sequence are equally likely.

In the next section, let's discuss linked list, in detail.

# Linked List

A linked list is a data structure that can change during execution. It is similar to an array because they both store collections of data. However, there are certain disadvantages of arrays:

+   1. The size of the array is fixed.
+   2. Due to the fixed size, programmers allocate a huge size in advance, but most of the time it is wasted.
+   3. Insertion of new elements at the front of an array is a potential problem.

To compensate with the disadvantages of an array, linked lists were introduced. In a linked list, successive elements are connected by pointers. The last element in a linked list points to NULL. Linked lists can grow and shrink in size during the execution of a program and can be made as long as possible.

Figure 24.1 shows a linked list:

![](bbox=[0.341, 0.773, 0.624, 0.809])

**Figure 24.1: Showing the Pictorial View of a Linear Linked List**

To keep track of a linked list, its first element, usually called the start or head, is very important. Linked list allows its elements to be rearranged efficiently. This is done by inserting or deleting the elements from a linked list. Suppose we want to delete the node [B] from the preceding linked list. The next pointer of the item immediately preceding the one to be deleted is altered, and made to point to the item following the deleted item, as shown in Figure 24.2:

![](bbox=[0.341, 0.914, 0.635, 0.95])

**Figure 24.2: Showing the Pictorial View Of Deleting an Element from a Linear Linked List**