+   d) function pop that pops a value off the stack
+    e) function isEmpty that determines if the stack is empty
+    f) function printStack that prints the stack

# **20.14** *(Postfix Evaluation Enhanced)*

Modify the postfix evaluator program of Exercise 20.13 so that it can process integer operands larger than 9.

# **20.15** *(Supermarket Simulation)*

Write a program that simulates a checkout line at a supermarket. The line is a queue object. Customers (i.e., customer objects) arrive in random integer intervals of 1–4 minutes. Also, each customer is served in random integer intervals of 1–4 minutes. Obviously, the rates need to be balanced. If the average arrival rate is larger than the average service rate, the queue will grow infinitely. Even with “balanced” rates, randomness can still cause long lines. Run the supermarket simulation for a 12-hour day (720 minutes) using the following algorithm:

+   1) Choose a random integer between 1 and 4 to determine the minute at which the first customer arrives.
+   2) At the first customer’s arrival time:
+      - Determine customer’s service time (random integer from 1 to 4);
+      - Begin servicing the customer;
+      - Schedule arrival time of next customer (random integer 1 to 4 added to the current time).
+   3) For each minute of the day:
+      - If the next customer arrives,
+        - Say so,
+        - Enqueue the customer,
+        - Schedule the arrival time of the next customer;
+      - If service was completed for the last customer,
+        - Say so,
+        - Dequeue next customer to be serviced,
+        - Determine customer’s service completion time
+          (random integer from 1 to 4 added to the current time).

Now run your simulation for 720 minutes, and answer each of the following:

+   a) What’s the maximum number of customers in the queue at any time?
+   b) What’s the longest wait any one customer experiences?
+   c) What happens if the arrival interval is changed from 1–4 minutes to 1–3 minutes?

**20.16** *(Allowing Duplicates in Binary Trees)* Modify the program of Figs. 20.20–20.22 to allow the binary tree object to contain duplicate values.

**20.17** *(Binary Tree of Strings)* Write a program based on Figs. 20.20–20.22 that inputs a line of text, tokenizes the sentence into separate words (you may want to use the `istringstream` library class), inserts the words in a binary search tree and prints the inorder, preorder and postorder traversals of the tree. Use an OOP approach.

**20.18** *(Duplicate Elimination)* In this chapter, we saw that duplicate elimination is straightforward when creating a binary search tree. Describe how you’d perform duplicate elimination using only a one-dimensional array. Compare the performance of array-based duplicate elimination with the performance of binary-search-tree-based duplicate elimination.

**20.19** *(Depth of a Binary Tree)* Write a function that receives a binary tree and determines how many levels it has.

**20.20** *(Recursively Print a List Backward)* Write a member function `printListBackward` that recursively outputs the items in a linked list object in reverse order. Write a test program that creates a sorted list of integers and prints the list in reverse order.