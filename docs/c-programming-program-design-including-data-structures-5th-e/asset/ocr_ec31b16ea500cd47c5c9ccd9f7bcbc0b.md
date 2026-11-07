```
```cpp
{
    cout << "The input file does not exist. "
         << "The program terminates!!!!" << endl; //Line 6
    return 1;                                      //Line 7
}

cout << fixed << showpoint << setprecision(2);     //Line 8

//randomly read the records and output them
inFile.seekg(6 * custSize, ios::beg);              //Line 9
inFile.read(reinterpret_cast<char *> (&cust),      //Line 10
            sizeof(cust));
cout << "Seventh customer's data: " << endl;       //Line 11
printCustData(cust);                               //Line 12

inFile.seekg(8 * custSize, ios::beg);              //Line 13
inFile.read(reinterpret_cast<char *> (&cust),      //Line 14
            sizeof(cust));
cout << "Ninth customer's data: " << endl;         //Line 15
printCustData(cust);

inFile.seekg(-8 * custSize, ios::end);             //Line 16
inFile.read(reinterpret_cast<char *> (&cust),      //Line 17
            sizeof(cust));
cout << "Eighth (from the end) customer's data: "    //Line 18
     << endl;
printCustData(cust);                               //Line 19

inFile.close();    //close the file              //Line 20

return 0;                                           //Line 21
}
```
```

```
```cpp
void printCustData(const customerType& customer)
{
    cout << "  ID: " << customer.ID << endl
         << "  First Name: " << customer.firstName << endl
         << "  Last Name: " << customer.lastName << endl
         << "  Account Balance: $" << customer.balance
         << endl;
}
```
```

# Sample Run:

```
```text
Seventh customer's data:
    ID: 22222
    First Name: Jose
    Last Name: Ramey
    Account Balance: $25345.35
Ninth customer's data:
    ID: 55555
    First Name: Tommy
    Last Name: Pitts
```
```