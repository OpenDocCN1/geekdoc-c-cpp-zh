# CHAPTER 6 Using Arrays

```
using System;
using static System.Console;
class FindPriceWithWhileLoop {
    static void Main() {
        int x;
        string inputOrdered;
        int itemOrdered;
        double itemPrice = 0;
        bool isValidItem = false;
        int[] validValues = {101, 108, 201, 213, 266, 304, 311, 409, 412};
        double[] prices = {0.89, 1.26, 3.50, 0.69, 5.79, 3.19, 0.99, 0.89, 1.26, 8.00};
        Write("Enter item number ");
        inputString = ReadLine();
        itemOrdered = Convert.ToInt32(inputString);
        x = 0;
        while(x < validValues.Length && itemOrdered != validValues[x]) {
            x++;
        }
        if(x != validValues.Length) {
            isValidItem = true;
            itemPrice = prices[x];
        }
        if(isValidItem)
            WriteLine("{0} sells for {1}", itemOrdered, itemPrice.ToString("C"));
        else
            WriteLine("No such item as {0}", itemOrdered);
    }
}
```

**Figure 6-6** The FindPriceWithWhileLoop program that searches with a while loop

In the application of Figure 6-6, the variable used as a subscript, x, is set to 0 and the Boolean variable isValidItem is false. In the shaded portion of the figure, the subscript remains smaller than the length of the array of item numbers, and the user’s requested item does not match a valid item, the subscript is increased so that subsequent array values can be tested. The while loop ends when a match is found or the array tests have been exhausted, whichever comes first. When x is not equal to the size of the array, a valid item has been found, and its price can be retrieved from the prices array. Figure 6-7 shows two executions of the program. In the first execution, a match is found; in the second, an invalid item is entered, so no match is found.

Copyright 2018 Cengage Learning. All Rights Reserved. No may be copied, scanned, or duplicated, in whole or in part. WCN-022-200-202