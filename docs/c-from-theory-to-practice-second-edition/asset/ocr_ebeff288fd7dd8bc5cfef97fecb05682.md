if the user enters the string 12, the program should assign the number 12 to a variable. If the user enters the string -1.234 the assigned value should be -1.234.

# U.10.20

Write a program that reads 20 strings (less than 100 characters each) and stores them in a two-dimensional array. Then, the program should read a string, and if it is found in the array, it should be removed. To remove the string, move the strings below that point one row up. In the place of the last row moving up, insert the null character. For example, if the array is:

```
one
two
three
four
...
```

and the user enters two, the new content should be:

```
one
three
four
...
```

# U.10.21

Write a program that reads 20 strings (less than 100 characters each) and stores them in a two-dimensional array. Then, the program should:

a. Read a column number and display the words that are contained in that column, including those that consist of a single character. In an example with five strings, if the user enters:

```
abcdegm
abcd fpoo
abcd
abc
abcdkmop
```

and the number 6 as column, the program should display:

```
word_1: gp
word_2: m
```

b. Read a row number, except the first one, and if the string in that row contains less than five different lowercase letters, the program should swap that string with the string in the first row.

# U.10.22

Write a program that reads the names of 20 bookstores and 500 book titles. Use two two-dimensional arrays to store them. Assume that all names are less than 100 characters. The program should also read for each bookstore the number of copies left in stock for each title. Then, the program should read a book title and display the names of the bookstores that offer this title and the number of copies of that title in those bookstores. Finally, the program should read the name of a bookstore and display its total number of copies left in stock.