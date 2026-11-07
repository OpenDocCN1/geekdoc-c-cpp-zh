```
```cpp
switch (customerType)                                      //Step 7
{
case 'r':                                                   //Step 7a
case 'R':                                                   //Step 7a.i
    amountDue = residential();
    cout << "Account number = "
         << accountNumber << endl;                         //Step 7a.ii
    cout << "Amount due = $"
         << amountDue << endl;                              //Step 7a.iii
    break;
case 'b':                                                   //Step 7b
case 'B':                                                   //Step 7b.i
    amountDue = business();
    cout << "Account number = "
         << accountNumber << endl;                         //Step 7b.ii
    cout << "Amount due = $"
         << amountDue << endl;                              //Step 7b.iii
    break;
default:
    cout << "Invalid customer type." << endl;               //Step 7c
}

return 0;
}

//Place the definitions of the functions residential and business here.
```
```

**Sample Run:** This sample run, the user input is shaded.

```
This program computes a cable bill.
Enter account number: 21341

Enter customer type: R, r (Residential), B, b (Business): B

Enter the number of basic service connections: 25

Enter the number of premium channels used: 9

Account number = 21341
Amount due = $615.00
```

# Flow of Compilation and Execution

As stated earlier, a C++ program is a collection of functions. Recall that functions can appear in any order. The only thing that you have to remember is that you must declare an identifier before you can use it. The program is compiled by the compiler sequentially from beginning to end. Thus, if the function `main` appears before any other user-defined functions, it is compiled first. However, if `main` appears at the end (or middle) of the program, all functions whose definitions (not prototypes) appear before the function `main` are compiled before the function `main`, in the order they are placed.