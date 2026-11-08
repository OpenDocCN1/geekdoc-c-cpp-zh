
## PROGRAMMING EXAMPLE: Sales Data Analysis

A company has six salespeople. Every month, they go on road trips to sell the company’s product. At the end of each month, the total sales for each salesperson, together with that salesperson’s ID and the month, is recorded in a file. At the end of each year, the manager of the company wants to see this report in the following tabular format:

| ID | QT1 | QT2 | QT3 | QT4 | Total |
|---:|---:|---:|---:|---:|---:|
| 12345 | 1892.00 | 0.00 | 494.00 | 322.00 | 2708.00 |
| 32214 | 343.00 | 892.00 | 9023.00 | 0.00 | 10258.00 |
| 23422 | 1395.00 | 1901.00 | 0.00 | 0.00 | 3296.00 |
| 57373 | 893.00 | 892.00 | 8834.00 | 0.00 | 10619.00 |
| 35864 | 2882.00 | 1221.00 | 0.00 | 1223.00 | 5326.00 |
| 54654 | 893.00 | 0.00 | 392.00 | 3420.00 | 4705.00 |
| Total | 8298.00 | 4906.00 | 18743.00 | 4965.00 |  |

Max Sale by SalesPerson: ID = 57373, Amount = $10619.00  
Max Sale by Quarter: Quarter = 3, Amount = $18743.00

In this report, QT1 stands for quarter 1 (months 1 to 3), QT2 for quarter 2 (months 4 to 6), QT3 for quarter 3 (months 7 to 9), and QT4 for quarter 4 (months 10 to 12).

The salespeople’s IDs are stored in one file; the sales data is stored in another file. The sales data is in the following form:

```
salesPersonID  month  saleAmount
.
.
.
```

Furthermore, the sales data is in no particular order; it is not ordered by ID.

A sample sales data is:

```
12345 1 893
32214 1 343
23422 3 903
57373 2 893
.
.
.
```

## PROBLEM ANALYSIS AND ALGORITHM DESIGN

Let us write a program that produces the output in the specified format.

- **Input** One file containing each salesperson’s ID and a second file containing the sales data.
- **Output** A file containing the annual sales report in the above format.

Based on the problem’s requirements, it is clear that the main components for each salesperson are the salesperson’s ID, quarterly sales amount, and total annual sales amount. Because the components are of different types, we can group them with the help of a struct, defined as follows:

```
struct salesPersonRec
{
    string ID;             // salesperson's ID
    double saleByQuarter[4];    // array to store the total
                                  // sales for each quarter
    double totalSale;      // salesperson's yearly sales amount
};
```

Because there are six salespeople, we use an array of six components, wherein each component is of type salesPersonRec, defined as follows:

```
salesPersonRec salesPersonList[NO_OF_SALES_PERSON];
```

wherein the value of NO_OF_SALES_PERSON is 6.

Because the program requires us to find the company’s total sales for each quarter, we need an array of four components to store the data. Note that this data will be used to determine the quarter in which the maximum sales were made. Therefore, the program also needs the following array:

```
double totalSaleByQuarter[4];
```

Recall that in C++, the array index starts with 0. Therefore, totalSaleByQuarter[0] stores data for quarter 1, totalSaleByQuarter[1] stores data for quarter 2, and so on.

We will refer to these variables throughout the discussion.

The array salesPersonList is shown in Figure 9-9.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_653_0.png)

The first step of the program is to read the salespeople’s IDs into the array `salesPersonList` and initialize the quarterly sales and total sales for each salesperson to 0. After this step, the array `salesPersonList` is as shown in Figure 9-10.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_653_1.png)

The next step is to process the sales data. Processing the sales data is quite straightforward. For each entry in the file containing the sales data:

- 1. Read the salesperson’s ID, month, and sale amount for the month.
- 2. Search the array `salesPersonList` to locate the component corresponding to this salesperson.
- 3. Determine the quarter corresponding to the month.
- 4. Update the sales for the quarter by adding the sale amount for the month.

Once the sales data file is processed:

- 1. Calculate the total sales by salesperson.
- 2. Calculate the total sales by quarter.
- 3. Print the report.

This discussion translates into the following algorithm:

