# **PROGRAMMING PROJECTS**
For more in-depth projects, please see www.cs.colorado.edu/~main/projects/

+   1. Reimplement the binary search using a loop and no recursion. If you are familiar with template functions, then your implementation should be a template function that can search any array that is sorted from smallest to largest (using the < operator).

+   2. Use a binary search technique to rewrite the guess_game function from Figure 14.1 on page 24. The function may ask questions such as “Is your number bigger than 42?” Your result should have worst-case time of O(log n).

+   3. Use double hashing to reimplement the hash table from Figure 12.4 on page 604.

+   4. In our open-address hash tables, we have used linear probing or double hashing. Another probing method, which avoids some clustering, is called quadratic probing. The simplest version of quadratic probing works like this: Start by hashing the key to an array index. If there is a collision, then move to the next array index. If there is a second collision, then move forward two more spots through the array. After a third collision, we move forward three more spots, and so on. For example, suppose that a new key hashes to location 327, and this location is full. The next location that we try is 328. If 328 is a second collision, then we move two spots forward to location 330. If 330 is a third collision, then we move three spots forward to location 333. If our calculation of the next spot takes us beyond the end of the array, then we “wrap around” to the front of the array. In general, if data[i] is the location that has just caused a collision, and we have already examined collision elements, then we increase i according to the assignment:
+   
+   i = (i + count) % CAPACITY;
+   
+   In this formula, the “% CAPACITY” causes the “wraparound” to the front of the array. In order for this approach to work correctly, the capacity must be a power of 2, such as 2^10 = 1024. Otherwise, the sequence of probes does not correctly examine all array items.
+   
+   For this project, use quadratic hashing to reimplement the hash table from Figure 12.4 on page 604.

+   5. Implement a dictionary program using a table. The user inputs a word, and the word’s vice definition is displayed. You will need to revise one of the table implementations to use a string as the search key. Use a hash function similar to the one you implemented for Self-Test Exercise 28.

+   6. Redo Programming Problem 12 of Chapter 10 to allow the user to search for books using the ISBN, book title, or author search key. One way to accomplish this would be to create a separate hash table of book objects for each search key; however, this would result in duplicated data and wasted memory. A better implementation would be to store the actual data in a list, and use separate hash tables for each search key. The value associated with each key is not the book itself, but just the position of the book in the book list of books. Assume that there are no duplicates in the search keys.

+   7. Design a scheme that allows for duplicate keys in the previous project.

+   8. Rewrite one of your hash tables so that it has additional member functions to provide statistics. You should include functions to calculate the load factor, the average number of items examined during a successful search, and the maximum number of items examined during a successful search. Find a large collection of information to put in your hash table, perhaps the list of users at your computing site. Test how the statistics vary based on the capacity of the hash table.