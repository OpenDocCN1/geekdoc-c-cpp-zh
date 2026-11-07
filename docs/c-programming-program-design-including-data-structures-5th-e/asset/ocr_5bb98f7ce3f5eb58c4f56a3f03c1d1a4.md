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

# EXAMPLE 1-3

In this example, we design an algorithm that calculates the monthly paycheck of a salesperson at a local department store.

Every salesperson has a base salary. The salesperson also receives a bonus at the end of each month, based on the following criteria: If the salesperson has been with the store for five years or less, the bonus is $10 for each year that he or she has worked there. If the salesperson has been with the store for more than five years, the bonus is $20 for each year that he or she has worked there. The salesperson can earn an additional bonus as follows: If the total sales made