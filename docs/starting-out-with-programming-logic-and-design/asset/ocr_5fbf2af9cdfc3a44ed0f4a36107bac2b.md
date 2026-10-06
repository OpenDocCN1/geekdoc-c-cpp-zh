# 11.3 Using a Loop to Repeat the Menu 465

```
// Variables for the fields
Declare String description
Declare Real quantity

// Declare an input file.
Declare inputFile coffeeFile

// Open the file.
Open coffeeFile "coffee.dat"

While NOT eof(coffeeFile)
// Read a record from the file.
Read coffeeFile description, quantity

// Display the record.
Display "Description: ", description,
"Quantity: ", quantity, " pounds"
End While

// Close the file.
Close coffeeFile
End Module
```

Figure 11-15 Flowchart for the displayRecords module in Program 11-6

![](bbox=[0.125, 0.523, 0.875, 0.915])