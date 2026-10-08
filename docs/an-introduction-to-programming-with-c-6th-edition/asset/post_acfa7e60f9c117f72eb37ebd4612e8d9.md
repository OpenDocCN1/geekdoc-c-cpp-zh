
# APPENDIX F Classes and Objects

section.) The Salesperson employee; statement in Line 26 uses the Salesperson class definition to instantiate a Salesperson object employee. The employee object contains three data members: a string variable name and two double named sales and bonus. As the program in Figure-4 shows you use employee., to refer to the name in the employee object. You use employee.sales and bonus employee. to refer to the employee object's sales and bonus variables. Figure-5 shows a sample run of the Sweets Unlimited program, and Figure F-6 shows the contents of the salesinfo.txt file created by the program.

![](img/d64a28a68f49d61137bf2f3170ac40ad_724_0.png)

Figure-5 Sample run of the Sweets Unlimited program

![](img/d64a28a68f49d61137bf2f3170ac40ad_724_1.png)

Figure-6 Contents of the salesinfo.txt file displayed in a text editor

# Header Files

Although you can enter a class definition in the program you can enter a class definition in a separate file called a header file. As shown earlier in Figure-4, most programmers use a header file. Figure-7 shows the definition of the Salesperson class header entered in a .cpp file. Unlike program files, which end with .cpp, header filenames end with .h. You will learn how to add a header file to a solution in F-2, which is contained in the Cpp6_Appendix.pdf file. Figure-8 shows a modified version of the Sweets Unlimited program. Unlike the original program, the modified program does not contain the Salesperson class definition. Instead, the modified program uses the class definition contained in the Salesperson.h header file. Typically, a header file is stored in the same location as the program that employs the class.

# Example 1—A Class that Contains Public Data Members Only

In this case, for example, the Salesperson.h file would be stored in the same location as the Modified Sweets Unlimited.cpp file. The programmer uses a #include directive to include the contents of the header file in the program. In the modified Sweets Unlimited, the #include "Salesperson.h" directive (which is stated in Figure-8) tells the compiler to merge the contents of the Salesperson.h file with the contents of the current program. In other words, it calls the compiler to include the Salesperson class definition in the current program. Notice that the header filename is enclosed in quotation marks. The quotation indicates that the header file is located in the same folder as the program file.

The angle bracket-(<>) in the other directives in Figure-8 indicates that those are defined in the folder that contains the C++ Standard header files.

```cpp
// Salesperson.h
//Created/revised by <name> on <current date>

#include <string>
using namespace std;

//declaration section
class Salesperson
{
public:
    string name;
    double sales;
    double bonus;
};
```

Figure-F-7 Salesperson class definition entered in the Salesperson.h header file

```cpp
// Modified Sweets Unlimited.cpp
//Saves to a sequential access file
//Created/revised by <name> on <current date>

#include <iostream>
#include <fstream>
#include "Salesperson.h"
using namespace std;

int main()
{
    //declare constant and file object
    const double BONUS_RATE = .05;
    ofstream outputFile;

    //create Salesperson object
    Salesperson employee;
}
```

Figure-F-8 Partial C++ code for the modified Sweets Unlimited program

Although you can define a class that contains only public variables, like the Salesperson class shown in Figure-7, it is rarely done. The disadvantage of using public variables in a class is that a class cannot control the values assigned to its public variables. Therefore, it cannot validate the values to ensure that they are appropriate for the variables. Besides, most classes contain only variables, but methods as well. This is because the purpose of a class in OOP is to encapsulate the attributes (variables) that describe an object and the behaviors (methods) that allow the object to perform tasks. The class used in the next example will show you how to include data validation and methods in a class.

# Example 2—A Class that Contains a Private Member and Public Member Methods

In this example, you will view the code for a class named Square. Square has one attribute: the length of one of its sides. It has four behaviors: it can initialize its size measurement when it is created; it can assign a value to its size measurement after it has been measured; it can provide its size measurement value; and it can calculate its area. Figure F-9 shows the Square class defined in the Square.h header file. The Square class contains one private member: int variable named side. When a variable is declared below the private keyword in a class statement, it can be used only by the code entered in the class definition. In this case, the code uses the side variable to store the side measurement of the Square object. The Square class also contains four public member methods named Square, setSide, getSize, and calculateArea. The prototypes for these methods appear below the public keyword in the implementation section. The definitions of the methods appear in the class definition.

```cpp
//Square.h
//Created/revised by <your name> on <current date>

//declaration section
class Square
{
public:
    Square();
    void setSide(int);
    int getSize();
    int calculateArea();
private:
    int side;
};

//implementation section
Square::Square()
{
    side = 0;
} // end of default constructor
```

Figure F-9 Square class definition entered in the Square.h header file (continues)

# Example 2—A Class that Contains a Private Data Member and Public Methods

(continued)

```cpp
void Square::setSide(int side)
{
    if(side > 0)
        side = side;
    else
        side = 0;
    //end if
} // end of setSide method

int Square::getSide()
{
    return side;
} // end of getSide method

int Square::calculateArea()
{
    return side * side;
} // end of calculateArea method
```

Figure F-9 Square class definition in the Square.h header file

In the Square class definition the first method prototype and the first method definition pertain to the default constructor. A constructor is a method that automatically executes time an object is instantiated from the class. The sole purpose of a constructor is to initialize the private variables. Every class has at least one constructor. Each of a class's constructors must have the same name as the class, but its formal parameters (if any) must be different from any other constructor in the class. A constructor with no parameters is called the default constructor. A class can have only one constructor. Because a constructor does not return a value, its prototype and definition do not begin with a data type. Notice that its definition begins with the name of the class followed by the scope resolution operator (::), the name of the constructor, and a set of parentheses—in case, Square::Square(). The scope operator indicates that the Square is a method of (or in) Square class.

As learned earlier, a programmer does not have direct access to a private variable in a class. Rather, it must access the private variable indirectly through a public method. A program that instantiates a Square object can use the setSide method to assign a value to the private side variable. In this case, the setSide method receives the value from the program that invokes it and stores the value in its formal parameter: an int named side. The code contained in the method definition verifies that the value received from the program is greater than zero. If it is, the code assigns the value to the private side variable; otherwise, it assigns the number to 0. Notice that the setSide method's prototype and definition begin with the keyword void, which indicates that the method does not return a value. A program that instantiates a Square object can use the getSide method, on the other hand, to retrieve the
