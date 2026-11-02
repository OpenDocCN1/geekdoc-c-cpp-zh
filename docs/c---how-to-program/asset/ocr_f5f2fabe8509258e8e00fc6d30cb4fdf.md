```
// clientData structure definition
struct clientData {
    unsigned int acctNum; // account number
    char lastName[15]; // account last name
    char firstName[10]; // account first name
    double balance; // account balance
};

int main(void)
{
    FILE *cfPtr; // accounts.dat file pointer

    // fopen opens the file; exits if file cannot be opened
    if ((cfPtr = fopen("accounts.dat", "wb")) == NULL) {
        puts("File could not be opened.");
    }
    else {
        // create clientData with default information
        struct clientData blankClient = {0, "", "", 0.0};

        // output 100 blank records to file
        for (unsigned int i = 1; i <= 100; ++i) {
            fwrite(&blankClient, sizeof(struct clientData), 1, cfPtr);
        }

        fclose (cfPtr); // fclose closes the file
    }
}
```

Fig. 11.10 | Creating a random-access file sequentially. (Part 2 of 2.)

Function fwrite writes a block of bytes to a file. Line 27 causes the structure blankClient of size sizeof(struct clientData) to be written to the file pointed to by cfPtr. The operator sizeof returns the size in bytes of its operand in parentheses (in this case struct clientData).

Function fwrite can actually be used to write several elements of an array of objects. To do so, supply in the call to fwrite a pointer to an array as the first argument and the number of elements to be written as the third argument. In the preceding statement, fwrite was used to write a single object that was not an array element. Writing a single object is equivalent to writing one element of an array, hence the 1 in the fwrite call.

> [Note: Figures 11.11, 11.14 and 11.15 use the data file created in Fig. 11.10, so you must run Fig. 11.10 before Figs. 11.11, 11.14 and 11.15.]

# 11.7 Writing Data Randomly to a Random-Access File

Figure 11.11 writes data to the file "accounts.dat". It uses the combination of fseek and fwrite to store data at specific locations in the file. Function fseek sets the file position pointer to a specific position in the file, then fwrite writes the data. A sample execution is shown in Fig. 11.12.