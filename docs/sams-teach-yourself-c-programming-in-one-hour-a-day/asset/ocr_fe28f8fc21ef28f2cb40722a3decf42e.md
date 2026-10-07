# Q&A

Why are pointers give you more control over the computer and your data. When used with functions, pointers enable you to change the values of variables that were passed, regardless of where they originated. In Lesson 15 and Lesson 16, “Pointers to Functions and Linked Lists,” you learn additional uses for pointers.

How does the compiler know the difference between * for multiplication, for dereferencing, and for declaring a pointer?

The compiler interprets the different uses of the asterisk based on the context in which it is used. If the statement being evaluated starts with a variable type, it can be assumed that the asterisk is for declaring a pointer. If the asterisk is used with a variable that has been declared as a pointer, but not in a variable declaration, the asterisk is assumed to dereference. If it is used in a mathematical expression, but not with a pointer variable, the asterisk can be assumed to be the multiplication operator.

What happens if I use the address-of operator on a pointer?

You get the address of the pointer variable. Remember, a pointer is just another variable that holds the address of the variable to which it points.

Are variables always stored in the same location?

No. Each time a program runs, its variables can be stored at different addresses within the computer. You should never assign a constant address value to a pointer.

# Workshop

The Workshop provides quiz questions to help you solidify your understanding of the material covered and exercises to provide you with experience in using what you’ve learned.

# Quiz

+   1. What operator is used to determine the address of a variable?
2. What operator is used to determine the value at the location pointed to by a pointer?
3. What is a pointer?
4. What is indirection?
5. How are the elements of an array stored in memory?