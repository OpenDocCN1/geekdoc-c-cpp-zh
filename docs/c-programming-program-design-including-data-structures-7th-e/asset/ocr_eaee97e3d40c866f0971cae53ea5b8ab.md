Figure 10-16 shows the UML class diagram of the `class dispenserType`.

![](bbox=[0.216, 0.179, 0.884, 0.368])

**FIGURE 10-16** UML class diagram of the `class dispenserType`

Because the juice machine sells four types of items, we shall declare four objects of type `dispenserType`. For example, the statement:

```
dispenserType apple(100, 65);
```

declares apple to be an object of type `dispenserType`, sets the number of apple juice bottles in the dispenser to 100, and sets the cost of each apple juice bottle to 65 cents (see Figure 10-17).

![](bbox=[0.216, 0.577, 0.884, 0.675])

**FIGURE 10-17** Object `apple`

Next, we discuss the definitions of the functions to implement the operations of the `class dispenserType`.

The function `getNoOfItems` returns the number of items of a particular product. Because the number of items currently in the dispenser is stored in the `private` member variable `numberOfItems`, the function returns the value of `numberOfItems`. The definition of this function is:

```
int dispenserType::getNoOfItems() const
{
    return numberOfItems;
}
```