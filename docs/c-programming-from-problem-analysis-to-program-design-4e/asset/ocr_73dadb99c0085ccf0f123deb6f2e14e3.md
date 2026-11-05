![](bbox=[0.198, 0.143, 0.773, 0.288])

**FIGURE 8-10** Class diagram

Figure 8-11 shows the Structured English, or pseudocode, used to design the step-by-step processes for the behaviors of the methods of the TempAgency example.

```
Main()
declare string array for salesman
declare double two-dim array for sales
DisplayInstructions()
GetSalesData(salesman, sales)
ProduceSalesProjectionTable(sales)
DisplaySalesProjections(salesman, sales)
```

```
DisplayInstructions( )
    Write message indicating what program will do
    Write message alerting user to what values will be entered
```

```
GetSalesData(string[ ] salesman, double[ , ] sales)
    Loop (for number of salesman — row)
        Write prompt to enter salesman name
        Read name into string salesman array
        Split name by space delimiters using Split( ) method
        Write prompt, including salesman first name for sales goal
        Parse sales amount
        Store sales amount in sales array in column 0
```

```
ProduceSalesProjectionTable(double[ , ] sales)
    Loop(for number of salesman — row)
        Initialize salesPercentage to 0.05
        Loop(for number of months — col)
            Store sales + increase in sales (row, col)
            Increment salesPercentage
            Increment col
        Increment row
```

```
DisplaySalesProjections(string[ ] salesman,
                         double[ , ] sales)
    declare string array for names
    Loop (for number of salesman — row)
        name = salesman.Split(' ')
        Write name[1] + ", " + name[0]
        Loop (for number of months + 1 — col)
            Write sales[row, col]
        Write blank line
```

**FIGURE 8-11** TempAgency class methods behavior