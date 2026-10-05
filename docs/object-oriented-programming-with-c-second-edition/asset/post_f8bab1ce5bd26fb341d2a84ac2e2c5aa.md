
```cpp
void hmeanexcp(char * s)
{
    strcpy(cError, s);
}
char * getError()
{
    return cError;
};
```

```cpp
void main()
{
    double x, y, z;
    x = 10;
    y = -10;
    try {
        z = test_hmean(x, y);
    } catch(hmeanexp&e) {
        cout << "Inside the catch block of main()\n";
    }
}
```

```cpp
double test_hmean(double p, double q)
{
    double r;
    try {
        r = hmean(p, q);
    } catch(hmeanexp&e) {
        cout << "Inside the catch block of test_hmean()\n";
    }
    return r;
}
```

```cpp
double hmean(double a, double b)
{
    if(a==b)
        throw hmeanexcp("Exception error - a=b not allowed");
    return 2.0*a*b/(a+b);
}
/*End of Rethrow.cpp*/
```

# Output

Inside the catch block of test_hmean

As can be seen, the catch handler of the main() function did not execute. This happened because the catch handler of the test_hmean() function did not re-throw the exception. We now understand that exceptions can be re-thrown. We have seen the reasons for throwing exceptions. We have also studied the method for re-throwing exceptions.

# Object-Oriented Programming with C++

# 11.4 Limitation of Exception Handling

The limitation of exception handling is that if a resource has acquired (file has been opened, memory has been allocated dynamically in the heap area, etc.) and the statements to release the resource are after the throw statements, then the acquired resource may remain locked up. Listing 11.15 illustrates this.

Listing 11.15 Dynamically resources remain locked after the throw statement

```cpp
#include<iostream>
class A {
    public:
    A()
    {
        cout<<"Constructor\n";
    }
    ~A()
    {
        cout<<"Destructor\n";
    }
};
void abc(int);
void main() {
    try {
        abc(-1);
    }
    catch(char * s)
    {
        cout<<s<<endl;
    }
    return 0;
}

void abc(int p) {
    A * Aptr = new A[2];
    if(p<0)
        throw "Invalid argument to abc()";
}
```

Output
Constructor
Constructor
Invalid argument to abc()

In Listing 11.15, the stack is unwound, memory occupied by the pointer Aptr in abc() function gets destroyed. However, the memory block at which the pointer points remains locked up. (This is evident from the fact that the destructor was not called for the objects created in the heap.)

# Exception Handling

In order to overcome this problem, classes whose objects function like pointers should be devised. Obviously, such objects will have pointers embedded in memory. Memory will be allocated dynamically for these pointers during the lifetime of the objects. This memory will be deallocated through the destructor. Thus, when the object is destroyed, the memory locked up and referenced by the embedded pointer will be destroyed.

# Summary

Statements to detect conditions that prohibit further execution of the library function and should be placed within the library function itself. Statements to take appropriate action when such conditions are detected and should be placed in the functions that call these library functions.

Append the try block with a series of catch blocks, one for each of the exceptions expected to be thrown.

Since the number of fundamental data types is limited, it is better to throw objects of exception classes created specifically for the purpose. These objects can be initialized with appropriate information before being thrown by the library functions. This information can be accessed within the corresponding catch block of the application program.

Exception handling enables the library function to notify the detected invalid conditions to the user using the throw statement. The program terminates prematurely if the application ignores such notifications. Application program can catch notifications in a try block and take appropriate action in a catch block.

Uncaught exceptions can be caught by the catch(...). Exceptions can be re-thrown. During unwinding of the stack, memory acquired by the objects themselves is destroyed. However, the memory acquired dynamically by the pointers embedded in these objects remains locked up. This is a limitation of exception handling.

Library functions announce the list of all possible exceptions that they throw by enrolling them in their headers. Appropriately, the application program should call these functions in a try block and

# Key Terms

- exception handling
- C-style solutions for exception handling
- try
- catch
- throw
- catching uncaught exceptions
- exception classes
- unwinding of the stack

# Exercises

- 1. What is exception handling? The need is for exception handling?
- 2. What is the negative impact if the library programmer simply terminates an application upon detecting an error condition?
- 3. Which three keywords are provided by C++ for implementing exception handling?
- 4. What happens if the application does not catch the exception thrown by a library function?
- 5. Explain how the stack is unwound when an exception is thrown.
- 6. What is the need to catch objects instead of values of fundamental types?
- 7. Why are nested exception classes needed?
- 8. How are uncaught exceptions caught?
- 9. What is the limitation of exception handling in C++?

- 10. Derive a class from another. Create two catch blocks—the first one for catching the base class-type exception and the second for catching the derived class-type exception. Throw an exception of the base class type from the try block. Observe the result. Now, throw an exception of the derived class-type from the try block. Observe and compare the results. Repeat the above two observations by reversing the sequence of the catch blocks. What do you conclude?
- 11. Add a function to the class String that will return the character from the position that is passed as a parameter to it. If the position is out of bounds, the function should throw a user-defined exception.
- 12. Explain the concept and method of re-throwing exceptions with the help of an example.

# Appendix A

# Case Study—A Word Query System

# Problem Statement

The word query system should allow us to determine whether a particular word exists in a given text file or not.

If the program finds the word being searched, it would display all the lines in which the word was found. The program would also display the number of occurrences of the word, the serial number of the line in the file, and the position of the word in the line.

# A Sample Run

The file having the following lines can be taken as input:

> Chess is the most intellectual sport known to mankind.
> A game of chess is a war of intelligence and a clash of wills.
> It is a game of kings, queens, rooks, bishops and pawns.
> What appears to be a two-dimensional black and white board of 64 squares is, for the chess master, a multicolored wonderland of cunning strategy and brilliant tactics.
> Chess has a rich and long history. Invented in India as a war game, it has followers over the whole world. A regular practice leads to better concentration and improved ability to deduce facts from logic.

The sample run of the program is as follows (we implement case sensitive search):

Please enter the word to be searched (enter to quit): **chess**
Number of occurrences of 'chess' = 2

Please enter the word to be searched (enter to quit): **master**
Number of occurrences of 'master' = 2

Please enter the word to be searched (enter to quit): **mind**
Number of occurrences of 'mind' = 1

Please enter the word to be searched (enter to quit): **golf**
Number of occurrences of 'golf' = 0

Please enter the word to be searched (enter to quit): <enter>
Bye!

# The Source Code

The program listing to implement the word query system as described in the Problem Statement follows:
(Please note that the code calls a few of the member functions of the library string class. These simple calls have been explained in the accompanying comments.)

```cpp
/*Beginning of textQuerySearch.cpp*/
#include<string>
#include<vector>
#include<fstream>
#include<map>

using namespace std;
void main() {
    ifstream infile("abc.txt");
    int flag=0;
    char cVar;
    string word,line;
    int lineNum=1;
    int iwordNum=1;
    typedef pair<int,int> location;
    location loc;
    typedef vector<location> lvec;
    lvec temp;
    vector<location>::iterator iter;
    map<string,lvec> wordmap;
    map<string,lvec>::iterator iter;

    map<int,string> linemap;
    while(infile) {
        infile.get(cVar);
        if(cVar==' ' || cVar=='.' || cVar==',' ||
        cVar==';' || cVar=='\n') {
            if(flag==0) {
                loc.first=lineNum;
                loc.second=iwordNum;
                iwordNum++;
                iter=wordmap.find(word);
```
