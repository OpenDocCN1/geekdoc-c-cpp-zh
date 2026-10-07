# 154 Learning SAS by Example: A Programmer's Guide, Second Edition

other characters.) The INPUT function takes the first argument (a character variable), and applies the informat in the second argument, resulting in a numeric variable.

A clever alternative (inspired by a good friend, Mike Zdeb) is to use the comma directly in the INPUT function. It is not commonly known that this informat not removes commas and dollar signs when reading a value, it also removes dashes. You can therefore use the COMMA11, informat in the INPUT function directly without having to remove the dashes. You can now merge data sets Division1 and Division2N as before. We will not bother to show you a listing of the result—it contains a numeric variable called SS.

# 10.14 One-to-One, One-to-Many, and Many-to-Many Merges

In the examples shown previously, there was only one observation for each value of the BY variable in both data sets. This is called a one-to-one merge. You may have a situation where one data set has only one observation for each value of the BY variable, but the other has many observation for each value of the BY variable. This is referred to as a one-to-many merge. As an example, suppose you want to merge data set Bert with a data set with multiple values of ID. To demonstrate this, take a look at the following two data sets:

Figure 10.20: Listing of Data Sets Bert and Oscar

| Listing of Data Set Bert | Listing of Data Set Oscar |
| ID | X | ID | Y |
| 123 | 90 | 123 | 200 |
| 222 | 95 | 123 | 250 |
| 333 | 100 | 222 | 205 |
| | | 333 | 317 |
| | | 333 | 400 |
| | | 333 | 500 |

Notice that data set Oscar has multiple observations with the same ID. What happens when you perform a merge? The resulting data set is shown next: