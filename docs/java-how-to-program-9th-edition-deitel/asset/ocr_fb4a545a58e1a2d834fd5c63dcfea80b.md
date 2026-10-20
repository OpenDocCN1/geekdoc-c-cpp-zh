Method readRecords (lines 30–64) reads and displays records from the file. Line 33 creates AccountRecord object record to store the current record’s information. Lines 35–36 display headers for the columns in the application’s output. Lines 40–51 read data from the file until the end-of-file marker is reached (in which case, method hasNext will return false at line 40). Lines 42–45 use Scanner methods nextInt, next and nextDouble to input an int (the account number), two Strings (the first and last names) and a double value (the balance). Each record is one line of data in the file. The values are stored in object record. If the information in the file is not properly formed (e.g., there’s a last name where there should be a balance), a NoSuchElementException occurs when the record is input. This exception is handled in lines 53–58. If the Scanner was closed before the data was input, an IllegalStateException occurs (handled in lines 59–63). If no exceptions occur, the record’s information is displayed on the screen (lines 48–50). Note in the format string in line 48 that the account number, first name and last name are left justified, while the balance is right justified and output with two digits of precision. Each iteration of the loop inputs one line of text from the text file, which represents one record.

Lines 67–71 define method closeFile, which closes the Scanner. Method main is defined in Fig. 17.10 in lines 6–13. Line 8 creates a ReadTextFile object, which is then used to open, add records to and close the file (lines 10–12).

# 17.4.3 Case Study: A Credit-Inquiry Program

To retrieve data sequentially from a file, programs start from the beginning of the file and read all the data consecutively until the desired information is found. It might be necessary to process the file sequentially several times (from the beginning of the file) during the execution of a program. Class Scanner does not allow repositioning to the beginning of the file. If it’s necessary to read the file again, the program must close the file and reopen it.

The program in Figs. 17.11–17.13 allows a credit manager to obtain lists of customers with zero balances (i.e., customers who do not owe any money), customers with credit balances (i.e., customers to whom the company owes money) and customers with debit balances (i.e., customers who owe the company money for goods and services received). A credit balance is a negative amount, a debit balance a positive amount.

# MenuOption Enumeration

We begin by creating an enum type (Fig. 17.11) to define the different menu options the user will have. The options and their values are listed in lines 7–10. Method getValue (lines 19–22) retrieves the value of a specific enum constant.

```
1  // Fig. 17.11: MenuOption.java
2  // Enumeration for the credit-inquiry program's options.
3
4  public enum MenuOption
5  {
6      // declare contents of enum type
7      ZERO_BALANCE( 1 ),
8      CREDIT_BALANCE( 2 ),
9      DEBIT_BALANCE( 3 ),
10     END( 4 );
```

Fig. 17.11 | Enumeration for the credit-inquiry program’s menu options. (Part 1 of 2.)