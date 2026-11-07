17. To find the price per square inch, first we need to find the area of the pizza. Then we divide the price of the pizza by the area of the pizza. Let radius denote the radius, area denote the area of the circle, and price denote the price of the pizza. Also, let pricePerSquareInch denote the price per square inch.

+   a. Get radius.
+   
+   b. area = π * radius * radius
+   
+   c. Get price.
+   
+   d. pricePerSquareInch = price / area

19. To calculate the selling price of an item, we need to know the original price (the price the store pays to buy) of the item. We can then use the following formula to find the selling price.

```
sellingPrice = originalPrice + originalPrice * .60
```

The algorithm is as follows:

+   a. Get originalPrice.
+   
+   b. Calculate the sellingPrice using the formula:

```
sellingPrice = originalPrice + originalPrice * .60
```

The information needed to calculate the selling price is the original price and the marked-up percentage.

21. Suppose that numOfPages denotes the number of pages to be faxed, and billingAmount denotes the total charges for the pages faxed. To calculate the total charges, you need to know the number of pages faxed.

If numOfPages is less than or equal to 10, the billing amount is service charges + (numOfPages × 0.20); otherwise, billing amount is service charges + 10 × 0.20 + (numOfPages − 10) × 0.10. That is,

You can now write the algorithm as follows:

+   a. Get numOfPages.
+   
+   b. Calculate billing amount using the formula:

```
if (numOfPages is less than or equal to 10)

    billingAmount = 3.00 + (numOfPages × 0.20);

otherwise

    billingAmount = 3.00 + 10 × 0.20 + (numOfPages − 10) × 0.10;
```

23. Suppose averageTestScore denotes the average test score, highestScore denotes the highest test score, testScore denotes a test score, sum denotes the sum of all of the test scores, count denotes the number of students in class, and studentName denotes the name of a student.