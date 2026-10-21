
add(Int1);

In the first case, when we have no argument passed to the function, it is actually called with arguments 100 and 200, respectively, as they are defined as default arguments in the function header. Thus, the number 300 is the output. In the second case, we have provided only one argument. This is considered as the first argument (obviously) and the second argument, which is not explicitly provided by the caller, is taken from default; thus, 5 is added to 200 and we get 205 as the output. Interestingly, if the user’s intention is to provide only the second argument and take the first argument as default and if the function is called as follows, it will not give the expected answer.

add(Int2);

The output is 207, which means that Int2 is considered as the first argument and the second argument was taken by default.

How will the C++ compiler know that Int2 is expected to be the second argument? Is it because it contains 2 in it? What if the arguments are Balance and Interest, which is more likely in a real-world program? There is no way for providing this information to the compiler. So, the first argument is assumed to be the default.

Program 3.9 of Chapter 3 has been modified in Program 4.3. The function CheckPass() is now added to the program. The function is simple enough to understand. It has only one line in the body and returns a bool value, true for passing and false for failing. The value returned depends on the student’s marks and the value of the passing marks.

The function PrintDetails() is also changed such that it now also displays whether the student has passed or not, after calling the CheckPass() function. PrintDetails() is called with more than one type of passing marks value to show how a function with default arguments can be called.

## PROGRAM 4.3 Default arguments

```
// DefaultArgument.cpp
#include <iostream>
#include <string>
using namespace std;

bool CheckPass(int TotalMarks, int PassingMarks = 50);
// Default value is specified here for an argument

class student
{
public:
    int RollNumber;
    string Name;
    string Address;
    int TotalMarks;

    void SetDetails(int Roll, string StudentName, string StudentAddress, int StudentMarks)
    {
        RollNumber = Roll;
        Name = StudentName;
        Address = StudentAddress;
        TotalMarks = StudentMarks;
    }

    void PrintDetails()
{
    cout << "Roll number is " << RollNumber << "\n";
    cout << "Name is " << Name << "\n";
    cout << "Address is " << Address << "\n";

    if(CheckPass(TotalMarks))
        // It takes passing marks as 50 here
        cout << "Congratulations! You have passed (passing marks 50)\n";
    if(CheckPass(TotalMarks,40))
        cout << "Congratulations! You have passed (passing marks 40)\n";
    if(CheckPass(TotalMarks, 35))
        cout << "Congratulations! You have passed (passing marks 35)\n";
    else
        cout << "Sorry! Better luck next time\n";
}
};
bool CheckPass(int TotalMarks, int PassingMarks)
/* Notice the default value for an argument is not repeated here,
it is an error if it is done that way */
{
    return(TotalMarks > PassingMarks);
}
void main()
{
    student ArrayOfStudents[3];
    ArrayOfStudents[0].SetDetails(1, "Umesh Yadav", "New Delhi", 75);
    ArrayOfStudents[0].PrintDetails();
    ArrayOfStudents[1].SetDetails(2, "Varon Aaron", "Jharkhand", 87);
    ArrayOfStudents[1].PrintDetails();
    ArrayOfStudents[2].SetDetails(3, "Vinay Kumar", "Tamil Nadu", 37);
    ArrayOfStudents[2].PrintDetails();
}
```

## How the Program Works

Look at the prototype of the CheckPass() function.

```
bool CheckPass(int TotalMarks, int PassingMarks = 50);
```

Here, PassingMarks is a default argument with the default value set as 50. This means that if the function CheckPass() is called with only one argument, the second argument’s default value should be taken as 50. The function can be called using CheckPass(72) or CheckPass(30) where the passing marks will be considered to be 50, that is, the second argument is assumed to be 50 by default. Thus, the call to CheckPass(72) is equivalent to calling CheckPass(72, 50). It should be noted that the function can also be called using CheckPass(40, 35) where the passing marks are explicitly specified as 35.

In this example, the default arguments are specified in the prototype. If the function is defined before it is used, the prototype can be omitted. In such cases, the function itself will have the default argument specified. If the default arguments are already specified in the prototype, it cannot be redefined in the function header. So, if the function CheckPass() is defined before its call, it will have the following header:

```
bool CheckPass(int TotalMarks, int PassingMarks = 50)
```

instead of

```
bool CheckPass(int TotalMarks, int PassingMarks)
```

and there will be no prototype then.

It is possible to have more than one default argument with more than one normal argument. The rule to pass those arguments is very simple. All the normal arguments must be passed before the default arguments in the argument list.

The CheckPass() function prototype can be rewritten as follows (assuming the code is changed to accommodate usage of other parameters):

```
CheckPass(int Sub1Marks, int Sub2Marks, int PassingMarks = 50)
```

```
CheckPass(int Sub1Marks, int Sub2Marks, int PassingMarks1 = 50,
int PassingMarks2 = 35);
```

```
CheckPass(int Sub1Marks, int PassingMarks1 = 50, int Sub2Marks,
int PassingMarks2 = 35);
```

```
/* This statement is wrong because PassingMarks1 is a default argument written before Sub2Marks, which is not a default argument. */
```

## 4.5.1 Using Static Variable as Default Argument to a Function

Functions with default arguments are very handy if, for most of the cases, the value of the argument remains the same. An interesting thing to note here is that a static variable can also be used as a default argument value. So it is possible to write

```
Account(AccountNumber = NextNumber)
```

where NextNumber is a static variable and is incremented every time a new Account object is created. This is an example which shows how an important functionality can be added to a program. As soon as a new account is created, it will get a unique account number automatically. This can be illustrated with a simple example shown in the following program. The getNext() function automatically receives the next immediate number. It can be observed that the static integer value Next is incremented and returned from the function.

This simple solution is possible only in cases where the next number series starts from zero and will not work if the getNext() series is supposed to start from some other number. Such a program will need some changes.

```
#include <iostream>
using namespace std;
static int Next;
int getNext(int NextNumber = Next)
{
    Next++;
    return NextNumber;
}
int main()
{
cout << getNext() << endl;
cout << getNext() << endl;
cout << getNext() << endl;
getchar();
```

Output

0

1

2

Readers are encouraged to reason out the following questions:

- 1. Why should all normal arguments precede all default arguments?
- 2. How can the compiler determine which argument corresponds to which one?
- 3. How can a compiler know for sure that a particular default argument is passed explicitly?

## 4.5.2 Functions with Objects as Parameters

Functions in C++ can have any valid data type as an argument or a return type similar to a C function. As an obvious consequence of the availability of objects in C++, functions in C++ can pass as well as return objects. Consider the following program.

### Passing an object

The function can be passed objects similar to other variables. The following program uses a non-member function PrintValues(), which takes a complex object as an argument and prints it.

```
// ReturnComplexObject.cpp
#include <iostream>
using namespace std;
class Complex
{
public:
double real;
double imag;
void SetValues(int TempReal, int TempImag)
{
real = TempReal;
imag = TempImag;
}
};
void PrintValues(Complex ComplexNumber)
{
cout << "(" << ComplexNumber.real << "," << ComplexNumber.imag << ")";
}
int main()
{
```
