Each book record is made up of the following fields: `Book Title`, `Author`, `Price`, and `Book Category`. Note the following example records, each made up of four lines:

```
Heidi
Spyri
55.00
Children's

----------------------------------------

Hawaii
Michener
6.95
Fiction
```

Input records for a control break program are usually stored in a data file on a storage device, such as a disk, and the records are sorted according to a predetermined control break variable. For example, the control break variable for this program is `category`, so the input records would be sorted according to category. You have not yet learned about reading data from an input file, so for this program the input will continue to be interactive. You will learn about reading input data from a file in the next chapter.

Figure 8-2 includes the pseudocode for the Bookstore program and Figure 8-3 includes the C++ code that implements the program.

```
start
    string title
    string author
    string category
    num price
    string HEADING = "BOOK LIST"
    string FOOTER = "Total number of book titles "
    string CATEGORY_FOOTER = "Category count "
    num grandTotal = 0
    string prevCategory
    num categoryTotal = 0
    print HEADING
    get title, author, category, price
    prevCategory = category
    while not eof
        if category not = prevCategory then
            grandTotal = categoryChange(categoryTotal, grandTotal)
            categoryTotal = 0
            prevCategory = category
        endif
        categoryTotal = categoryTotal + 1
        print title
        get title, author, category, price
```

**Figure 8-2** Bookstore program pseudocode