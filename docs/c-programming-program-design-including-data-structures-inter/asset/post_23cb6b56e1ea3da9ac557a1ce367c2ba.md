
```cpp
int getCost() const;
//Function to show the cost of the item.
//Postcondition: The value of cost is returned.

void makeSale();
//Function to reduce the number of items by 1.
//Postcondition: numberOfItems--;

dispenserType(int setNoOfItems = 50, int setCost = 50);
//Constructor
//Sets the cost and number of items in the dispenser
//to the value specified by the user.
//Postcondition: numberOfItems = setNoOfItems;
//              cost = setCost;
//              If no value is specified for a
//              parameter, then its default value is
//              assigned to the corresponding member
//              variable.

private:
    int numberOfItems;    //variable to store the number of
                          //items in the dispenser
    int cost;             //variable to store the cost of an item
};
```

Figure 10-16 shows the UML class diagram of the class dispenserType.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_725_0.png)

**FIGURE 10-16** UML class diagram of the class dispenserType

Because the juice machine sells four types of items, we shall declare four objects of type dispenserType. For example, the statement:

```cpp
dispenserType apple(100, 65);
```

declares apple to be an object of type dispenserType, sets the number of apple juice bottles in the dispenser to 100, and sets the cost of each apple juice bottle to 65 cents (see Figure 10-17).

```cpp
if (setCost >= 0)
    cost = setCost;
else
    cost = 50;
}
```

## MAIN PROGRAM

When the program executes, it must do the following:

- 1. Show the different products sold by the juice machine.
- 2. Show how to select a particular product.
- 3. Show how to terminate the program.

Furthermore, these instructions must be displayed after processing each selection (except exiting the program) so that the user need not remember what to do if he or she wants to buy two or more items. Once the user has made the appropriate selection, the juice machine must act accordingly. If the user has opted to buy a product and that product is available, the juice machine should show the cost of the product and ask the user to deposit the money. If the amount deposited is at least the cost of the item, the juice machine should sell the item and display an appropriate message.

This discussion translates into the following algorithm:

- 1. Show the selection to the customer.
- 2. Get the selection.
- 3. If the selection is valid and the dispenser corresponding to the selection is not empty, sell the product.

We divide this program into three functions: showSelection, sellProduct, and main.

### showSelection

This function displays the information necessary to help the user select and buy a product. This definition of the function showSelection is:

```cpp
void showSelection()
{
    cout << "*** Welcome to Shelly's Juice Shop ***" << endl;
    cout << "To select an item, enter " << endl;
    cout << "1 for orange juice" << endl;
    cout << "2 for apple juice" << endl;
    cout << "3 for mango juice" << endl;
    cout << "4 for strawberry banana juice" << endl;
    cout << "9 to exit" << endl;
}//end showSelection
```

### sellProduct

This function attempts to sell the product selected by the customer. Therefore, it must have access to the dispenser holding the product. The first thing that this function does is check whether the dispenser holding the product is empty. If the dispenser is empty, the function informs the customer that this product is sold out. If the dispenser is not empty, it tells the user to deposit the necessary amount to buy the product. If the user does not deposit enough money to buy the product, sellProduct tells the user how much additional money must be deposited. If the user fails to deposit enough money in two tries to buy the product, the function simply returns the money. (Programming Exercise 11, at the end of this chapter, asks you to revise the definition of the function sellProduct so that it keeps asking the user to enter the additional amount as long as the user has not entered enough money to buy the product.) If the amount deposited by the user is sufficient, it accepts the money and sells the product. Selling the product means to decrement the number of items in the dispenser by 1 and to update the money in the cash register by adding the cost of the product. (Because this program does not return the extra money deposited by the customer, the cash register is updated by adding the money entered by the user.)

From this discussion, it is clear that the function sellProduct must have access to the dispenser holding the product (to decrement the number of items in the dispenser by 1 and to show the cost of the item) as well as the cash register (to update the cash). Therefore, this function has two parameters: one corresponding to the dispenser and the other corresponding to the cash register. Furthermore, both parameters must be referenced.

In pseudocode, the algorithm for this function is:

- 1. If the dispenser is not empty,
  - a. Show and prompt the customer to enter the cost of the item.
  - b. Get the amount entered by the customer.
  - c. If the amount entered by the customer is less than the cost of the product,
    - i. Show and prompt the customer to enter the additional amount.
    - ii. Calculate the total amount entered by the customer.
  - d. If the amount entered by the customer is at least the cost of the product,
    - i. Update the amount in the cash register.
    - ii. Sell the product—that is, decrement the number of items in the dispenser by 1.
    - iii. Display an appropriate message.
  - e. If the amount entered by the user is less than the cost of the item, return the amount.
- 2. If the dispenser is empty, tell the user that this product is sold out.

This definition of the function sellProduct is:

```cpp
void sellProduct(dispenserType& product,
                 cashRegister& pCounter)
{
    int amount;   //variable to hold the amount entered
    int amount2;  //variable to hold the extra amount needed

    if (product.getNoOfItems() > 0) //if the dispenser is not
                                    //empty
    {
        cout << "Please deposit " << product.getCost()
             << " cents" << endl;
        cin >> amount;

        if (amount < product.getCost())
        {
            cout << "Please deposit another "
                 << product.getCost() - amount
                 << " cents" << endl;
            cin >> amount2;
            amount = amount + amount2;
        }

        if (amount >= product.getCost())
        {
            pCounter.acceptAmount(amount);
            product.makeSale();
            cout << "Collect your item at the bottom and "
                 << "enjoy." << endl;
        }
        else
            cout << "The amount is not enough. "
                 << "Collect what you deposited." << endl;
        cout << "*******************************"
             << endl << endl;
    }
    else
        cout << "Sorry, this item is sold out." << endl;
}//end sellProduct
```

Now that we have described the functions showSelection and sellProduct, the function main is described next.

### main

The algorithm for the function `main` is as follows:

- 1. Create the cash register—that is, declare an object of type `cashRegister`.
- 2. Create four dispensers—that is, declare four objects of type `dispenserType` and initialize these objects. For example, the statement:

  `dispenserType orange(100, 50);`

  creates a dispenser object, orange, to hold the juice. The number of items in the dispenser is 100, and the cost of an item is 50 cents.
- 3. Declare additional variables as necessary.
- 4. Show the selection; call the function `showSelection`.
- 5. Get the selection.
- 6. While not done (a selection of 9 exits the program),
  - a. Sell the product; call the function `sellProduct`.
  - b. Show the selection; call the function `showSelection`.
  - c. Get the selection.

The definition of the function main is as follows:

```cpp
int main()
{
    cashRegister counter;
    dispenserType orange(100, 50);
    dispenserType apple(100, 65);
    dispenserType mango(75, 80);
    dispenserType strawberryBanana(100, 85);

    int choice;  //variable to hold the selection

    showSelection();
    cin >> choice;

    while (choice != 9)
    {
        switch (choice)
        {
            case 1:
                sellProduct(orange, counter);
                break;
            case 2:
                sellProduct(apple, counter);
                break;
            case 3:
                sellProduct(mango, counter);
                break;
            case 4:
                sellProduct(strawberryBanana, counter);
                break;
            default:
                cout << "Invalid selection." << endl;
        }//end switch

        showSelection();
        cin >> choice;
    }//end while

    return 0;
}//end main
```
