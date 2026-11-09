given in the pointer variable.
The whole of this operation is performed by using the Unary operator *. The following are the pointers that are most frequently used in C++ programming:

+   - Null pointers
+   - Array of pointers
+   - Pointer to pointer
+   - Passing pointers to Functions
+   - Return pointer to Functions

# Object Oriented C++

# Classes and Objects

Object Oriented Programming in C++ language is a simple way to create objects and perform multiple operations. At first, we are required to define a class before creating an object for which the below mentioned syntax could be used:

```
```cpp
class className
{
        //data
};
```
```

A class can be defined as Public, Private, or Protected so that the data members could only be accessed specifically within the program.

Sample code:

```
```cpp
class student
{

        private:

                char name[20];

                int  rollNo;

                int  total;

                float perc;

        public:

                //member function to get student's details

                void getDetails(void);

                //member function to print student's details

                void putDetails(void);
```
```