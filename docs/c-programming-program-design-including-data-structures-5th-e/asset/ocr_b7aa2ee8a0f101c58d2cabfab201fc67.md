```
```cpp
inventory::inventory(string n, int iNum, double cost, int inStock)
{
    name = n;
    itemNum = iNum;
    price = cost;
    unitsInStock = inStock;
}
```
```

Consider the following declarations:

```
```cpp
inventory item1;
inventory item2("Dryer");
inventory item3("Washer", 2345, 278.95);
inventory item4("Toaster", 8231, 34.49, 200);
```
```

For item1, the default constructor in Line 1 executes because no value is passed to this variable. For item2, the constructor in Line 2 executes because only one parameter, which is of type string, is passed, and it matches with the constructor in Line 2. For item3, the constructor in Line 3 executes because three parameters are passed to item3, and they match with the constructor in Line 3. Similarly, for item4, the constructor in Line 4 executes (see Figure 11-7).

![](bbox=[0.201, 0.492, 0.888, 0.69])

FIGURE 11-7  Effect of constructors on objects

> > **NOTE**
> > If the values passed to a class object do not match the parameters of any constructor and if no type conversion is possible, a compile-time error will be generated.