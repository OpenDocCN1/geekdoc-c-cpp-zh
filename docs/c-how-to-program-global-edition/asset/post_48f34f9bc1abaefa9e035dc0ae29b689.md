
Enter request
1 - List accounts with zero balances
2 - List accounts with credit balances
3 - List accounts with debit balances
4 - End of run
? 1

Accounts with zero balances:
300    White    0.00

? 2

Accounts with credit balances:
400    Stone    -42.16

? 3

Accounts with debit balances:
100    Jones    24.98
200    Doe      345.67
500    Rich     224.62

? 4
End of run.

Fig. 11.8 | Sample output of the credit inquiry program of Fig. 11.7.

## Updating a Sequential File

Data in this type of sequential file cannot be modified without the risk of destroying other data. For example, if the name "white" needs to be changed to "Worthington," the old name cannot simply be overwritten. The record for White was written to the file as

```
300 White 0.00
```

If the record is rewritten beginning at the same location in the file using the new name, the record will be

```
300 Worthington 0.00
```

The new record is larger (has more characters) than the original record. The characters beyond the second "o" in "Worthington" will overwrite the beginning of the next sequential record in the file. The problem here is that in the formatted input/output model using fprintf and fscanf, fields—and hence records—can vary in size. For example, the values 7, 14, -117, 2074 and 27383 are all ints stored in the same number of bytes internally, but they're different-sized fields when displayed on the screen or written to a file as text.

Therefore, sequential access with fprintf and fscanf is not usually used to update records in place. Instead, the entire file is usually rewritten. To make the preceding name change, the records before 300 White 0.00 in such a sequential-access file would be copied to a new file, the new record would be written and the records after 300 White 0.00 would be copied to the new file. This requires processing every record in the file to update one record.

The function fread copies data from the file specified by the file position pointer to an area in memory beginning with a specified address. Now, when writing a four-byte integer, instead of using

```
fprintf(fPtr, "%d", number);
```

which could print a single digit or as many as 11 digits (10 digits plus a sign, each of which requires at least one byte of storage, based on the character set for the locale), we can use

```
fwrite(&number, sizeof(int), 1, fPtr);
```

which always writes four bytes on a system with four-byte integers from a variable number to the file represented by fPtr (we'll explain the 1 argument shortly). Later, fread can be used to read those four bytes into an integer variable number. Although fread and fwrite read and write data, such as integers, in fixed-size rather than variable-size format, the data they handle are processed in computer “raw data” format (i.e., bytes of data) rather than in printf’s and scanf’s human-readable text format. Because the “raw” representation of data is system dependent, “raw data” may not be readable on other systems, or by programs produced by other compilers or with other compiler options.

## fwrite and fread Can Write and Read Arrays

Functions fwrite and fread are capable of reading and writing arrays of data to and from files. The third argument of both fread and fwrite is the number of elements of the array that should be read from or written to a file. The preceding fwrite function call writes a single integer to a file, so the third argument is 1 (as if one element of an array were being written). File-processing programs rarely write a single field to a file. Normally, they write one struct at a time, as we show in the following examples.

## Problem Statement

Consider the following problem statement:

Create a transaction-processing system capable of storing up to 100 fixed-length records. Each record should consist of an account number that will be used as the record key, a last name, a first name and a balance. The resulting program should be able to update an account, insert a new account record, delete an account and list all the account records in a formatted text file for printing. Use a random-access file.

The next several sections introduce the techniques necessary to create the transaction-processing program. Figure 11.10 shows how to open a random-access file, define a record format using a struct, write data to the file and close the file. This program initializes all 100 records of the file “accounts.dat” with empty structs using the function fwrite. Each empty struct contains 0 for the account number, "" (the empty string) for the last name, "" for the first name and 0.0 for the balance. The file is initialized in this manner to create the space in which the file will be stored and to make it possible to determine whether a record contains data.

// Fig. 11.10: fig11_10.c
// Creating a random-access file sequentially
#include <stdio.h>

Fig. 11.10 | Creating a random-access file sequentially. (Part 1 of 2.)

```c
// Fig. 11.11: fig11_11.c
// Writing data randomly to a random-access file
#include <stdio.h>

// clientData structure definition
struct clientData {
    unsigned int acctNum;  // account number
    char lastName[15];     // account last name
    char firstName[10];    // account first name
    double balance;        // account balance
}; // end structure clientData

int main(void)
{
    FILE *cfPtr;  // accounts.dat file pointer

    // fopen opens the file; exits if file cannot be opened
    if ((cfPtr = fopen("accounts.dat", "rb+")) == NULL) {
        puts("File could not be opened.");
    }
    else {
        // create clientData with default information
        struct clientData client = {0, "", "", 0.0};

        // require user to specify account number
        printf("%s", "Enter account number\n");
        printf("%s", " (1 to 100, 0 to end input): ");
        scanf("%d", &client.acctNum);

        // user enters information, which is copied into file
        while (client.acctNum != 0) {
            // user enters last name, first name and balance
            printf("%s", "\nEnter lastname, firstname, balance: ");

            // set record lastName, firstName and balance value
            fscanf(stdin, "%14s%9s%lf", client.lastName,
                client.firstName, &client.balance);

            // seek position in file to user-specified record
            fseek(cfPtr, (client.acctNum - 1) *
                sizeof(struct clientData), SEEK_SET);

            // write user-specified information in file
            fwrite(&client, sizeof(struct clientData), 1, cfPtr);

            // enable user to input another account number
            printf("%s", "\nEnter account number: ");
            scanf("%d", &client.acctNum);
        }

    }
    fclose(cfPtr); // fclose closes the file
}
```

Enter account number (1 to 100, 0 to end input): 37
Enter lastname, firstname, balance: Barker Doug 0.00
Enter account number: 29
Enter lastname, firstname, balance: Brown Nancy -24.54
Enter account number: 96
Enter lastname, firstname, balance: Stone Sam 34.98
Enter account number: 88
Enter lastname, firstname, balance: Smith Dave 258.34
Enter account number: 33
Enter lastname, firstname, balance: Dunn Stacey 314.33
Enter account number: 0

Fig. 11.12 | Sample execution of the program in Fig. 11.11.

## 11.7.1 Positioning the File Position Pointer with fseek

Lines 40–41 position the file position pointer for the file referenced by cfPtr to the byte location calculated by (client.accountNum - 1) * sizeof(struct clientData). The value of this expression is called the offset or the displacement. Because the account number is between 1 and 100 but the byte positions in the file start with 0, 1 is subtracted from the account number when calculating the byte location of the record. Thus, for record 1, the file position pointer is set to byte 0 of the file. The symbolic constant SEEK_SET indicates that the file position pointer is positioned relative to the beginning of the file by the amount of the offset. As the above statement indicates, a seek for account number 1 in the file sets the file position pointer to the beginning of the file because the byte location calculated is 0.

Figure 11.13 illustrates the file pointer referring to a FILE structure in memory. The file position pointer in this diagram indicates that the next byte to be read or written is 5 bytes from the beginning of the file.

## fseek Function Prototype

The function prototype for fseek is

```
int fseek(FILE *stream, long int offset, int whence);
```

where offset is the number of bytes to seek from whence in the file pointed to by stream—a positive offset seeks forward and a negative one seeks backward. Argument whence is one of the values SEEK_SET, SEEK_CUR or SEEK_END (all defined in <stdio.h>), which indicate the location from which the seek begins. SEEK_SET indicates that the seek starts at the beginning of the file; SEEK_CUR indicates that the seek starts at the current location in the file; and SEEK_END indicates that the seek is measured from at the end of the file.
