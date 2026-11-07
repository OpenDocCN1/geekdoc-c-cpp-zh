```
```cpp
for (index = 0; index < listSize; index++)
    for (quarter = 0; quarter < 4; quarter++)
        list[index].totalSale +=
            list[index].saleByQuarter[quarter];
} //end totalSaleByPerson
```
```

# Function `printReport`

This function prints the annual report in the specified format. The algorithm in pseudocode is:

+   1. Print the heading—that is, the first three lines of output.
+   2. Print the data for each salesperson.
+   3. Print the last line of the table.

Note that the next two functions will produce the final two lines of output.

Clearly, the printReport function must have access to the array salesPersonList and the array totalSaleByQuarter. Also, because the output will be stored in a file, this function must have access to the ofstream variable associated with the output file. Thus, this function has four parameters: a parameter corresponding to the array salesPersonList, a parameter corresponding to the array totalSaleByQuarter, a parameter specifying the size of the array, and a parameter corresponding to the ofstream variable. The definition of this function is:

```
```cpp
void printReport (ofstream& outfile, salesPersonRec list[],
                  int listSize, double saleByQuarter[])
{
    int index;
    int quarter;

    outfile << "--------- Annual Sales Report ---------"
            << "-----" << endl;
    outfile << endl;
    outfile << "  ID          QT1        QT2        QT3        "
            << "QT4        Total" << endl;
    outfile << "--------------------------------------------------"
            << endl;
    outfile << "____________________________________________" << endl;

    for (index = 0; index < listSize; index++)
    {
        outfile << list[index].ID << "  ";

        for (quarter = 0; quarter < 4; quarter++)
            outfile << setw(10)
                    << list[index].saleByQuarter[quarter];

        outfile << setw(10) << list[index].totalSale << endl;
    }

    outfile << "Total  ";
```
```