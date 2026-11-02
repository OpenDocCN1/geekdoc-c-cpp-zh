
```c
// delete an existing record
void deleteRecord(FILE *fPtr)
{
    // obtain number of account to delete
    printf("%s", "Enter account number to delete (1 - 100): ");
    unsigned int accountNum; // account number
    scanf("%d", &accountNum);

    // move file pointer to correct record in file
    fseek(fPtr, (accountNum - 1) * sizeof(struct clientData),
        SEEK_SET);

    struct clientData client; // stores record read from file

    // read record from file
    fread(&client, sizeof(struct clientData), 1, fPtr);

    // display error if record does not exist
    if (client.acctNum == 0) {
        printf("Account %d does not exist.\n", accountNum);
    }
    else { // delete record
        // move file pointer to correct record in file
        fseek(fPtr, (accountNum - 1) * sizeof(struct clientData),
            SEEK_SET);

        struct clientData blankClient = {0, "", "", 0}; // blank client

        // replace existing record with blank record
        fwrite(&blankClient,
            sizeof(struct clientData), 1, fPtr);
    }
}

// create and insert record
void newRecord(FILE *fPtr)
{
    // obtain number of account to create
    printf("%s", "Enter new account number (1 - 100): ");
    unsigned int accountNum; // account number
    scanf("%d", &accountNum);

    // move file pointer to correct record in file
    fseek(fPtr, (accountNum - 1) * sizeof(struct clientData),
        SEEK_SET);

    // create clientData with default information
    struct clientData client = {0, "", "", 0.0};

    // read record from file
    fread(&client, sizeof(struct clientData), 1, fPtr);

194   // display error if account already exists
195   if (client.acctNum != 0) {
196      printf("Account #%d already contains information.\n",
197         client.acctNum);
198   }
199   else { // create record
200      // user enters last name, first name and balance
201      printf("%s", "Enter lastname, firstname, balance\n? ");
202      scanf("%14s%14s%lf", client.lastName, client.firstName,
203         &client.balance);
204
205      client.acctNum = accountNum;
206
207      // move file pointer to correct record in file
208      fseek(fPtr, (client.acctNum - 1) *
209         sizeof(struct clientData), SEEK_SET);
210
211      // insert record in file
212      fwrite(&client,
213         sizeof(struct clientData), 1, fPtr);
214
215   }
216
217   // enable user to input menu choice
218   unsigned int enterChoice(void)
219   {
220      // display available options
221      printf("%s", "\nEnter your choice\n"
222         " 1 - store a formatted text file of accounts called\n"
223         "     \"accounts.txt\" for printing\n"
224         " 2 - update an account\n"
225         " 3 - add a new account\n"
226         " 4 - delete an account\n"
227         " 5 - end program\n? ");
228
229      unsigned int menuChoice; // variable to store user's choice
230      scanf("%u", &menuChoice); // receive choice from user
231      return menuChoice;
232   }
```

**Fig. 11.15** | Transaction-processing program. (Part 5 of 5.)

## 11.10 Secure C Programming

### *fprintf_s and fscanf_s*

The examples in Sections 11.3–11.4 used functions fprintf and fscanf to write text to and read text from files, respectively. The new standard's Annex K provides more secure versions of these functions named fprintf_s and fscanf_s that are identical to the printf_s and scanf_s functions we've previously introduced, except that you also specify a FILE pointer argument indicating the file to manipulate. If your C compiler's standard libraries include these functions, you should use them instead of fprintf and fscanf. As with scanf_s and printf_s, Microsoft's versions of fprintf_s and fscanf_s differ from those in Annex K.

### Chapter 9 of the CERT Secure C Coding Standard

Chapter 9 of the CERT Secure C Coding Standard is dedicated to input/output recommendations and rules—many apply to file processing in general and several of these apply to the file-processing functions presented in this chapter. For more information on each, visit www.securecoding.cert.org.

