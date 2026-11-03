
### Section 11.8 Reading Data from a Random-Access File

- Function `fread` reads a specified number of bytes from a file into memory.
- Function `fread` can be used to read several fixed-size array elements by providing a pointer to the array in which the elements will be stored and by indicating the number of elements to be read.
- Function `fread` returns the number of items it successfully input. If this number is less than the third argument in the function call, then a read error occurred.

## Self-Review Exercises

11.1 Fill in the blanks in each of the following:

- a) Function ______ closes a file.
- b) The ______ function reads data from a file in a manner similar to how `scanf` reads from `stdin`.
- c) Function ______ reads a character from a specified file.
- d) Function ______ reads a line from a specified file.
- e) Function ______ opens a file.
- f) Function ______ is normally used when reading data from a file in random-access applications.
- g) Function ______ repositions the file position pointer to a specific location in the file.

11.2 State which of the following are true and which are false. If false, explain why.

- a) Function `fscanf` cannot be used to read data from the standard input.
- b) You must explicitly use `fopen` to open the standard input, standard output and standard error streams.
- c) A program must explicitly call function `fclose` to close a file.
- d) If the file position pointer points to a location in a sequential file other than the beginning of the file, the file must be closed and reopened to read from the beginning of the file.
- e) Function `fprintf` can write to the standard output.
- f) Data in sequential-access files is always updated without overwriting other data.
- g) It's not necessary to search through all the records in a random-access file to find a specific record.
- h) Records in random-access files are not of uniform length.
- i) Function `fseek` may seek only relative to the beginning of a file.

11.3 Write a single statement to accomplish each of the following. Assume that each of these statements applies to the same program.

- a) Write a statement that opens the file `"oldmast.dat"` for reading and assigns the returned file pointer to `ofPtr`.
- b) Write a statement that opens the file `"trans.dat"` for reading and assigns the returned file pointer to `tfPtr`.
- c) Write a statement that opens the file `"newmast.dat"` for writing (and creation) and assigns the returned file pointer to `nfPtr`.
- d) Write a statement that reads a record from the file `"oldmast.dat"`. The record consists of integer `accountNum`, string `name` and floating-point `currentBalance`.
- e) Write a statement that reads a record from the file `"trans.dat"`. The record consists of the integer `accountNum` and floating-point `dollarAmount`.
- f) Write a statement that writes a record to the file `"newmast.dat"`. The record consists of the integer `accountNum`, string `name` and floating-point `currentBalance`.

11.4 Find the error in each of the following program segments and explain how to correct it.

- a) The file referred to by `fPtr` (`"payables.dat"`) has not been opened.

    ```
    printf(fPtr, "%s%d%f\n", account, company, amount);
    ```

- b)

    ```
    open("receive.dat", "r+");
    ```

- c) The following statement should read a record from the file "payables.dat". File pointer payPtr refers to this file, and file pointer recPtr refers to the file "receive.dat":

    ```
    scanf(recPtr, "%d%s%d\n", &account, company, &amount);
    ```

- d) The file "tools.dat" should be opened to add data to the file without discarding the current data.

    ```
    if ((fPtr = fopen("tools.dat", "w")) != NULL)
    ```

- e) The file "courses.dat" should be opened for appending without modifying the current contents of the file.

    ```
    if ((fPtr = fopen("courses.dat", "ws")) != NULL)
    ```

## Answers to Self-Review Exercises

11.1 a) fclose. b) fscanf. c) fgetc. d) fgets. e) fopen. f) fread. g) fseek.

11.2 a) False. Function fscanf can be used to read from the standard input by including the pointer to the standard input stream, stdin, in the call to fscanf.

- b) False. These three streams are opened automatically by C when program execution begins.
- c) False. The files will be closed when program execution terminates, but all files should be explicitly closed with fclose.
- d) False. Function rewind can be used to reposition the file position pointer to the beginning of the file.
- e) True.
- f) False. In most cases, sequential file records are not of uniform length. Therefore, it's possible that updating a record will cause other data to be overwritten.
- g) True.
- h) False. Records in a random-access file are normally of uniform length.
- i) False. It's possible to seek from the beginning of the file, from the end of the file and from the current location in the file.

11.3 a) ofPtr = fopen("oldmast.dat", "r");

## Exercises

11.5 Fill in the blanks in each of the following:

