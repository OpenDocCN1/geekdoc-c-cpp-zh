Assume that **myObject1** and **myObject2** are as declared in Parts e and f. What is the output of the following C++ code?

```
```cpp
myObject1.printX();
cout << endl;
myObject1.incrementCount();
myClass::incrementCount();
myObject1.printCount();
cout << endl;
myObject2.printCount();
cout << endl;
myObject2.printX();
cout << endl;
myObject1.setX(14);
myObject1.incrementCount();
myObject1.printX();
cout << endl;
myObject1.printCount();
cout << endl;
myObject2.printCount();
cout << endl;
```
```

+   30. In Example 10-9, we designed the *class die*. Using this class declare an array, named *rolls*, of 100 components of type *die*. Write C++ statements to roll each die of the array *rolls*, find and output the highest number rolled and the number of times this number was rolled, and find and output the number that was rolled maximum number of times together with its count. Also write a program to test your statements. (1, 3)

# PROGRAMMING EXERCISES

+   1. Chapter 9 defined the `struct studentType` to implement the basic properties of a student. Define the `class studentType` with the same components as the `struct studentType`, and add member functions to manipulate the data members. (Note that the data members of the `class studentType` must be private.) Write a program to illustrate how to use the `class studentType`.

+   2. Write a program that uses the `class productType` defined in Exercises 8 and 10 of this chapter.

+   3. Write a program that uses the `class houseType` defined in Exercises 11 and 12 of this chapter.

+   4. Define a `class counterType` to implement a counter. Your class must have a private data member `counter` of type `int` and functions to set `counter` to the value specified by the user, initialize `counter` to 0, retrieve the value of `counter`, and increment and decrement `counter` by one. The value of `counter` must be nonnegative.