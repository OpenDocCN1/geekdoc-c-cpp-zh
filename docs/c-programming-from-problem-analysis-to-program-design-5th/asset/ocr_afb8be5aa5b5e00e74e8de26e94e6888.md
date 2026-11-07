Figure 12-16 shows the UML class diagram of the class `dispenserType`.

![](bbox=[0.2, 0.159, 0.895, 0.352])

**FIGURE 12-16**  UML class diagram of the class `dispenserType`

Because the candy machine sells four types of items, we shall declare four objects of type `dispenserType`. For example, the statement:

```
dispenserType chips(100, 65);
```

declares `chips` to be an object of type `dispenserType`, sets the number of chip bags in the dispenser to 100, and sets the cost of each chip bag to 65 cents (see Figure 12-17).

![](bbox=[0.2, 0.551, 0.895, 0.65])

**FIGURE 12-17**  Object `chips`

Next, we discuss the definitions of the functions to implement the operations of the class `dispenserType`.

The function `getNoOfItems` returns the number of items of a particular product. Because the number of items currently in the dispenser is stored in the private member variable `numberOfItems`, the function returns the value of `numberOfItems`. The definition of this function is:

```
int dispenserType::getNoOfItems() const
{
    return numberOfItems;
}
```