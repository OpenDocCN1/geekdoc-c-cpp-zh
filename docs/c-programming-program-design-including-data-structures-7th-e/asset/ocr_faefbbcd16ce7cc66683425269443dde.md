```
if (1 <= month && month <= 3)
    quarter = 0;
else if (4 <= month && month <= 6)
    quarter = 1;
else if (7 <= month && month <= 9)
    quarter = 2;
else
    quarter = 3;

if (index < listSize)
    list[index].saleByQuarter[quarter] += amount;
else
    cout << "Invalid salesperson's ID." << endl;

infile >> sID;
} //end while
} //end getData
```

**Function saleByQuarter**

This function finds the company's total sales for each quarter. To find the total sales for each quarter, we add the sales amount of each salesperson for that quarter. Clearly, this function must have access to the array salesPersonList and the array totalSaleByQuarter. This function also needs to know the number of rows in each array. Thus, this function has three parameters. The definition of this function is:

```
void saleByQuarter(salesPersonRec list[], int listSize,
                   double totalByQuarter[])
{
    int quarter;
    int index;

    for (quarter = 0; quarter < 4; quarter++)
        totalByQuarter[quarter] = 0.0;

    for (quarter = 0; quarter < 4; quarter++)
        for (index = 0; index < listSize; index++)
            totalByQuarter[quarter] +=
                list[index].saleByQuarter[quarter];
} //end saleByQuarter
```

**Function totalSaleByPerson**

This function finds each salesperson's yearly sales amount. To find an employee's yearly sales amount, we add that employee's sales amount for the four quarters. Clearly, this function must have access to the array salesPersonList. This function also needs to know the size of the array. Thus, this function has two parameters.

The definition of this function is:

```
void totalSaleByPerson(salesPersonRec list[], int listSize)
{
    int index;
    int quarter;
```

9