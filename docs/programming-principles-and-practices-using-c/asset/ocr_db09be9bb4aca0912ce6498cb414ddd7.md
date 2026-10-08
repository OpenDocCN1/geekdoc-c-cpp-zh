+   6. Add operators for the **Book** class. Have the `==` operator check whether the ISBN numbers are the same for two books. Have `!=` also compare the ISBN numbers. Have a `<<` print out the title, author, and ISBN on separate lines.

+   7. Create an enumerated type for the **Book** class called **Genre**. Have the types be fiction, nonfiction, periodical, biography, and children. Give each book a **Genre** and make appropriate changes to the **Book** constructor and member functions.

+   8. Create a **Patron** class for the library. The class will have a user's name, library card number, and library fees (if owed). Have functions that access this data, as well as a function to set the fee of the user. Have a helper function that returns a Boolean (**bool**) depending on whether or not the user owes a fee.

+   9. Create a **Library** class. Include vectors of **Books** and **Patrons**. Include a **struct** called **Transaction**. Have it include a **Book**, a **Patron**, and a **Date** from the chapter. Make a vector of **Transactions**. Create functions to add books to the library, add patrons to the library, and check out books. Whenever a user checks out a book, have the library make sure that both the user and the book are in the library. If they aren't, report an error. Then check to make sure that the user owes no fees. If the user does, report an error. If not, create a **Transaction**, and place it in the vector of **Transactions**. Also write a function that will return a vector that contains the names of all **Patrons** who owe fees.

+   10. Implement **leapyear()** from §9.8.

+   11. Design and implement a set of useful helper functions for the **Date** class with functions such as **next\_workday()** (assume that any day that is not a Saturday or a Sunday is a workday) and **week\_of\_year()** (assume that week 1 is the week with January 1 in it and that the first day of a week is a Sunday).

+   12. Change the representation of a **Date** to be the number of days since January 1, 1970 (known as day 0), represented as a **long int**, and re-implement the functions from §9.8. Be sure to reject dates outside the range we can represent that way (feel free to reject days before day 0, i.e., no negative days).

+   13. Design and implement a rational number class, **Rational**. A rational number has two parts: a numerator and a denominator, for example, 5/6