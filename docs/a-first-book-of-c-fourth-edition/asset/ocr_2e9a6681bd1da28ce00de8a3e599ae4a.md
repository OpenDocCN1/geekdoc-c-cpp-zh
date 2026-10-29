```
else
    cout << "\nNo record has been created.";

return 0;
}
// input a name and phone number
void populate(TeleType *record)  // record is a pointer to a
{                               // structure of type TeleType
    cout << "Enter a name: ";
    getline(cin, record->name);
    cout << "Enter the phone number: ";
    getline(cin, record->phoneNo);

    return;
}
// display the contents of one record
void dispOne(TeleType *contents)  // contents is a pointer to a
{                                // structure of type TeleType
    cout << "\nThe contents of the record just created are:"
         << "\nName: " << contents->name
         << "\nPhone Number: " << contents->phoneNo << endl;

    return;
}
```

A sample run of Program 16.7 is as follows:

```
Do you want to create a new record (respond y or n): y
Enter a name: Monroe, James
Enter the phone number: (555) 617-1817
The contents of the record just created are:
Name: Monroe, James
Phone Number: (555) 617-1817
```

In reviewing Program 16.7, notice that only two variable declarations are made in main(). The variable key is declared as a character variable, and the variable recPoint is declared as a pointer to a structure of the TeleType type. Because the declaration for the TeleType type is global, TeleType can be used in main() to define recPoint as a pointer to a structure of the TeleType type.

If a user enters y in response to the first prompt in main(), a call to new is made for the required memory to store the designated structure. After recPoint has been loaded with the correct address, this address can be used to access the newly created structure.

The populate() function is used to prompt the user for data needed in filling the structure and to store the user-entered data in the correct structure members. The argument passed to populate() in main() is the pointer recPoint. Like all passed arguments, the value in