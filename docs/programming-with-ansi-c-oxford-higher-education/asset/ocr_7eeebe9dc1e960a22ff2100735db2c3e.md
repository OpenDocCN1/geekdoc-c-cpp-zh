```
cout << "Parameterized constructor is called for" << CustName << "\n";
}

void ShowDetails()
{
    cout << "\n Customer number is " << CustNo;
    cout << "\n Customer name is " << CustName;
    cout << "\n Customer address is " << CustAddress;
    cout << "\n" << CustName << " is interested in following items" << "\n";
    for(int i = 0; i < TotalItems; i++)
    {
        ItemsInterested[i].ShowDetails();
    }
}
};

customer::~customer()
{
    cout << "Destructor is called for " << CustName << "\n";
    delete [] ItemsInterested;
}

void main()
{
    Item ItemArray[]=
    {
        Item(3, "Sandwiches"), Item(4, "Paper Bags"), Item(5, "Napkins"), Item(6, "Toys"),
        Item(10, "Bananas"), Item(9, "Pen"), Item(1, "Pencil"), Item(2, "Eraser"),
    };

    customer Steve (1, "Steve Waugh", "Australia", ItemArray + 2, 6);
    Steve.ShowDetails();
    customer Mark (2, "Mark Waugh", "Australia", ItemArray + 2, 3);
    Mark.ShowDetails();
    customer Beckham;
    /* Overloading the assignment operator is mandatory here */
    Beckham = customer (3, "David Beckham", "England", ItemArray, 5);
    Beckham.ShowDetails();
}
```

# Need for Overloading Assignment Operator

The following statement will not work if the assignment operator is not overloaded:

```
Beckham = customer(3, "David Beckham", "England", ItemArray, 5)
```

This is because the compiler creates a new temporary object from the RHS expression to pass it on to the LHS. Immediately after the execution of the assignment statement, the temporary object is destroyed. It destroys the dynamically allocated list of items. Memberwise copy will only copy the pointer value and not the content; it would destroy the items that are pointed to by the pointer of Beckham.ItemsInterested as well. This is similar to the problem that occurred during initialization. Copy constructors have been used to solve this problem.