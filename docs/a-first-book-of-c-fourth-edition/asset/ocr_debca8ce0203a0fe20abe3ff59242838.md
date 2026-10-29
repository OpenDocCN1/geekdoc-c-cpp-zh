```
public:
    Checkout();  // constructor
    // the following is an inline destructor
    ~Checkout()
    {
        cout << "!!!! This Customer object has been deleted !!!!\n";
    }
    void showObject();
    void getItems(){return;}  // inline do-nothing methods
    void getTime() {return;}  // will be used in Program 12.5
};
```

```
// class implementation section
Checkout::Checkout()  // constructor
{
    cout << "\n**** A new Customer object has been created ****\n";
    numItems = 5;
    arrivalTime = 2.5;
}
```

```
void Checkout::showObject()
{
    cout << "\n    For this object:\n";
    cout << "        numItems = " << numItems
         << "\n        arrivalTime = " << arrivalTime << endl;
    return;
}
```

The constructor method causes the following display whenever an object is created:
**** A new Customer object has been created ****

Similarly, the destructor method, which is called automatically when an object is destroyed, causes the following message to be displayed:
!!!! This Customer object has been deleted !!!!

These messages are included to help you monitor creation and deletion of an object by using dynamic allocation. Table 12.2 describes two C++ operators, new and delete, that provide this capability. (These operators require the new header file.)

# Table 12.2 Dynamic Allocation and Deallocation Operators

| Operator Name | Description |
|---|---|
| new | Reserves the correct number of bytes for the variable or object type requested by the declaration. Returns the address of the first reserved location or a NULL value if not enough memory is available. |
| delete | Releases previously reserved memory. The address of the first reserved location must be passed as an argument to the operator. |