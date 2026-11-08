+   24. Suppose that queue is implemented as an array with the special reserved slot, as described in this chapter. Suppose that the size of the array implementing queue is 100. Also, suppose that the value of `queueFront` is 74 and the value of `queueRear` is 99.
+   
+      a. What are the values of `queueFront` and `queueRear` after adding an element to queue?
+   
+      b. What are the values of `queueFront` and `queueRear` after removing an element from queue? Also, what is the position of the removed queue element?

+   25. Write a function template, `reverseStack`, that takes as a parameter a stack object and uses a queue object to reverse the elements of the stack.

+   26. Write a function template, `reverseQueue`, that takes as a parameter a queue object and uses a stack object to reverse the elements of the queue.

+   27. Add the operation `queueCount` to the class `queueType` (the array implementation of queues), which returns the number of elements in the queue. Write the definition of the function template to implement this operation.

+   28. Draw the UML class diagram of the class `linkedStackType`.

+   29. Draw the UML class diagram of the class `queueADT`.

+   30. Draw the UML class diagram of the class `queueType`.

+   31. Draw the UML class diagram of the class `linkedQueueType`.

# PROGRAMMING EXERCISES

+   1. Two stacks of the same type are the same if they have the same number of elements and their elements at the corresponding positions are the same. Overload the relational operator `==` for the class `stackType` that returns true if two stacks of the same type are the same; it returns false otherwise. Also, write the definition of the function template to overload this operator.

+   2. Repeat Programming Exercise 1 for the class `linkedStackType`.

+   3. a. Add the following operation to the class `stackType`:
+   
+      ```cpp
+      void reverseStack(stackType<Type>& otherStack);
+      ```
+   
+      This operation copies the elements of a stack in reverse order onto another stack.
+   
+      Consider the following statements:
+   
+      ```cpp
+      stackType<int> stack1;
+      stackType<int> stack2;
+      ```
+   
+      The statement:
+   
+      ```cpp
+      stack1.reverseStack(stack2);
+      ```