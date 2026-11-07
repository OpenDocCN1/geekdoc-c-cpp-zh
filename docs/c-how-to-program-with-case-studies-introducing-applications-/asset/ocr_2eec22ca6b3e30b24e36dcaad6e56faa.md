```
```c
// prototypes
int enterChoice(void);
void textFile(FILE *readPtr);
void updateRecord(FILE *fPtr);
void newRecord(FILE *fPtr);
void deleteRecord(FILE *fPtr);

int main(void) {
    FILE *cfPtr = NULL; // accounts.dat file pointer

    // fopen opens the file; exits if file cannot be opened
    if ((cfPtr = fopen("accounts.dat", "rb+")) == NULL) {
        puts("File could not be opened.");
    }
    else {
        int choice = 0; // user

        // enable user to specify action
        while ((choice = enterChoice()) != 5) {
            switch (choice) {
                case 1: // create text file from record file
                    textFile(cfPtr);
                    break;
                case 2: // update record
                    updateRecord(cfPtr);
                    break;
                case 3: // create record
                    newRecord(cfPtr);
                    break;
                case 4: // delete existing record
                    deleteRecord(cfPtr);
                    break;
                default: // display message for invalid choice
                    puts("Incorrect choice");
                    break;
            }
        }
    }

    fclose(cfPtr); // fclose closes the file
}

// create formatted text file for printing
void textFile(FILE *readPtr) {
    FILE *writePtr = NULL; // accounts.txt file pointer

    // fopen opens the file; exits if file cannot be opened
    if ((writePtr = fopen("accounts.txt", "w")) == NULL) {
        puts("File could not be opened.");
```
```

Fig. 11.7 | Transaction-processing program. (Part 2 of 5.)