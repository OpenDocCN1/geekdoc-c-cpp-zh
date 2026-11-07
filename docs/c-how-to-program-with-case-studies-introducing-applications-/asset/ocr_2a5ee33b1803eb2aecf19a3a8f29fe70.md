the program displays a message that the record is empty, then redisplays the menu choices. If the record contains information, function updateRecord inputs the transaction amount, calculates the new balance and rewrites the record to the file. A typical output for option 2 is

```
Enter account to update (1 - 100): 37
37      Barker      Doug            0.00

Enter charge (+) or payment (-): +87.99
37      Barker      Doug            87.99
```

# Option 3: Create a New Account

Option 3 calls the function newRecord (lines 128–161) to add a new account to the file. If the user enters an account number for an existing account, newRecord displays an error message indicating that the record already contains information, and the menu choices are printed again. This function uses the same process to add a new account, as does the program in Fig. 11.5. A typical output for option 3 is

```
Enter new account number (1 - 100): 22
Enter lastname, firstname, balance
? Johnston Sarah 247.45
```

# Option 4: Delete an Account

Option 4 calls function deleteRecord (lines 164–190) to delete a record from the file. Deletion is accomplished by asking the user for the account number and reinitializing the record. If the account contains no information, deleteRecord displays an error message indicating that the account does not exist.

# Code for the Transaction-Processing Program

The program is shown in Fig. 11.7. The file "accounts.dat" is opened for update (reading and writing) using "rb+" mode.

```
// fig11_07.c
// Transaction-processing program reads a random-access file sequentially,
// updates data already written to the file, creates new data to
// be placed in the file, and deletes data previously stored in the file.
#include <stdio.h>

// clientData structure definition
struct clientData {
  int account;
  char lastName[15];
  char firstName[10];
  double balance;
};
```