- 1. Initialize the array `salesPersonList`.
- 2. Process the sales data.
- 3. Calculate the total sales by quarter.
- 4. Calculate the total sales by salesperson.
- 5. Print the report.
- 6. Calculate and print the maximum sales by salesperson.
- 7. Calculate and print the maximum sales by quarter.

To reduce the complexity of the main program, let us write a separate function for each of these seven steps.

This function reads the salesperson’s ID from the input file and stores the salesperson’s ID in the array `salesPersonList`. It also initializes the quarterly sales amount and the total sales amount for each salesperson to 0. The definition of this function is:

```
void initialize(ifstream& indata, salesPersonRec list[],
                 int listSize)
{
    int index;
    int quarter;

    for (index = 0; index < listSize; index++)
    {
        indata >> list[index].ID; // get salesperson's ID

        for (quarter = 0; quarter < 4; quarter++)
            list[index].saleByQuarter[quarter] = 0.0;

        list[index].totalSale = 0.0;
    }
} //end initialize
```

### Function `getData`

This function reads the sales data from the input file and stores the appropriate information in the array `salesPersonList`. The algorithm for this function is:

- 1. Read the salesperson’s ID, month, and sales amount for the month.
- 2. Search the array `salesPersonList` to locate the component corresponding to the salesperson. (Because the salesperson’s IDs are not sorted, we will use a sequential search to search the array.)
- 3. Determine the quarter corresponding to the month.
- 4. Update the sales for the quarter by adding the sales amount for the month.

Suppose that the entry read is:

```
57373  2  350
```

Here, the salesperson’s ID is 57373, the month is 2, and the sale amount is 350. Suppose that the array `salesPersonList` is as shown in Figure 9-11.

| `salesPersonList` | ID | Q1 | Q2 | Q3 | Q4 | `totalSale` |
|---|---:|---:|---:|---:|---:|---:|
| `salesPersonList[0]` | 12345 | 150.80 | 0.0 | 0.0 | 654.92 | 0.0 |
| `salesPersonList[1]` | 32214 | 0.0 | 439.90 | 0.0 | 0.0 | 0.0 |
| `salesPersonList[2]` | 23422 | 0.0 | 0.0 | 0.0 | 564.76 | 0.0 |
| `salesPersonList[3]` | 57373 | 354.80 | 0.0 | 0.0 | 0.0 | 0.0 |
| `salesPersonList[4]` | 35864 | 0.0 | 0.0 | 763.90 | 0.0 | 0.0 |
| `salesPersonList[5]` | 54654 | 783.45 | 0.0 | 0.0 | 563.80 | 0.0 |

**FIGURE 9-11** Array `salesPersonList`

Now, ID 57373 corresponds to the array component `salesPersonList[3]`, and month 2 corresponds to quarter 1. Therefore, you add 350 to 354.80 to get the new amount, 704.80. After processing this entry, the array `salesPersonList` is as shown in Figure 9-12.

| salesPersonList | ID | saleByQuarter | totalSale |
|---|---:|---|---:|
| salesPersonList[0] | 12345 | 150.80, 0.0, 0.0, 654.92 | 0.0 |
| salesPersonList[1] | 32214 | 0.0, 439.90, 0.0, 0.0 | 0.0 |
| salesPersonList[2] | 23422 | 0.0, 0.0, 0.0, 564.76 | 0.0 |
| salesPersonList[3] | 57373 | 704.80, 0.0, 0.0, 0.0 | 0.0 |
| salesPersonList[4] | 35864 | 0.0, 0.0, 763.90, 0.0 | 0.0 |
| salesPersonList[5] | 54654 | 783.45, 0.0, 0.0, 563.80 | 0.0 |

Annotations: ID = 57373; month = 2.

**FIGURE 9-12** Array salesPersonList after processing entry 57373 2 350

The definition of the function getData is:

```
void getData(ifstream infile, salesPersonRec list[],
             int listSize)
{
    int index;
    int quarter;
    string sID;
    int month;
    double amount;

    infile >> sID;      //get salesperson's ID

    while (infile)
    {
        infile >> month >> amount;  //get the sale month and
                                    //the sale amount

        for (index = 0; index < listSize; index++)
            if (sID == list[index].ID)
                break;
```
