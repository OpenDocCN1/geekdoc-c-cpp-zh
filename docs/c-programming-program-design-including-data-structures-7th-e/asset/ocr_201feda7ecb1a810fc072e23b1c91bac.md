```
**Sample Run:** In this sample run, the user input is shaded.

List 3: Enter 5 strings: `hello sunny warm winter summer`
Line 8: stringList: hello sunny warm winter summer
Line 11: Enter the string to be deleted: `hello`
Line 15: After removing hello stringList: sunny warm winter summer
Line 18: Enter the search item: `winter`
Line 22: winter found in stringList.
```

The preceding program works as follows. The statement in Line 1 declares stringList to be an object of the type unorderedArrayListType. The member variable list of stringList is an array of 25 components and the component type is string. The statement in Line 2 declares the string variable str. The statement in Line 3 prompts the user to enter 5 strings. The statement in Line 5 gets the next string from the input stream. The statement in Line 6 uses the member function insertEnd of stringList to store the string into stringList. The statement in Line 9 uses the member function print of stringList to output the elements of stringList. The statement in Line 11 prompts the user to enter the string to be deleted from stringList, and the statement in Line 12 gets the string to be deleted from the input stream. The statement in Line 14 uses the member function remove of stringList to remove the string from stringList. The statement in Line 16 outputs the modified stringList.

The statements in Lines 18 through 24 tests the function seqSearch.

**NOTE:** The Web site accompanying this book contains additional programs illustrating how to use the `class template unorderedArrayListType` to create lists of `double` elements and `clockTyp` objects.

Just as we can derive the `class template unorderedArrayListType`, from the abstract class template `arrayListType`, to manipulate unordered lists, we can also derive the `class template orderedArrayListType` to manipulate ordered lists. (See Programming Exercise 21 at the end of this chapter.)

# QUICK REVIEW

+   1. An operator that has different meanings with different data types is said to be overloaded.
+   2. In C++, `>>` is used as a stream extraction operator and as a right shift operator. Similarly, `<<` is used as a stream insertion operator and as a left shift operator. Both are examples of operator overloading.
+   3. Any function that overloads an operator is called an operator function.
+   4. The syntax of the heading of the operator function is:
+      `returnType operator operatorSymbol(parameters)`