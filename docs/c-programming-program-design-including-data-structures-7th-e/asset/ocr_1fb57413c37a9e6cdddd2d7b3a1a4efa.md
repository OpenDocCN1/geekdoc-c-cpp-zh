```
```cpp
15.  partsType inventory [100];
17.  void getData(partsType& pType)
    {
        for (int j = 0; j < length; j++)
        {
            cin >> pType.partName;
            cin >> pType.partNum;
            cin >> pType.price;
            cin >> pType.quantitiesInStock;
        }
    }

    for (int j = 0; j < 100; j++)
        getData(inventory[i]);
```
```

# # Chapter 10

+   1. a. false; b. false; c. true; d. false; e. false

3. The type of function `print` is missing. Also, a constructor has no type. The statements in Lines 5 and 6 should be:

```
```cpp
void print() const;              //Line 5
temp(int = 0, int = 0);          //Line 6
```
```

5. A class is not a function. The semicolon after `private` should be a colon, there is a missing semicolon after `}`, and a constructor has no type. The statements in Lines 1, 8, 9, and 13 should be:

```
```cpp
class discover()                    //Line 1

discover(string, int, int);        //Line 8
private:                             //Line 9
};                                  //Line 13
```
```

+   7. a. `void bagType::set(string s, double a, double b, double c, double d)`

```
```cpp
{
    style = s;
    l = a;
    w = b;
    h = c;
    price = d;
}
```
```

+   b. `void bagType::print() const`

```
```cpp
{
    cout << "Bag Type: " << style << ", length = " << l
```
```