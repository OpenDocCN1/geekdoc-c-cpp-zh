`salePrice` denotes the selling price of the item, `stateSalesTax` denotes the state’s sales tax, `citySalesTax` denotes the city’s sales tax, `luxuryTax` denotes the luxury tax, `salesTax` denotes the total sales tax, and `amountDue` denotes the final price of the item.

To calculate the sales tax, we must know the selling price of the item and whether the item is a luxury item.

The `stateSalesTax` and `citySalesTax` can be calculated using the following formulas:

```
stateSalesTax = salePrice · 0.04
citySalesTax = salePrice · 0.015
```

Next, you can determine `luxuryTax` as follows:

```
if (item is a luxury item)
    luxuryTax = salePrice · 0.1
otherwise
    luxuryTax = 0
```

Next, you can determine `salesTax` as follows:

```
salesTax = stateSalesTax + citySalesTax + luxuryTax
```

Finally, you can calculate `amountDue` as follows:

```
amountDue = salePrice + salesTax
```

The algorithm to determine `salesTax` and `amountDue` is, therefore:

+   1. Get the selling price of the item.
+   2. Determine whether the item is a luxury item.
+   3. Find the state’s portion of the sales tax using the formula:
+      ```
+      stateSalesTax = salePrice · 0.04
+      ```
+   4. Find the city’s portion of the sales tax using the formula:
+      ```
+      citySalesTax = salePrice · 0.015
+      ```
+   5. Find the luxury tax using the following formula:
+      ```
+      if (item is a luxury item)
+          luxuryTax = salePrice · 0.1
+      otherwise
+          luxuryTax = 0
+      ```
+   6. Find `salesTax` using the formula:
+      ```
+      salesTax = stateSalesTax + citySalesTax + luxuryTax
+      ```
+   7. Find `amountDue` using the formula:
+      ```
+      amountDue = salePrice + salesTax
+      ```