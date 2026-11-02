difference between object and instance isn't terribly important. But it's very important to remember that the words object and instance have the same meaning. (Okay! They have nearly the same meaning.)

# Making reference to an object's parts

After you've created an object, you use dots to refer to the object's parts. For example, in Listing 17-3, I put a value into the onePurchase object's amount part with the following code:

```
onePurchase.amount = keyboard.nextDouble();
```

Later in Listing 17-3, I get the amount part's value with the following code:

```
onePurchase.total = onePurchase.amount * 1.05;
```

This dot business may look cumbersome, but it really helps programmers when they're trying to organize the code. In Listing 17-1, each variable is a separate entity. But in Listing 17-3, each use of the word amount is inextricably linked to the notion of a purchase. That's good.

# Creating several objects

After you've created a Purchase class, you can create as many purchase objects as you want. For example, in Listing 17-5, I create three purchase objects.

# Listing 17-5: Processing Purchases

```
import java.util.Scanner;

class ProcessPurchases {
    public static void main(String args[]) {
        Scanner keyboard = new Scanner(System.in);
        Purchase aPurchase;
        for (int count = 0; count < 3; count++) {
            aPurchase = new Purchase();
            System.out.print("Amount: ");
            aPurchase.amount = keyboard.nextDouble();
            System.out.print("Taxable? (true/false) ");
            aPurchase.taxable = keyboard.nextBoolean();
            if (aPurchase.taxable) {
                aPurchase.total = aPurchase.amount * 1.05;
            }
        }
    }
}
```