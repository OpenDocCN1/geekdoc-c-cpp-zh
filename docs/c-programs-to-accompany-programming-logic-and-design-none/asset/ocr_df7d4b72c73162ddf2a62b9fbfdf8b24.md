```
```cpp
// Get user input
cout << "Enter name: ";
cin.getline(name, STR_LENGTH);
cout << "Enter address: ";
cin.getline(address, STR_LENGTH);
cout << "Enter item number: ";
cin >> item;
cout << "Enter quantity: ";
cin >> quantity;
// Initialize loop index to 0
sub = 0;
// Loop through array
while(sub < SIZE)
{
    // Test to see if this item is a valid item
    if(item == valid_item[sub])
        foundIt = true;    // Set flag to true
    sub += 1;              // Increment loop index
}
// Test value of foundIt
if(foundIt == true)
    cout << MSG_YES << endl;
else
    cout << MSG_NO << endl;
return 0;
}
```
```

**Figure 6-4** Pseudocode and C++ code for mail-order program *(continued)*

As shown in Figure 6-4, when you translate the pseudocode to C++, you make a few changes. In both the pseudocode and the C++ code, the variable named `foundIt` is the flag. However, in the C++ code you assign the value `false` instead of the string constant "N" to the variable named `foundIt`. This is because the variable named `foundIt` is declared as a variable of the `bool` type. The bool data type is one of C++’s primitive data types and is only used to store true and false values.

Also, notice the pseudocode includes one statement to get the user’s name, address, item, and quantity, whereas it takes many statements in C++ to get the user’s input.

> > **NOTE** The variable named `foundIt` could be declared as a string as it was in the pseudocode. It is better to use a bool in C++ for true and false values.

> > **NOTE** Notice the mail-order program uses character arrays, not strings, to store the customer’s name and address. Character arrays must be used because the program uses the `getline()` function to retrieve the user’s input for name and address. You will learn about using character arrays to store strings and using the `getline()` function as you learn more about C++.