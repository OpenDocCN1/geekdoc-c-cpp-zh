```
```cpp
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
```

Now that we have described the functions showSelection and sellProduct, the function main is described next.

**main** The algorithm for the function `main` is as follows:

+   1. Create the cash register—that is, declare an object of type `cashRegister`.
+   2. Create four dispensers—that is, declare four objects of type `dispenserType` and initialize these objects. For example, the statement:
+   
+      `dispenserType orange(100, 50);`
+   
+      creates a dispenser object, orange, to hold the juice. The number of items in the dispenser is 100, and the cost of an item is 50 cents.