
```c
case 2:
    puts("\nAccounts with credit balances:\n");
    // read file contents (until eof)
    while (!feof(cfPtr)) {
        // output only if balance is less than 0
        if (balance < 0) {
            printf("%-10d%-13s%7.2f\n",
                account, name, balance);
        }
        // read account, name and balance from file
        fscanf(cfPtr, "%d%29s%f",
            &account, name, &balance);
    }
    break;
case 3:
    puts("\nAccounts with debit balances:\n");
    // read file contents (until eof)
    while (!feof(cfPtr)) {
        // output only if balance is greater than 0
        if (balance > 0) {
            printf("%-10d%-13s%7.2f\n",
                account, name, balance);
        }
        // read account, name and balance from file
        fscanf(cfPtr, "%d%29s%f",
            &account, name, &balance);
    }
    break;
}
rewind(cfPtr); // return cfPtr to beginning of file
printf("%s", "\n? ");
scanf("%d", &request);
}
puts("End of run.");
fclose(cfPtr); // fclose closes the file
}
```

```
Enter request
 1 - List accounts with zero balances
 2 - List accounts with credit balances
 3 - List accounts with debit balances
 4 - End of run
? 1

Accounts with zero balances:
300        White             0.00

? 2

Accounts with credit balances:
400        Stone           -42.16

? 3

Accounts with debit balances:
100        Jones            24.98
200        Doe             345.67
500        Rich            224.62

? 4
End of run.
```

**Fig. 11.8** | Sample output of the credit inquiry program of Fig. 11.7.

## Updating a Sequential File

Data in this type of sequential file cannot be modified without the risk of destroying other data. For example, if the name “White” needs to be changed to “Worthington,” the old name cannot simply be overwritten. The record for White was written to the file as

```text
300 White 0.00
```

If the record is rewritten beginning at the same location in the file using the new name, the record will be

```text
300 Worthington 0.00
```

The new record is larger (has more characters) than the original record. The characters beyond the second 0 in “Worthington” will overwrite the beginning of the next sequential record in the file. The problem here is that in the formatted input/output model using fprintf and fscanf, fields—and hence records—can vary in size. For example, the values 7, 14, −117, 2074 and 27383 are all ints stored in the same number of bytes internally, but they’re different-sized fields when displayed on the screen or written to a file as text.

Therefore, sequential access with fprintf and fscanf is not usually used to update records in place. Instead, the entire file is usually rewritten. To make the preceding name change, the records before 300 White 0.00 in such a sequential-access file would be copied to a new file, the new record would be written and the records after 300 White 0.00 would be copied to the new file. This requires processing every record in the file to update one record.

## 11.5 Random-Access Files

As we stated previously, records in a file created with the formatted output function `fprintf` are not necessarily of the same length. However, individual records that you write to and read from a random-access file are normally *fixed in length* and may be accessed directly (and thus quickly) without searching through other records. This makes random-access files appropriate for airline reservation systems, banking systems, point-of-sale systems, and other kinds of transaction-processing systems that require rapid access to specific data. There are other ways of implementing random-access files, but we'll limit our discussion to this straightforward approach using fixed-length records.

Because every record in a random-access file normally has the same length, the exact location of a record relative to the beginning of the file can be calculated as a function of the record key. We'll soon see how this facilitates *immediate* access to specific records, even in large files.

Figure 11.9 illustrates one way to implement a random-access file. Such a file is like a freight train with many cars—some empty and some with cargo. Each car in the train has the same length.

![](img/d0d3b7423c2d9e5650be79209ea1885d_486_0.png)

**Fig. 11.9** | C's view of a random-access file.

Fixed-length records enable data to be inserted in a random-access file *without destroying other data in the file*. Data stored previously can also be updated or deleted without rewriting the entire file. In the following sections we explain how to

- create a random-access file,
- enter data,
- read the data both sequentially and randomly,
- update the data,
- and delete data no longer needed.

## 11.6 Creating a Random-Access File

Function `fwrite` transfers a specified number of bytes beginning at a specified location in memory to a file. The data is written beginning at the location in the file indicated by the file position pointer. Function `fread` transfers a specified number of bytes from the location in the file specified by the file position pointer to an area in memory beginning with a specified address. Now, when writing a four-byte integer, instead of using

```c
    fprintf(fPtr, "%d", number);
```

which could print a single digit or as many as 11 digits (10 digits plus a sign, each of which requires at least one byte of storage, based on the character set for the locale), we can use

```c
    fwrite(&number, sizeof(int), 1, fPtr);
```

which always writes four bytes on a system with four-byte integers from a variable number to the file represented by fPtr (we’ll explain the 1 argument shortly). Later, fread can be used to read those four bytes into an integer variable number. Although fread and fwrite read and write data, such as integers, in fixed-size rather than variable-size format, the data they handle are processed in computer “raw data” format (i.e., bytes of data) rather than in printf’s and scanf’s human-readable text format. Because the “raw” representation of data is system dependent, “raw data” may not be readable on other systems, or by programs produced by other compilers or with other compiler options.

### fwrite and fread Can Write and Read Arrays

Functions fwrite and fread are capable of reading and writing arrays of data to and from files. The third argument of both fread and fwrite is the number of elements in the array that should be read from or written to a file. The preceding fwrite function call writes a single integer to a file, so the third argument is 1 (as if one element of an array were being written). File processing programs rarely write a single field to a file. Normally, they write one struct at a time, as we show in the following examples.

### Problem Statement

Consider the following problem statement:

> *Create a transaction-processing system capable of storing up to 100 fixed-length records. Each record should consist of an account number that will be used as the record key, a last name, a first name and a balance. The resulting program should be able to update an account, insert a new account record, delete an account and list all the account records in a formatted text file for printing. Use a random-access file.*

The next several sections introduce the techniques necessary to create the transaction-processing program. Figure 11.10 shows how to open a random-access file, define a record format using a struct, write data to the file and close the file. This program initializes all 100 records of the file “accounts.dat” with empty structs using the function fwrite. Each empty struct contains 0 for the account number, "" (the empty string) for the last name, "" for the first name and 0.0 for the balance. The file is initialized in this manner to create the space in which the file will be stored and to make it possible to determine whether a record contains data.

```c
    1 // Fig. 11.10: fig11_10.c
    2 // Creating a random-access file sequentially
    3 #include <stdio.h>
    4
```

**Fig. 11.10** | Creating a random-access file sequentially. (Part 1 of 2.)
