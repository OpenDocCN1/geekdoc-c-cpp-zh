```
```cpp
// read all records from file
while (inCredit) {
   // display record
   if (client.getAccountNumber() != 0) {
      outputLine(cout, client);
   }

   // read next from file
   inCredit.read(reinterpret_cast<char*>(&client), sizeof(ClientData));
}

// display single record
void outputLine(ostream& output, const ClientData& record) {
   output << left << setw(10) << record.getAccountNumber()
          << setw(16) << record.getLastName()
          << setw(10) << setprecision(2) << right << fixed
          << showpoint << record.getBalance() << endl;
}
```
```

| Account | Last Name | First Name | Balance |
|---:|---|---|---:|
| 29 | Brown | Nancy | -24.54 |
| 33 | Dunn | Stacey | 314.33 |
| 37 | Barker | Doug | 0.00 |
| 88 | Smith | Dave | 258.34 |
| 96 | Stone | Sam | 34.98 |

**Fig. 14.12 Reading a random-access file sequentially.**

Figure 14.12 reads every record in the `credit.dat` file sequentially, checks each record to determine whether it contains data, and displays formatted outputs for records containing data. The condition in line 31 implicitly uses the stream’s operator `bool` to determine whether the end of file was reached or whether an error occurred when reading from the file—in both cases the `while` statement terminates. The data input from the file is output by function `outputLine` (lines 43–49), which takes two arguments—a reference to an `ostream` object and a `ClientData` structure to be output. The `ostream` parameter type is interesting, because any `ostream` object