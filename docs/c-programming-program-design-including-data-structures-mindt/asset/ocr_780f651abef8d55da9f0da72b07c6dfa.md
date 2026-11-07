+   5. Print the report.
+   6. Calculate and print the maximum sales by salesperson.
+   7. Calculate and print the maximum sales by quarter.

To reduce the complexity of the main program, let us write a separate function for each of these seven steps.

# Function `initialize`

This function reads the salesperson’s ID from the input file and stores the salesperson’s ID in the array `salesPersonList`. It also initializes the quarterly sales amount and the total sales amount for each salesperson to 0. The definition of this function is:

```
```cpp
void initialize(ifstream& indata, salesPersonRec list[],
                int listSize)
{
    for (int index = 0; index < listSize; index++)
    {
        indata >> list[index].ID; //get salesperson’s ID

        for (int quarter = 0; quarter < 4; quarter++)
            list[index].saleByQuarter[quarter] = 0.0;

        list[index].totalSale = 0.0;
    }
} //end initialize
```
```

# Function `getData`

This function reads the sales data from the input file and stores the appropriate information in the array `salesPersonList`. The algorithm for this function is as follows:

+   1. Read the salesperson’s ID, month, and sales amount for the month.
+   2. Search the array `salesPersonList` to locate the component corresponding to the salesperson. (Because the salespeople’s IDs are not sorted we will use a sequential search to search the array.)
+   3. Determine the quarter corresponding to the month.
+   4. Update the sales for the quarter by adding the sales amount for the month.

Suppose that the entry read is:

```
```text
57373 2 350
```
```

Here, the salesperson’s ID is 57373, the month is 2, and the sales amount is 350. Suppose that the array `salesPersonList` is as shown in Figure 9-11.