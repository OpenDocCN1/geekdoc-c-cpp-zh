copy of that output statement. The member function’s parameter will be an Account object and the member function will output the object’s name and balance. You’ll then replace the six duplicated statements in main with calls to displayAccount, passing as an argument the specific Account object to output.

Modify Fig. 9.6 to define the following `displayAccount` function **before** `main`:

```
```cpp
void displayAccount(const Account& account) {
    // place the statement that displays
    // account's name and balance here
}
```
```

Replace the comment in the member function’s body with a statement that displays account’s name and balance.

Once you’ve defined `displayAccount`, modify `main` to replace the statements that display each Account’s name and balance with calls to `displayAccount` of the form:

```
```cpp
displayAccount(nameOfAccountObject);
```
```

Each call’s argument should be the `account1` or `account2` object, as appropriate. Then, test the updated program to ensure that it produces the same output as shown in Fig. 9.6.

# **9.13 (Complex Class)**

Create a class called `Complex` for performing arithmetic with complex numbers. Write a program to test your class. Complex numbers have the form

$$\mathrm{realPart} + \mathrm{imaginaryPart} * i$$

where $i$ is

$$\sqrt{-1}$$

Use double variables to represent the private data of the class. Provide a constructor that enables an object of this class to be initialized when it’s declared. The constructor should contain default values in case no initializers are provided. Provide public member functions that perform the following tasks:

+   a) **add**—Adds two Complex numbers: To form the real part of the result, add the real parts of the two Complex numbers. To form the imaginary part of the result, add the imaginary parts of two Complex numbers.
+   
+   b) **subtract**—Subtracts two Complex numbers: To form the real part of the result, subtract the real part of the Complex argument from the real part of the Complex object that calls subtract. To form the imaginary part of the result, subtract the imaginary part of the Complex argument from the imaginary part of the Complex object that calls subtract.
+   
+   c) **toString**—Returns a string representation of a Complex number in the form `(a, b)`, where a is the real part and b is the imaginary part.

In Chapter 11, you’ll learn how to overload +, − and << so you can write expressions like a + b and a - b and cout << a to add, subtract and output Complex objects. **[Note:** The C++ Standard Library provides its own class `complex` for complex-number arithmetic. For information on this class, visit http://en.cppreference.com/w/cpp/numeric/complex].