- **FIO03-C:** When opening a file for writing using the nonexclusive file-open modes (Fig. 11.5), if the file exists, function fopen opens it and truncates its contents, providing no indication of whether the file existed before the fopen call. To ensure that an existing file is not opened and truncated, you can use C11’s new exclusive write mode (discussed in Section 11.3), which allows fopen to open the file only if it does not already exist.
- **FIO04-C:** In industrial-strength code, you should always check the return values of file-processing functions that return error indicators to ensure that the functions performed their tasks correctly.
- **FIO07-C:** Function rewind does not return a value, so you cannot test whether the operation was successful. It’s recommended instead that you use function fseek, because it returns a nonzero value if it fails.
- **FIO09-C:** We demonstrated both text files and binary files in this chapter. Due to differences in binary data representations across platforms, files written in binary format often are not portable. For more portable file representations, consider using text files or a function library that can handle the differences in binary file representations across platforms.
- **FIO14-C:** Some library functions do not operate identically on text files and binary files. In particular, function fseek is not guaranteed to work correctly with binary files if you seek from SEEK_END, so SEEK_SET should be used.
- **FIO42-C:** On many platforms, you can have only a limited number of files open at once. For this reason, you should always close a file as soon as it’s no longer needed by your program.

## Summary

### Section 11.1 Introduction

- Files (p. 474) are used for permanent retention of large amounts of data.
- Computers store files on secondary storage devices, such as hard drives, solid-state drives, flash drives and DVDs.

### Section 11.2 Files and Streams

- C views each file as a sequential stream of bytes (p. 474). When a file is opened, a stream is associated with the file.
- Three streams are automatically opened when program execution begins—the standard input (p. 474), the standard output (p. 474) and the standard error (p. 474).
- Streams provide communication channels between files and programs.
- The standard input stream enables a program to read data from the keyboard, and the standard output stream enables a program to print data on the screen.
- Opening a file returns a pointer to a FILE structure (defined in `<stdio.h>`; p. 475) that contains information used to process the file. This structure includes a file descriptor (p. 475), i.e., an index into an operating system array called the open file table (p. 475). Each array element contains a file control block (FCB; p. 475) that the operating system uses to administer a particular file.
- The standard input, standard output and standard error are manipulated using the predefined file pointers `stdin`, `stdout` and `stderr`.
- Function `fgetc` (p. 475) reads one character from a file. It receives as an argument a FILE pointer for the file from which a character will be read.
- Function `fputc` (p. 475) writes one character to a file. It receives as arguments a character to be written and a FILE pointer for the file to which the character will be written.
- The `fgets` and `fputs` functions (p. 475) read a line from a file or write a line to a file, respectively.

### Section 11.3 Creating a Sequential-Access File

- C imposes no structure on a file. You must provide a file structure to meet the requirements of a particular application.
- A C program administers each file with a separate FILE structure.
- Each open file must have a separately declared pointer of type FILE that's used to refer to the file.
- Function `fopen` (p. 480) takes as arguments a filename and a file open mode (p. 477) and returns a pointer to the FILE structure for the file opened.
- The file open mode `"w"` indicates that the file is to be opened for writing. If the file does not exist, `fopen` creates it. If the file exists, the contents are discarded without warning.
- Function `fopen` returns `NULL` if it's unable to open a file.
- Function `feof` (p. 478) receives a pointer to a FILE and returns a nonzero (true) value when the end-of-file indicator has been set; otherwise, the function returns zero. Any attempt to read from a file for which `feof` returns true will fail.
- Function `fprintf` (p. 475) is equivalent to `printf` except that `fprintf` also receives as an argument a file pointer for the file to which the data will be written.
- Function `fclose` (p. 478) receives a file pointer as an argument and closes the specified file.
- When a file is opened, the file control block (FCB) for the file is copied into memory. The FCB is used by the operating system to administer the file.
- To create a new file, or to discard an existing file's contents before writing data, open the file for writing (`"w"`).
- To read an existing file, open it for reading (`"r"`).
- To add records to the end of an existing file, open the file for appending (`"a"`).
- To open a file so that it may be written to and read from, open the file for updating in one of the three update modes—`"r+"`, `"w+"` or `"a+"`. Mode `"r+"` opens a file for reading and writing. Mode `"w+"` creates a file for reading and writing. If the file already exists, it's opened and its contents are discarded. Mode `"a+"` opens a file for reading and writing—all writing is done at the end of the file. If the file does not exist, it's created.
- Each file open mode has a corresponding binary mode (containing the letter `b`) for manipulating binary files.
- C11 also supports exclusive write mode by appending `x` to the `w`, `w+`, `wb` and `wb+` modes.
