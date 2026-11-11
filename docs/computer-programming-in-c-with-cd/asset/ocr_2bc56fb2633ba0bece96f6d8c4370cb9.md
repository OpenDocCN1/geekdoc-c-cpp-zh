again to enter another number with a string, Enter third number: to store the value in the num3 variable. Now the program calculates the average of the three numbers that are stored in the variables (num1, num2, and num3). The result (average of these three variables) is displayed on the console screen.

# TEST YOUR KNOWLEDGE

**Q2.** Write a program to convert any number into hexadecimal, decimal, and octal equivalent.

Ans.

```
#include<iostream.h>
#include<fstream.h>

void main()
{
    int number;
    cout<<"Enter any integer number:";
    cin>>number;
    cout<<"Hexadecimal equivalent is:"<<hex<<number<<endl;
    cout<<"Decimal equivalent is:"<<dec<<number<<endl;
    cout<<"Octal equivalent is:"<<oct<<number<<endl;
}
```

**Output:**

Enter any integer number:12
Hexadecimal equivalent is:c
Decimal equivalent is:12
Octal equivalent is:14

C++ provides certain functions known as manipulators to format the results using cout and cin objects. Let’s now discuss these manipulators in detail in the following section.

# Working with Manipulators

Manipulators are functions used to control the format of input or output stream. These manipulators are used in conjunction with the insertion (`<<`) and extraction (`>>`) operators on stream objects. Some of the commonly used manipulators available in C++ are as follows:

+   - The endl manipulator
+   - The setw() manipulator
+   - The setprecision() manipulator
+   - The setfill() manipulator