- a) Computers store large amounts of data on secondary storage devices as ________.
- b) A(n) ________ is composed of several fields.
- c) To facilitate the retrieval of specific records from a file, one field in each record is chosen as a(n) ________.
- d) A group of related characters that conveys meaning is called a(n) ________.
- e) The file pointers for the three streams that are opened automatically when program execution begins are named ________, ________, and ________.
- f) Function ________ writes a character to a specified file.
- g) Function ________ writes a line to a specified file.
- h) Function ________ is generally used to write data to a random-access file.
- i) Function ________ repositions the file position pointer to the beginning of the file.

11.6 State which of the following are true and which are false. If false, explain why.

- a) The impressive functions performed by computers essentially involve the manipulation of zeros and ones.
- b) People prefer to manipulate bits instead of characters and fields because bits are more compact.
- c) People specify programs and data items as characters; computers then manipulate and process these characters as groups of zeros and ones.
- d) A person's zip code is an example of a numeric field.
- e) Data items processed by a computer form a data hierarchy in which data items become larger and more complex as we progress from fields to characters to bits, and so on.
- f) A record key identifies a record as belonging to a particular field.
- g) Most companies store their information in a single file to facilitate computer processing.
- h) Files are always referred to by name in C programs.
- i) When a program creates a file, the file is automatically retained by the computer for future reference.

### 11.7 (Creating Data for a File-Matching Program)

Write a simple program to create some test data for checking out the program of Exercise 11.8. Use the following sample account data:

Master File:

| Account number | Name | Balance |
|---|---|---|
| 100 | Alan Jones | 348.17 |
| 300 | Mary Smith | 27.19 |
| 500 | Sam Sharp | 0.00 |
| 700 | Suzy Green | -14.22 |

Transaction File:

| Account number | Dollar amount |
|---|---|
| 100 | 27.14 |
| 300 | 62.11 |
| 400 | 100.56 |
| 900 | 82.17 |

### 11.8 (File Matching)

Exercise 11.3 asked the reader to write a series of single statements. Actually, these statements form the core of an important type of file-processing program, namely, a file-matching program. In commercial data processing, it's common to have several files in each system.

In an accounts receivable system, for example, there's generally a master file containing detailed information about each customer such as the customer's name, address, telephone number, outstanding balance, credit limit, discount terms, contract arrangements and possibly a condensed history of recent purchases and cash payments.

As transactions occur (i.e., sales are made and cash payments arrive in the mail), they're entered into a file. At the end of each business period (i.e., a month for some companies, a week for others and a day in some cases) the file of transactions (called "trans.dat" in Exercise 11.3) is applied to the master file (called "oldmast.dat" in Exercise 11.3), thus updating each account's record of purchases and payments. After each of these updates runs, the master file is rewritten as a new file ("newmast.dat"), which is then used at the end of the next business period to begin the processing again.

File-matching programs must deal with certain problems that do not exist in single-file programs. For example, a match does not always occur. A customer on the master file might have made any purchases or cash payments in the current business period, and therefore no record for this customer will appear on the transaction file. Similarly, a customer who did make some purchases or cash payments might have just moved to this community, and the company may not have had a chance to create a master record for this customer.

Use the statements written in Exercise 11.3 as the basis for a complete file-matching accounts receivable program. Use the account number on each file as the record key for matching purposes. Assume that each file is a sequential file with records stored in increasing account-number order.

When a match occurs (i.e., records with the same account number appear on both the master file and the transaction file), add the dollar amount on the transaction file to the current balance on the master file and write the "newmast.dat" record. (Assume that purchases are indicated by positive amounts on the transaction file, and that payments are indicated by negative amounts.)

When there's a master record for a particular account but no corresponding transaction record, merely write the master record to "newmast.dat". When there's a transaction record but no corresponding master record, print the message "Unmatched transaction record for account number ..." (fill in the account number from the transaction record).

### 11.9 (Testing the File-Matching Exercises)

Run the program of Exercise 11.8 using the files of test data created in Exercise 11.7. Check the results carefully.

### 11.10 (File Matching with Multiple Transactions)

It's possible (actually common) to have several transaction records with the same record key. This occurs because a particular customer might make several purchases and cash payments during a business period. Rewrite your accounts receivable file-matching program of Exercise 11.8 to provide for the possibility of handling several transaction records with the same record key. Modify the test data of Exercise 11.7 to include the following additional transaction records:

| Account number | Dollar amount |
|---|---|
| 300 | 83.89 |
| 700 | 80.78 |
| 700 | 1.53 |

### 11.11 (Write Statements to Accomplish a Task)

Write statements that accomplish each of the following. Assume that the structure
