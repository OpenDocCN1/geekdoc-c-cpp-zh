```
```c
printf("%-6d%-16s%-11s%10.2f\n", client.account, client.lastName,
    client.firstName, client.balance);

// move file pointer to correct record in file
fseek(fPtr, (account - 1) * sizeof(struct clientData), SEEK_SET);

// write updated record over old record in file
fwrite(&client, sizeof(struct clientData), 1, fPtr);
}

// create and insert record
void newRecord(FILE *fPtr) {
    // obtain number of account to create
    printf("%s", "Enter new account number (1 - 100): ");
    int account = 0; // account number
    scanf("%d", &account);

    // move file pointer to correct record in file
    fseek(fPtr, (account - 1) * sizeof(struct clientData), SEEK_SET);

    // read record from file
    struct clientData client = {0, "", "", 0.0};
    fread(&client, sizeof(struct clientData), 1, fPtr);

    // display error if account already exists
    if (client.account != 0) {
        printf("Account #%d already contains information.\n",
            client.account);
    }
    else { // create record
        // user enters last name, first name, and balance
        printf("%s", "Enter lastname, firstname, balance\n? ");
        scanf("%14s%9s%lf", &client.lastName, &client.firstName,
            &client.balance);

        client.account = account;

        // move file pointer to correct record in file
        fseek(fPtr, (client.account - 1) * sizeof(struct clientData),
            SEEK_SET);

        // insert record in file
        fwrite(&client, sizeof(struct clientData), 1, fPtr);
    }
}

// delete an existing record
void deleteRecord(FILE *fPtr) {
    // obtain number of account to delete
    printf("%s", "Enter account number to delete (1 - 100): ");
    int account = 0; // account number
    scanf("%d", &account);
}
```
```

Fig. 11.7  |  Transaction-processing program. (Part 4 of 5.)