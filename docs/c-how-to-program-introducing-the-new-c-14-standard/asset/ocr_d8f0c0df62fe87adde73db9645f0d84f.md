```
```cpp
// copy all records from record file into text file
while (!readFromFile.eof()) {
    // write single record to text file
    if (client.getAccountNumber() != 0) { // skip empty records
        outputLine(outPrintFile, client);
    }

    // read next record from record file
    readFromFile.read(
        reinterpret_cast<char*>(&client), sizeof(ClientData));
}
}

// update balance in record
void updateRecord(fstream& updateFile) {
    // obtain account number of account to update
    int accountNumber{getAccount("Enter account to update")};

    // move file-position pointer to correct record in file
    updateFile.seekg((accountNumber - 1) * sizeof(ClientData));

    // create record object and read first record from file
    ClientData client;
    updateFile.read(reinterpret_cast<char*>(&client), sizeof(ClientData));

    // update record
    if (client.getAccountNumber() != 0) {
        outputLine(cout, client); // display the record

        // request user to specify transaction
        cout << "\nEnter charge (+) or payment (-): ";
        double transaction; // charge or payment
        cin >> transaction;
```
```