```
```cpp
25
26        // Call nameAndAddress function
27        nameAndAddress();
28        // Output customer name and address
29        cout << "Customer Name:  " << firstName << " " << lastName << endl;
30        cout << "Customer Balance:  " << balance << endl;
31
32        return 0;
33    } // End of main function
34
35    void nameAndAddress()
36    {
37        // Declare and initialize local, constant Strings
38        const string ADDRESS_LINE1 = "ABC Manufacturing";
39        const string ADDRESS_LINE2 = "47 Industrial Lane";
40        const string ADDRESS_LINE3 = "Wild Rose, WI 54984";
41
42        // Output
43        cout << ADDRESS_LINE1 << endl;
44        cout << ADDRESS_LINE2 << endl;
45        cout << ADDRESS_LINE3 << endl;
46    } // End of nameAndAddress function
```
```

**Figure 7-1** C++ code for Customer Bill program (*continued*)

On lines 1-6, you see a multiline comment that describes the Customer Bill program followed by two `#include` preprocessor directives on lines 7 and 8 that give the program the ability to perform input and output and the ability to use strings. On line 9, you see the function declaration for the `nameAndAddress` function. As with variables in C++, you must declare a function before you can call the function in your program. A **function declaration** (also known as a **function prototype**) should specify the data type of the value the function returns, the name of the function, and the data type of each of its arguments. On line 9 you see that the `nameAndAddress` function returns nothing (`void`) and expects no arguments.

The program begins execution with the `main` function, which is shown on line 11. This function contains the declaration of three variables (lines 14, 15, and 16), `firstName`, `lastName`, and `balance`, which are local to the `main` function. Next, on lines 19 through 24, interactive input statements retrieve values for `firstName`, `lastName`, and `balance`. The function `nameAndAddress` is then called on line 27, with no arguments listed within its parentheses. Remember that **arguments**, which are sometimes called **actual parameters**, are data items sent to functions. There are no arguments for the `nameAndAddress` function because this function requires no data. You will learn about passing arguments to functions later in this chapter. The last two statements (lines 29 and 30) in the `main` function are print statements that output the customer’s `firstName`, `lastName`, and `balance`.