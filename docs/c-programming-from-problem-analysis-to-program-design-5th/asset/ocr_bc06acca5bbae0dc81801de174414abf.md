# # Friendly Hardware Store

| itemID | itemName | pOrdered | pInStore | pSold | manufPrice | sellingPrice |
|---|---|---|---|---|---|---|
| 4444 | Circular Saw | 150 | 150 | 40 | 45.00 | 125.00 |
| 3333 | Cooking Range | 50 | 50 | 20 | 450.00 | 850.00 |
| . |  |  |  |  |  |  |
| . |  |  |  |  |  |  |

Total Inventory: $########.##  
Total number of items in the store: ________

The total inventory is the total selling value of all of the items currently in the store. The total number of items is the sum of the number of pieces of all of the items in the store.

Your program must be menu driven, giving the user various choices, such as checking whether an item is in the store, selling an item, and printing the report. After inputting the data, sort it according to the items' names. Also, after an item is sold, update the appropriate counts.

Initially, the number of pieces (of an item) in the store is the same as the number of pieces ordered, and the number of pieces of an item sold is zero. Input to the program is a file consisting of data in the following form:

```
    itemID
    itemName
    pOrdered manufPrice sellingPrice
```

Use seven parallel vectors to store the information. The program must contain at least the following functions: one to input data into the vectors, one to display the menu, one to sell an item, and one to print the report for the manager.