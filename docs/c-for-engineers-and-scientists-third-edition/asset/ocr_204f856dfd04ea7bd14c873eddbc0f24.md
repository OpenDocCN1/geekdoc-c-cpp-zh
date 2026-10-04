# Chapter 11

# Data Type Conversions

+   3. **(Debug)** a. Determine whether the following addition operator produces the same result as the function in Program 11.8:

```
Date::operator+(int days) // return a Date object
{
    temp.day = day + days; // add the days in
    temp.month = month + int(day/30); // determine total months
    temp.day = temp.day % 30; // determine actual day
    temp.year = year + int(temp.month/12); // determine total years
    temp.month = temp.month % 12; // determine actual month
    return temp;
}
```

+   b. Verify your answer to Exercise 3a by including the function in a working C++ program.

+   4. **(Modify)** a. Rewrite the equity relational operator function in Program 11.7

+   b. Verify the operation of the friend function written for Exercise 4a by including it in a working C++ program.

+   5. **(Modify)** a. Construct an addition operator for the Complex class declared in Program 11.6. It should be a member function that adds two complex numbers and returns a number.

+   b. Add a member multiplication operator function to the class used in Exercise 5a that multiplies two complex numbers and returns a complex number.

+   c. Verify the operation of the operator functions written for Exercises 5a and 5b by including them in a working C++ program.

+   6. **(Modify)** a. Rewrite the addition operator function in Program 11.8 to account for the actual days in a month, omitting leap years. (*Note*: This function requires an array to store the days in each month.)

+   b. Verify the operation of the operator function written for Exercise 6a by including it in a working C++ program.

# 11.4 Data Type Conversions

Sections 3.1 and 3.3 describe the conversion from one built-in data type to another. With the introduction of user-defined data types, the possibilities for conversion between data types expand to the following:

+   - Conversion from built-in type to built-in type
- Conversion from built-in type to class type
- Conversion from class type to built-in type
- Conversion from class type to class type

The first conversion is handled by C++'s implicit conversion rules or its explicit cast operator. The second conversion is made by using a type conversion constructor. The third