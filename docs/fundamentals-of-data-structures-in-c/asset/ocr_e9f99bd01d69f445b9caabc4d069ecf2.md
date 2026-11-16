```
? 3
The First Polynomial is ...
3.00x^2 + 2.00x^1 + 1.00x^0 = 0
The Second Polynomial is ...
5.00x^1 + 5.00x^0 = 0
? 4
The Resultant Polynomial after Addition is ...
3.00x^2 + 7.00x^1 + 6.00x^0 = 0
? 5
The Resultant Polynomial after Subtraction is ...
3.00x^2 + -3.00x^1 + -4.00x^0 = 0
? 6
The Resultant Polynomial after Multiplication is ...
15.00x^3 + 25.00x^2 + 15.00x^1 + 5.00x^0 = 0
? 7
The Resultant Polynomial after Division is ...
Quotient : 0.60x^1 + -0.20x^0= 0
Remainder : 2.00x^0 = 0
? 8
End of Run of your Program . . .
```

*Program 3.8 is capable of reading input in any sequence, and at the same time, reading input with an exponent value of zero. If you enter the same value of exponent again and again, it will automatically add the co-efficients of same exponent and store it in descending order. You can also change any one of the existing polynomial and manipulate (add, subtract, multiply, divide) the new polynomial with the old polynomial.*

# Advantages of Linked Lists

+   * It is not necessary to specify the number of elements in a linked list during its declaration (since memory can be allocated dynamically when a node is added to the list).
+   * Linked list can grow and shrink in size depending upon the insertion and deletion that occurs in the list.
+   * Insertions and deletions at any place in a list can be handled easily and efficiently.
+   * A linked list does not waste any memory space.

# Disadvantages of Linked Lists

+   * Searching a particular element in a list is difficult and time consuming.
+   * A linked list will use more storage space than an array to store the same number of elements (. . . Each element in a list needs additional memory space for storing the address of the next node).