
4. 10 20
20 20
30 20

5. To the unwary or to the neophyte, this looks like two objects of type pointer to int, that is, int*. Unfortunately, the * binds to the identifier, not to the type (that is, not to the int). The result is that this declaration declares intPtr1 to be an int pointer, while intPtr2 is an ordinary int variable.

```
6. delete p;
```

```
7. typedef double* NumberPtr;
NumberPtr myPoint;
```

8. The new operator takes a type for its argument. new allocates space on the freestore manager for a variable of the type of the argument. It returns a pointer to that memory, provided there is enough space. If there is not enough space, the new operator may return NULL, or may abort the program, depending on how your particular compiler works.

```
9. typedef char* CharArray;
```

```
10. cout << "Enter 10 integers:\n";
for (int i = 0; i < 10; i++)
    cin >> entry[i];
```

```
11. delete [] entry;
```

12. 0 1 2 3 4 5 6 7 8 9

13. The constructor is named MyClass, the same name as the name of the class. The destructor is named ~MyClass.

14. The dialogue would change to the following:

```
This program tests the class PFArrayD.
Enter capacity of this super array: 10
Enter up to 10 nonnegative numbers.
Place a negative number at the end.
1.1
2.2
3.3
4.4
-1
You entered the following 4 numbers:
1.1 2.2 3.3 4.4
(plus a sentinel value.)
Good-bye cruel world! The short life of
this dynamic array is about to end.
Test again? (y/n) n
```

15. The `PFArrayD` before the `::` is the name of the class. The `PFArrayD` right after the `::` is the name of the member function. (Remember, a constructor is a member function that has the same name as the class.) The `PFArrayD` inside the parentheses is the type for the parameter `pfArrayObject`.

16.
- a. A destructor is a member function of a class. A destructor’s name always begins with a tilde, `~`, followed by the class name.
- b. A destructor is called when a class object goes out of scope.
- c. A destructor actually does whatever the class author programs it to do!
- d. A destructor is *supposed* to delete dynamic variables that have been allocated by constructors for the class. Destructors may also do other clean-up tasks.

17. In the case of the assignment operator `=` and the copy constructor, if there are only built-in types for data, the copy mechanism is exactly what you want, so the default works fine. In the case of the destructor, no dynamic memory allocation is done (no pointers), so the default do-nothing action is again what you want.

## Programming Projects

1. Reread the code in Display 10.9. Then, write a class `TwoD` that implements the two-dimensional dynamic array of doubles using ideas from this display in its constructors. You should have a private member of type pointer to double to point to the dynamic array, and two `int` (or unsigned int) values that are `MaxRows` and `MaxCols`.

You should supply a default constructor for which you are to choose a default maximum row and column sizes and a parameterized constructor that allows the programmer to set maximum row and column sizes.

Further, you should provide a `void` member function that allows setting a particular row and column entry and a member function that returns a particular row and column entry as a value of type double.

Remark: It is difficult or impossible (depending on the details) to overload `[ ]` so it works as you would like for two-dimensional arrays. So simply use accessor and mutator functions using ordinary function notation.

Overload the `+` operator as a friend function to add two two-dimensional arrays. This function should return the `TwoD` object whose `i`th row, `j`th column element is the sum of the `i`th row, `j`th column element of the left-hand operand `TwoD` object and the `i`th row, `j`th column element of the right-hand operand `TwoD` object.

Provide a copy constructor, an overloaded operator `=`, and a destructor.

Declare class member functions that do not change the data as `const` members.

2. Using dynamic arrays, implement a polynomial class with polynomial addition, subtraction, and multiplication.

Discussion: A variable in a polynomial does nothing but act as a placeholder for the coefficients. Hence, the only interesting thing about polynomials is the array of coefficients and the corresponding exponent. Think about the polynomial

x*x*x + x + 1

Where is the term in x*x? One simple way to implement the polynomial class is to use an array of type double to store the coefficients. The index of the array is the exponent of the corresponding term. If a term is missing, then it simply has a zero coefficient.

There are techniques for representing polynomials of high degree with many missing terms. These use so-called sparse matrix techniques. Unless you already know these techniques, or learn very quickly, do not use these techniques.

Provide a default constructor, a copy constructor, and a parameterized constructor that enables an arbitrary polynomial to be constructed.

Supply an overloaded operator = and a destructor.

Provide these operations:
- polynomial + polynomial, constant + polynomial, polynomial + constant,
- polynomial − polynomial, constant − polynomial, polynomial − constant,
- polynomial * polynomial, constant * polynomial, polynomial * constant,

Supply functions to assign and extract coefficients, indexed by exponent.

Supply a function to evaluate the polynomial at a value of type double.

You should decide whether to implement these functions as members, friends, or standalone functions.

3. Write a program that accepts a line of text input from the user and checks if the number of words counted from both end of the text is equal. Your program should work by using two pointers. The “head” pointer should be set to the address of the first character in the string, and the “tail” pointer should be set to the address of the last character in the string (i.e., the character before the terminating null). The program should keep incrementing the “head” pointer and keep decrementing the “tail” pointer until the pointers are at the other end. On finding whitespace characters while going across the string, increment the word counts and compare them at the end.

4. Create a class named Subscriber that has three member variables:

- `name` — A string that stores the name of the subscriber
- `numChannels` — An integer that tracks how many channels the subscriber subscribes to.
- `channelList` — A dynamic array of strings used to store the names of the channels the subscriber subscribes to.

Write appropriate constructor(s), mutator, and accessor functions for the class along with the following:

- A function that inputs all values from the user, including the list of channel names. This function will have to support input for an arbitrary number of channels.
- A function that outputs the name and list of all channels.
- A function that resets the number of channels to 0 and the channelList to an empty list.
- An overloaded assignment operator that correctly makes a new copy of the list of channels.
- A destructor that releases all memory that has been allocated.
Write a main function that tests all your functions.

5. This programming project is based on Programming Projects 7.8 and 5.7. Write a program that outputs a histogram of grades for an assignment given to a class of students. The program should input each student's grade as an integer and store the grade in a vector. Grades should be entered until the user enters -1 for a grade. The program should then scan through the vector and compute the histogram. In computing the histogram, the minimum value of a grade is 0, but your program should determine the maximum value entered by the user. Use a dynamic array to store the histogram. Output the histogram to the console.

6. One problem with dynamic arrays is that once the array is created using the new operator the size cannot be changed. For example, you might want to add or delete entries from the array similar to the behavior of a vector. This project asks you to create a class called DynamicStringArray that includes member functions that allow it to emulate the behavior of a vector of strings.

The class should have the following:

- A private member variable called dynamicArray that references a dynamic array of type string.
- A private member variable called size that holds the number of entries in the array.
- A default constructor that sets the dynamic array to nullptr and sets size to 0.
- A function that returns size.
- A function named addEntry that takes a string as input. The function should create a new dynamic array one element larger than dynamicArray, copy all elements from dynamicArray into the new array, add the new string onto the end of the new array, increment size, delete the old dynamicArray, and then set dynamicArray to the new array.
- A function named deleteEntry that takes a string as input. The function should search dynamicArray for the string. If not found, it returns false. If found, it creates a new dynamic array one element smaller than dynamicArray. It should copy all elements except the input string into the new array, delete dynamicArray, decrement size, and return true.

![](img/c76bba8c1d927f399768ffe2ab5f5bee_503_0.png)
