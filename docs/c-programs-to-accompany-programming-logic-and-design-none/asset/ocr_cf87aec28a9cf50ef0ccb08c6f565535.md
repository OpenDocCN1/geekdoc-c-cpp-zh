```
    1     // IncreaseSalary.cpp - This program demonstrates pass by reference.
    2     // Input:  None
    3     // Output:  Beginning salary along with new salary
    4     #include <iostream>
    5     using namespace std;
    6
    7     void increase(double, double, double&);
    8     int main()
    9     {
    10        double salary = 50000.00;
    11        double raise = .15;
    12        double new_salary;
    13
    14        cout << "Salary is: " << salary << endl;
    15
    16        // Call the increase function; the variables salary and raise
    17        // are passed by value, the variable new_salary is passed by
    18        // reference.
    19        increase(salary, raise, new_salary);
    20
    21        cout << "New salary is: " << new_salary << endl;
    22        return 0;
    23    } // End of main function
    24
    25    void increase(double amt, double pcnt, double& new_sal)
    26    {
    27        // Changes the value of new_salary in the main function
    28        new_sal = amt * (1 + pcnt);
    29        return;
    30    }
```

**Figure 7-7** Pass by reference example

On line 7 in Figure 7-7, you see the function declaration for the function named `increase`. The function declaration includes the data types for three arguments that are passed to the `increase` function. The first two arguments are doubles and the third argument is a reference to a double (`double&`). The function declaration on line 7 has been shaded in Figure 7-7.

On line 19, you see the function call to the `increase` function in the `main` function. The `increase` function is also shaded so you can easily see that it passes three arguments (`salary`, `raise`, and `new_salary`) that are all local variables declared in the `main` function.

On line 25, also shaded, you see the header for the `increase` function that includes three parameters, `double amt`, `double pcnt`, and `double& new_sal`. The first two arguments are passed by value, which means that `amt` contains a copy of the value stored in `salary` and `pcnt` contains a copy of the value stored in `raise`. The third argument is passed by reference, which means that `new_sal` is actually an alias for the variable `new_salary`. Because `new_sal` is an alias for `new_salary`, when the value of `new_sal` is changed on line 28, the value of `new_salary`, which is declared in the `main` function, is also changed.

> > **NOTE**
> >
> > In Chapter 3 of this book, you learned that local variables are not available to other functions in the program.