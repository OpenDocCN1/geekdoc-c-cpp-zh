# LAB 6-4 Desk-Check

Desk-check the code shown in Figure 6-34 three times, using the numbers 2, 5, and 100.

```
//declare variable
int number = 0;

//enter input item
cout << "Enter a number: ";
cin >> number;

//perform calculations
switch (number)
{
    case 1:
    case 2:
    case 3:
        number = number * 2;
        break;
    case 4:
    case 5:
        number = number + 5;
        break;
    default:
        number = number - 50;
}

//display number
cout << "Final number: " << number << endl;
```

Figure 6-34 Code for Lab 6-4

# LAB 6-5 Debug

Follow the instructions for starting C++ and running the program contained in the Lab6-5.cpp file. The file is contained in either the Cpp6\Chap06\Lab6-5 Project folder or the Cpp6\Chap06 folder.

Test the program using the following codes: 1, 2, 3, 4, 5, 9, and -3. Debug the program.