+   6. Change the representation of Link and List from $27.9 without changing the user interface provided by the functions. Allocate Links in an array of links and have the members first, last, pre, and suc be ints (indices into the array).

+   7. What are the advantages and disadvantages of intrusive containers compared to C++ standard (non-intrusive) containers? Make lists of pros and cons.

+   8. What is the lexicographical order on your machine? Write out every character on your keyboard together with its integer value; then, write the characters out in the order determined by their integer value.

+   9. Using only C facilities, including the C standard library, read a sequence of words from stdin and write them to stdout in lexicographical order. Hint: The C sort function is called qsort(); look it up somewhere. Alternatively, insert the words into an ordered list as you read them. There is no C standard library list.

+   10. Make a list of C language features adopted from C++ or C with Classes ($27.1).

+   11. Make a list of C language features not adopted by C++.

+   12. Implement a (C-style string, int) lookup table with operations such as find(struct table*, const char*), insert(struct table*, const char*, int), and remove(struct table*, const char*). The representation of the table could be an array of a struct pair or a pair of arrays (const char*[]) and int*); you choose. Also choose return types for your functions. Document your design decisions.

+   13. Write a program that does the equivalent of string s; cin>>s; in C; that is, define an input operation that reads an arbitrarily long sequence of whitespace-terminated characters into a zero-terminated array of chars.

+   14. Write a function that takes an array of ints as its input and finds the smallest and the largest elements. It should also compute the median and mean. Use a struct holding the results as the return value.

+   15. Simulate single inheritance in C. Let each “base class” contain a pointer to an array of pointers to functions (to simulate virtual functions as free-standing functions taking a pointer to a “base class” object as their first argument); see $27.2.3. Implement “derivation” by making the “base class” the type of the first member of the derived class. For each class, initialize the array of “virtual functions” appropriately. To test the ideas, implement a version of “the old Shape example” with the base and derived draw() just printing out the name of their class. Use only language features and library facilities available in standard C.

+   16. Use macros to obscure (simplify the notation for) the implementation in the previous exercise.