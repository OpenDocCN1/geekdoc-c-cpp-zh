Write a program that creates a circular linked list of nodes to determine which position you should stand in to marry the princess if there are no suitors. Your program should simulate the elimination process by deleting the node that corresponds to the suitor that is eliminated for each step in the process. Be careful that you do not leave any memory leaks.

+   6. Modify the `Queue` template class given in Section 17.2 so that it implements a **priority queue**. A priority queue is similar to a regular queue except that each item added to the queue also has an associated priority. For this problem, make the priority an integer where 0 is the highest priority and larger values are increasingly lower in priority.
+   
+   The `remove` function should return and remove the item that has the highest priority. For example,
+   
+   ```cpp
+   q.add('X', 10);
+   q.add('Y', 1);
+   q.add('Z', 3);
+   
+   cout << q.remove(); //Returns Y
+   cout << q.remove(); //Returns Z
+   cout << q.remove(); //Returns X
+   ```
+   
+   Test your queue on data with priorities in various orders (e.g., ascending, descending, mixed). You can implement the priority queue by performing a linear search in the `remove()` function. In future courses, you may study a data structure called a *heap* that provides a more efficient way to implement a priority queue.

+   7. Add a `remove` function, a `cardinality` function, and an iterator for the `Set` class given in Displays 17.28 and 17.29. Write a suitable test program.

+   8. The hash table from Displays 17.24 and 17.25 hashed a string to an integer and stored the same string in the hash table. Modify the program so that instead of storing strings it stores `Employee` objects. Define the `Employee` class so that it contains private string member variables for the combined first and last name, job title, and phone number. Include functions to get and set these member variables. Use the employee name as the input to the hash function. The modification will require changes to the linked list, since the `LinkedList` class created only linked lists of strings. For the most generality, modify the hash table so that it uses generic types. You will also need to add a `get` function to the hash table class that returns the `Employee` object stored in the hash table that corresponds to the input name. The `Employee` class may require defining the `==` and `!=` operators. Test your program by adding and retrieving several names, including names that hash to the same slot in the hash table.

+   9. Displays 17.24 through 17.26 provide the beginnings of a spell-checker. Refine the program to make it more useful. The modified program should read in a text file, parse each word, and determine whether each word is in the hash table and if not