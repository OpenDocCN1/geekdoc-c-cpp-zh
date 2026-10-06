# Sequence Structures

It was mentioned earlier that the statements in Program 2-1 execute in the order that they appear, from the top of the program to the bottom. A set of statements that execute in the order that they appear is called a sequence structure. In fact, all of the programs you see in this chapter are sequence structures.

A structure, also called a control structure, is a logical design that controls the order in which a set of statements executes. In the 1960s, a group of mathematicians proved that only three program structures are needed to write any type of program. The simplest of these structures is the sequence structure—decision structures and repetition structures.

# Strings and String Literals

Programs almost always work with data of some type. For example, Program 2-1 uses the following three pieces of data:

+   * Kate Austen
* 1234 Walnut Street
* Asheville, NC 28899"

These pieces of data are sequences of characters. In programming terms, a sequence of characters that is used as data is called a string. When a string appears in the actual code of a program (or in pseudocode, as it does in Program 2-1) it is called a literal. In program, or pseudocode, a string literal is usually enclosed in quotation marks. As mentioned earlier, the quotation marks mark where the string begins and ends.

In this book, we will always enclose string literals in double quote marks ("). Most programming languages use this same convention, but a few use single quote marks ('').

# Variables and Input

![](bbox=[0.128, 0.631, 0.203, 0.686])

Often a program needs to store data in the computer's memory so it can perform operations on data. For example, consider the typical online shopping experience: You browse a site and add the items that you want to purchase to the shopping cart. As you add items to the shopping cart, data about those items is stored in memory. Then, when you click the checkout button, a program on the Web calculates the total of all the items you have in your shopping cart, applicable sales taxes, shipping costs, and the total of all these charges. When the program performs these calculations, it stores the results in the computer's memory.

Programs use variables to store data in memory. A variable is a storage location in memory that is referenced by a name. For example, a program that calculates the sales on a purchase might use a variable tax to hold that value in memory. And a program that calculates the distance from Earth to a star might use a variable named distance to hold that value in memory.

In this section, we will discuss basic input operation: reading data that has been typed on the keyboard. When a program reads data from the keyboard, it usually stores data in a variable so it can be used later by the program. In pseudocode we will read