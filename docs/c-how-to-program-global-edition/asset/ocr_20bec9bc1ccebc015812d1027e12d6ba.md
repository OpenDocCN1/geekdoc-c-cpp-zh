```
int isEmpty(StackNodePtr topPtr)
Determine whether the stack is empty.
```

```
void printStack(StackNodePtr topPtr)
Print the stack.
```

# 12.14 (Postfix Evaluator Modification)

Modify the postfix evaluator program of Exercise 12.13 so that it can process integer operands larger than 9.

# 12.15 (Supermarket Simulation)

Write a program that simulates a check-out line at a supermarket. The line is a queue. Customers arrive in random integer intervals of 1 to 4 minutes. Also, each customer is serviced in random integer intervals of 1 to 4 minutes. Obviously, the rates need to be balanced. If the average arrival rate is larger than the average service rate, the queue will grow infinitely. Even with balanced rates, randomness can still cause long lines. Run the supermarket simulation for a 12-hour day (720 minutes) using the following algorithm:

+   1) Choose a random integer between 1 and 4 to determine the minute at which the first customer arrives.
+   2) At the first customer's arrival time:
+      Determine customer's service time (random integer from 1 to 4);
+      Begin servicing the customer;
+      Schedule arrival time of next customer (random integer 1 to 4 added to the current time).
+   3) For each minute of the day:
+      If the next customer arrives,
+        Say so;
+        Enqueue the customer;
+        Schedule the arrival time of the next customer.
+      If service was completed for the last customer,
+        Say so;
+        Dequeue next customer to be serviced;
+        Determine customer's service completion time (random integer from 1 to 4 added to the current time).

Now run your simulation for 720 minutes and answer each of the following:

+   a) What's the maximum number of customers in the queue at any time?
+   b) What's the longest wait any one customer experienced?
+   c) What happens if the arrival interval is changed from 1 to 4 minutes to 1 to 3 minutes?

# 12.16 (Allowing Duplicates in a Binary Tree)

Modify the program of Fig. 12.19 to allow the binary tree to contain duplicate values.

# 12.17 (Binary Search Tree of Strings)

Write a program based on the program of Fig. 12.19 that inputs a line of text, tokenizes the sentence into separate words, inserts the words in a binary search tree, and prints the in-order, pre-order, and post-order traversals of the tree.

[Hint: Read the line of text into an array. Use strtok to tokenize the text. When a token is found, create a new node for the tree, assign the pointer returned by strtok to member string of the new node, and insert the node in the tree.]

# 12.18 (Duplicate Elimination)

We've seen that duplicate elimination is straightforward when creating a binary search tree. Describe how you would perform duplicate elimination using only a one-dimensional array. Compare the performance of array-based duplicate elimination with the performance of binary-search-tree-based duplicate elimination.

# 12.19 (Depth of a Binary Tree)

Write a function depth that receives a binary tree and determines how many levels it has.