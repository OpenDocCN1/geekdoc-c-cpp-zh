

![](img/d0d3b7423c2d9e5650be79209ea1885d_479_0.png)

**Fig. 11.4** | Relationship between FILE pointers, FILE structures and FCBs.

### 11.3.6 File Open Modes

Files may be opened in one of several modes, which are summarized in Fig. 11.5. Each file open mode in the first half of the table has a corresponding *binary* mode (containing the letter b) for manipulating binary files. The binary modes are used in Sections 11.5–11.9 when we introduce random-access files.

| Mode | Description |
|---|---|
| `r` | Open an existing file for reading. |
| `w` | Create a file for writing. If the file already exists, discard the current contents. |
| `a` | Open or create a file for writing at the end of the file—i.e., write operations append data to the file. |
| `r+` | Open an existing file for update (reading and writing). |
| `w+` | Create a file for reading and writing. If the file already exists, discard the current contents. |
| `a+` | Open or create a file for reading and updating; all writing is done at the end of the file—i.e., write operations append data to the file. |
| `rb` | Open an existing file for reading in binary mode. |
| `wb` | Create a file for writing in binary mode. If the file already exists, discard the current contents. |
| `ab` | Append: open or create a file for writing at the end of the file in binary mode. |
| `rb+` | Open an existing file for update (reading and writing) in binary mode. |
| `wb+` | Create a file for update in binary mode. If the file already exists, discard the current contents. |
| `ab+` | Open or create a file for update in binary mode; writing is done at the end of the file. |

**Fig. 11.5**  File opening modes.

#### C11 Exclusive Write Mode

In addition, C11 provides exclusive write mode, which you indicate by adding an x to the end of the w, w+, or wb+ modes. In exclusive write mode, `fopen` will fail if the file already exists or cannot be created. If opening a file in exclusive write mode is successful and the underlying system supports exclusive file access, then only your program can access the file while it’s open. (Some compilers and platforms do not support exclusive write mode.) If an error occurs while opening a file in any mode, `fopen` returns `NULL`.

> **Common Programming Error 11.3**
>
> *Opening a nonexistent file for reading is an error.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_480_0.png)

> **Common Programming Error 11.4**
>
> *Opening a file for reading or writing without having been granted the appropriate access rights to the file (this is operating-system dependent) is an error.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_480_1.png)

> **Common Programming Error 11.5**
>
> *Opening a file for writing when no space is available is a runtime error.*

![](img/d0d3b7423c2d9e5650be79209ea1885d_480_2.png)

> **Common Programming Error 11.6**
>
> Opening a file in write mode (`"w"`) when it should be opened in update mode (`"r+"`) causes the contents of the file to be discarded.

> **Error-Prevention Tip 11.1**
>
> Open a file only for reading (and not updating) if its contents should not be modified. This prevents the unintentional modification of the file's contents. This is another example of the principle of least privilege.

## 11.4 Reading Data from a Sequential-Access File

Data is stored in files so that it can be retrieved for processing when needed. The previous section demonstrated how to create a file for sequential access. This section shows how to read data sequentially from a file.

Figure 11.6 reads records from the file "clients.txt" created by the program of Fig. 11.2 and prints their contents. Line 7 indicates that cfPtr is a *pointer to a FILE*. Line 10 attempts to open the file "clients.txt" for reading (`"r"`) and determines whether it opened successfully (i.e., `fopen` does not return `NULL`). Line 19 reads a "record" from the file. Function `fscanf` is equivalent to function `scanf`, except `fscanf` receives as an argument a file pointer for the file from which the data is read. After this statement executes the first time, account will have the value 100, name will have the value "Jones" and balance will have the value 24.98. Each time the second `fscanf` statement (line 24) executes, the program reads another record from the file and account, name and balance take on new values. When the program reaches the end of the file, the file is closed (line 27) and the program terminates. Function `feof` returns true only after the program attempts to read the nonexistent data following the last line.

