```
```r
$RowB, $SL,
$RowC, $SL,
$RowD, $SL,
$RowF, $SL,
$RowG, $SL,
$RowH, $SL,
$RowI, $SL,
$RowJ,
$DL)));

#Print the table
print $AstroTable;
```
```

In the lines trailing comments #1 and #2 in Listing05_13, you define the data and formatting information that the program uses. After you complete this code, you write no code that cannot be used in a fairly generic way. The goal of this approach to defining formatting for the table involves removing as much detail as possible from the work of constructing the table (an activity that begins with the code associated with comment #3). When you employ scalars to store formatting information, you can, for example, change the width or content of any field of the table, altering only the identifiers you set up in the sections designated by comments #1 and #2. Such isolation of tasks characterizes many programming efforts.

In the code accompanying comment #3, you make use of the identifiers created earlier in the program and no longer use literal text strings, tags, or formatting specifiers. Instead, you make use of the generic components defined in the line associated with comments #1 and #2. Likewise, notice the “Perlism” of leaving the parentheses out of the calls to sprintf(). This practice is probably more common than use of parentheses, but it remains that leaving the parentheses out constitutes (in this context) a programming idiosyncrasy. Ultimately, how easily you can read and maintain your code should determine whether you employ parentheses.

Figure 5.15 illustrates the output of Listing05_13. The lines of code trailing comment #1 serve as what you might view as a set of data retrieved from a database.

In the section of Listing05_13 affiliated with comment #4, you construct the table. The construction of the table might be reduced much further than it is. Use of the row identifiers allows you to see how to construct the table and affords you the chance to add or subtract rows with relative ease. To eliminate a row, just comment it out.