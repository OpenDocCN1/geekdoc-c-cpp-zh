```
else {
    rewind(readPtr); // sets pointer to beginning of file
    fprintf(writePtr, "%-6s%-16s%-11s%10s\n",
        "Acct", "Last Name", "First Name","Balance");

    // copy all records from random-access file into text file
    while (!feof(readPtr)) {
        // create clientData with default information
        struct clientData client = {0, "", "", 0.0};
        size_t result =
            fread(&client, sizeof(struct clientData), 1, readPtr);

        // write single record to text file
        if (result != 0 && client.account != 0) {
            fprintf(writePtr, "%-6d%-16s%-11s%10.2f\n", client.account,
                client.lastName, client.firstName, client.balance);
        }
    }

    fclose(writePtr); // fclose closes the file
}

// update balance in record
void updateRecord(FILE *fPtr) {
    // obtain number of account to update
    printf("%s", "Enter account to update (1 - 100): ");
    int account = 0; // account number
    scanf("%d", &account);

    // move file pointer to correct record in file
    fseek(fPtr, (account - 1) * sizeof(struct clientData), SEEK_SET);

    // read record from file
    struct clientData client = {0, "", "", 0.0};
    fread(&client, sizeof(struct clientData), 1, fPtr);

    // display error if account does not exist
    if (client.account == 0) {
        printf("Account #%d has no information.\n", account);
    }
    else { // update record
        printf("%-6d%-16s%-11s%10.2f\n\n", client.account, client.lastName,
        client.firstName, client.balance);

        // request transaction amount from user
        printf("%s", "Enter charge (+) or payment (-): ");
        double transaction = 0.0; // transaction amount
        scanf("%lf", &transaction);
        client.balance += transaction; // update record balance
    }
```