```c
// Fig. 11.6: fig11_06.c
// Reading and printing a sequential file
#include <stdio.h>

int main(void)
{
    FILE *cfPtr; // cfPtr = clients.txt file pointer

    // fopen opens file; exits program if file cannot be opened
    if ((cfPtr = fopen("clients.txt", "r")) == NULL) {
        puts("File could not be opened");
    }
    else { // read account, name and balance from file
        unsigned int account; // account number
        char name[30]; // account name
        double balance; // account balance

        printf("%-10s%-13s%s\n", "Account", "Name", "Balance");
        fscanf(cfPtr, "%d%29s%lf", &account, name, &balance);

        // while not end of file
        while (!feof(cfPtr)) {
            printf("%-10d%-13s%7.2f\n", account, name, balance);
            fscanf(cfPtr, "%d%29s%lf", &account, name, &balance);
        }

        fclose(cfPtr); // fclose closes the file
    }
}
```

**Fig. 11.6** | Reading and printing a sequential file.

| Account | Name | Balance |
|---|---|---|
| 100 | Jones | 24.98 |
| 200 | Doe | 345.67 |
| 300 | White | 0.00 |
| 400 | Stone | -42.16 |
| 500 | Rich | 224.62 |

### 11.4.1 Resetting the File Position Pointer

To retrieve data sequentially from a file, a program normally starts reading from the beginning of the file and reads all data consecutively until the desired data is found. It may be desirable to process the data sequentially in a file several times (from the beginning of the file) during the execution of a program. The statement

`rewind(cfPtr);`

causes a program's file position pointer—which indicates the number of the next byte in the file to be read or written—to be repositioned to the beginning of the file (i.e., byte 0) pointed to by cfPtr. The file position pointer is not really a pointer. Rather it's an integer value that specifies the byte in the file at which the next read or write is to occur. This is sometimes referred to as the file offset. The file position pointer is a member of the FILE structure associated with each file.

### 11.4.2 Credit Inquiry Program

The program of Fig. 11.7 allows a credit manager to obtain lists of customers with zero balances (i.e., customers who do not owe any money), customers with credit balances (i.e., customers to whom the company owes money) and customers with debit balances (i.e., customers who owe the company money for goods and services received). A credit balance is a negative amount; a debit balance is a positive amount.

The program displays a menu and allows the credit manager to enter one of four options:

- Option 1 produces a list of accounts with zero balances.
- Option 2 produces a list of accounts with credit balances.
- Option 3 produces a list of accounts with debit balances.
- Option 4 terminates program execution.

A sample output is shown in Fig. 11.8.

```c
// Fig. 11.7: fig11_07.c
// Credit inquiry program
#include <stdio.h>

// function main begins program execution
int main(void)
{
    FILE *cfPtr; // clients.txt file pointer

    // fopen opens the file; exits program if file cannot be opened
    if ((cfPtr = fopen("clients.txt", "r")) == NULL) {
        puts("File could not be opened");
    }
    else {

        // display request options
        printf("%s", "Enter request\n"
            " 1 - List accounts with zero balances\n"
            " 2 - List accounts with credit balances\n"
            " 3 - List accounts with debit balances\n"
            " 4 - End run\n");
        unsigned int request; // request number
        scanf("%u", &request);

        // process user's request
        while (request != 4) {
            unsigned int account; // account number
            double balance; // account balance
            char name[30]; // account name

            // read account, name and balance from file
            fscanf(cfPtr, "%d%29s%lf", &account, name, &balance);

            switch (request) {
                case 1:
                    puts("\nAccounts with zero balances:");

                    // read file contents (until eof)
                    while (!feof(cfPtr)) {
                        // output only if balance is 0
                        if (balance == 0) {
                            printf("%-10d%-13s%7.2f\n",
                                account, name, balance);
                        }

                        // read account, name and balance from file
                        fscanf(cfPtr, "%d%29s%lf",
                            &account, name, &balance);
                    }
                    break;
```

**Fig. 11.7** | Credit inquiry program. (Part 1 of 2.)

