If the user does not deposit enough money to buy the product, sellProduct tells the user how much additional money must be deposited. If the user fails to deposit enough money in two tries to buy the product, the function simply returns the money. (Programming Exercise 11, at the end of this chapter, asks you to revise the definition of the function sellProduct so that it keeps asking the user to enter the additional amount as long as the user has not entered enough money to buy the product.) If the amount deposited by the user is sufficient, it accepts the money and sells the product. Selling the product means to decrement the number of items in the dispenser by 1 and to update the money in the cash register by adding the cost of the product. (Because this program does not return the extra money deposited by the customer, the cash register is updated by adding the money entered by the user.)

From this discussion, it is clear that the function sellProduct must have access to the dispenser holding the product (to decrement the number of items in the dispenser by 1 and to show the cost of the item) as well as the cash register (to update the cash). Therefore, this function has two parameters: one corresponding to the dispenser and the other corresponding to the cash register. Furthermore, both parameters must be referenced.

In pseudocode, the algorithm for this function is:

+   1. If the dispenser is not empty,
+       a. Show and prompt the customer to enter the cost of the item.
+       b. Get the amount entered by the customer.
+       c. If the amount entered by the customer is less than the cost of the product,
+           i. Show and prompt the customer to enter the additional amount.
+           ii. Calculate the total amount entered by the customer.
+       d. If the amount entered by the customer is at least the cost of the product,
+           i. Update the amount in the cash register.
+           ii. Sell the product—that is, decrement the number of items in the dispenser by 1.
+           iii. Display an appropriate message.
+       e. If the amount entered by the user is less than the cost of the item, return the amount.
+   2. If the dispenser is empty, tell the user that this product is sold out.

This definition of the function sellProduct is:

```
    void sellProduct(dispenserType& product,
                     cashRegister& pCounter)
```