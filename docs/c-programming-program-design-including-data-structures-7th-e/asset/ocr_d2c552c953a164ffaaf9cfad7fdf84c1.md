```
```cpp
do
{
    func1();
    cin >> choice;
    cout << endl;

    if (choice == 1)
    {
        func2(num1, num2, num3);
        cout << num1 << ", " << num2 << ", " << num3 << endl;
    }
}
while (choice != 99);

return 0;
}

void func1()
{
    cout << "To run the program, enter 1." << endl;
    cout << "To exit the program, enter 99." << endl;
    cout << "Enter 1 or 99: ";
}

void func2(/*formal parameters*/)
{
    //Write the body of func2.
}
```
```

The function `func2` has three parameters of type `int`, `int`, and `double`, say a, b, and c, respectively. Write the definition of the function `func2` so that its action is as follows:

+   a. Prompt the user to input two integers and store the numbers in a and b, respectively.
+   
+   b. If both of the numbers are nonzero:
+      i. If a >= b, the value assigned to c is a to the power b, that is, a^b.
+      ii. If a < b, the value assigned to c is b to the power a, that is, b^a.
+   
+   c. If a is nonzero and b is zero, the value assigned to c is the square root of the absolute value of a.
+   
+   d. If b is nonzero and a is zero, the value assigned to c is the square root of the absolute value of b.
+   
+   e. Otherwise, the value assigned to c is 0.

The values of a, b, and c are passed back to the calling environment.

After completing the definition of the `func2` and writing its function prototype, test run your program.