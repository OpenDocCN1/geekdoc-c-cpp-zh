+   3. The variables `sum`, `rainfall`, and `average` should be declared to be what data type to calculate the most accurate average rainfall?
+   
+   4. Could you replace `DAYS_IN_WEEK` in the statement `average = sum / DAYS_IN_WEEK;` with the variable named `counter` and still get the desired result? Explain.

# ## LAB 5-6: ACCUMULATING TOTALS IN A LOOP

In this lab, you add a statement to a loop body in a C++ program provided with the data files for this book. When completed, the statement you add should calculate the total daily sales for a book store. The loop executes until the user enters the word “done” instead of a book title. After the user enters a book title, he or she is asked to enter the transaction amount. The transaction amounts are listed in Table 5-1.

> > **NOTE**
> >
> > This program uses a C++ function, `cin.ignore()`, that you have not yet learned about. You will learn about `cin.ignore()` in Chapter 6.

> > **NOTE**
> >
> > When entering the transaction amount data, do not type the $.

| Book Title | Transaction Amount |
|---|---|
| Harry Potter and the Deathly Hallows | $17.99 |
| A Thousand Splendid Suns | $14.99 |
| The Dangerous Book for Boys | $14.99 |
| Eat, Pray, Love | $ 9.00 |
| Marley and Me | $14.99 |
| The Tipping Point | $ 8.99 |
| Fahrenheit 451 | $ 4.99 |

Table 5-1 Input for Lab 5-6

Note that variables have been declared for you and the input statements and all but one output statement have been written. In this lab, you will add the output statement that displays the bookstore’s total daily sales and you will calculate a total of daily sales for the bookstore.

+   1. Open the source code file named `BookSales.cpp` using Notepad or the text editor of your choice.
+   
+   2. Add a statement to the loop body that allows you to calculate a total of daily sales for the bookstore.
+   
+   3. Save this source code file in a directory of your choice and then make that directory your working directory.