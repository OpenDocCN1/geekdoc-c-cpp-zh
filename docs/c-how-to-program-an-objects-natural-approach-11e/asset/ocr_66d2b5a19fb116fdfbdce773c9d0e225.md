+   c) Use the ______ algorithm (header `<numeric>`) to sum the values in a range.
+   
+   d) Use the ______ algorithm to apply a general function to every element in a range when you need to modify those elements.
+   
+   e) The `binary_search` algorithm requires that the sequence of values must be ______.
+   
+   f) Use the function `iter_swap` to exchange the elements that are pointed to by two ______ iterators and exchanges the values in those elements.
+   
+   g) The two-argument `minmax` algorithm returns a(n) ______ in which the smaller item is stored in first, and the larger item is stored in second.
+   
+   h) ______ algorithms modify the containers they operate on.

**14.6** List several advantages function objects provide over function pointers.

**14.7** What happens when you apply the unique algorithm to a sorted sequence of elements in a range?

**14.8**  *(Duplicate Elimination)* Read 20 integers into an array. Next, sort the array, then use the `unique` algorithm to reduce the array to the unique values entered by the user. Use the `copy` algorithm to display the unique values.

**14.9**  *(Duplicate Elimination)* Modify Exercise 14.8 to use the `unique_copy` algorithm. Insert the unique values into a vector that's initially empty. Use a `back_inserter` to grow the vector as new values are added. Use the `copy` algorithm to display the unique values.

**14.10**  *(Reading Data from a File)* Use an `istream_iterator<int>`, the `copy` algorithm and a `back_inserter` to read the contents of a text file that contains int values separated by whitespace. Place the int values into a vector of ints. The first argument to the `copy` algorithm should be the `istream_iterator<int>` object that's associated with the text file's ifstream object. The second argument should be an `istream_iterator<int>` object that's initialized using the class template `istream_iterator`'s default constructor—the resulting object can be used as an “end” iterator. After reading the file's contents, display the contents of the resulting vector.

**14.11**  *(Merging Ordered Lists)* Write a program that uses standard library algorithms to merge two ordered lists of strings into a single ordered list of strings, then displays the resulting list.

**14.12**  *(Palindrome Tester)* A palindrome is a string that is spelled the same way forward and backward. Examples of palindromes include “radar” and “able was i ere i saw elba.” Write a function `palindromeTester` that uses the `reverse` algorithm on a copy of a string, then compares the original string and the reversed string to determine whether the original string is a palindrome. Like the standard library containers, string objects are ranges. Assume that the original string contains all lowercase letters and does not contain any punctuation. Use function `palindromeTester` in a program.

**14.13**  *(Enhanced Palindrome Tester)* Enhance Exercise 14.12's `palindromeTester` function to allow strings containing uppercase and lowercase letters and punctuation. Before testing whether the original string is a palindrome, function `palindromeTester` should convert the string to lowercase letters and eliminate any punctuation. For simplicity, assume the only punctuation characters can be

`, . ! ; : ( )`