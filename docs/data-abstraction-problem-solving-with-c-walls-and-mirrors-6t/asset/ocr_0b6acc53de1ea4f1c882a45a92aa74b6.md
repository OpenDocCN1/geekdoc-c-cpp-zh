c. The hash table is 10,000 entries long. The search keys are integers in the range 0 through 9999. The hash function is
h(key) = (key * random) truncated to an integer
where random represents a sophisticated random-number generator that returns a real value between
0 and 1.
d. The hash table is 10,000 entries long (HASH_TABLE_SIZE is 10000). The search keys are integers in the
range 0 through 9999. The hash function is given by the following C++ function:
int hashIndex(int x)
{
    for (int i = 1; i <= 1000000; i++)
        x = (x * x) % HASH_TABLE_SIZE;
    return x;
} // end hashIndex

# PROGRAMMING PROBLEMS

+   1. Complete the implementation of the class ArrayDictionary as given in Listing 18-3.
+   2. Complete the implementation of the class TreeDictionary as given in Listing 18-4.
+   3. Write the sorted link-based, unsorted array-based, and unsorted link-based implementations of the ADT dictionary described in this chapter.
+   4. Write unsorted and sorted implementations of the ADT dictionary that use, respectively, the ADTs list and sorted list, which Chapters 8 and 12 described.
+   5. Repeat Programming Problem 5 of Chapter 16, using the ADT dictionary as the database.
+   6. Develop a program that can be used to test an implementation of the ADT dictionary.
+   7. Implement the symbol table described in Exercise 5 by reusing the class TreeDictionary, as described in Section 18.2.2 of this chapter.
+   8. Consider any collection of data that you can organize in at least two ways. For example, you can order employees by name or by Social Security number and books by title or by author. Note that other information about the employees or books is present in the database but is not used to organize these items. This program assumes that the search keys (for example, book title or book author) are unique and are strings. Thus, in the previous examples, the Social Security number must be a string instead of an integer, and only one book per author is permitted. Choose any set of data that conforms to these requirements, and create a text file.
+   
+   Program behavior. When your program begins execution, it should read your text file. If then should provide some typical database management operations, all under user control via an interface of your design. For example, you should be able to add an item, remove an item, display (that is, retrieve) an item, and display all of the items in search-key order. You should be able to use either of two search keys to designate the item to be removed or displayed.
+   
+   Implementation notes. The items in the database should be objects that contain two search keys and additional data, all of which appear in the text file. Thus, you need to design and implement a class of these objects.
+   
+   Although your program could create two dictionaries from these objects—one organized by one search key (such as the employee name) and the other organized by another search key (such as the Social Security number)—this approach could waste a substantial amount of memory due to the duplication of all of the data in both dictionaries.