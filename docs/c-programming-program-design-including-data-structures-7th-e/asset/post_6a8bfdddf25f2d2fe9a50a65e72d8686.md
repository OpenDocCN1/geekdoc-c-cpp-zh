
- 31. The copy constructor makes a copy of the actual variable.
- 33. Classes with pointer data members should include the destructor, overload the assignment operator, and explicitly provide the copy constructor by including it in the class definition and providing its definition.
- 35.
    ```text
    ClassA x: 4

    ClassA x: 6
    ClassB y: 10
    ```
- 37. Yes.
- 39.
    - a. Because employeeType is an abstract class, you cannot instantiate an object of this class. Therefore, this statement is illegal.
    - b. This statement is legal.
    - c. This statement is legal.

## Chapter 13
- 1. a. true; b. false; c. true; d. false; e. false; f. false; g. false; h. false; i. true; j. false; k. false; l. true; m. true
- 3. `.`, `.*`, `::`, `?:`, and `sizeof`
- 5. The statement `return this;` returns the address of the object while the statement `return *this;` returns the value of the object.
- 7. A friend function is a nonmember of a class, whereas a member function is a member of a class.
- 9. Because the left operand of << is a stream object, which is not of the type mystery.
- 11. `()`, `[]`, `->`, and `=`
- 13.
    ```cpp
    a. friend strange operator+(const strange&, const strange&);
    b. friend bool operator==(const strange&, const strange&);
    c. friend strange operator<<(strange&, int&);
    ```
- 15. In Line 4, the return type of the function `operator*` should be `temp`. The correct statement is:
    ```cpp
    temp operator*(const temp& obj);        //Line 4
    ```
- 17. In Line 3, the return type of the function `operator<` should be `bool`. The correct statement is:
    ```cpp
    friend bool operator<(const mystery& a,
                         const mystery& b);  //Line 3
    ```
- 19. In Lines 3 and 11, the return type of the function `operator+` should be `discover`. Also since `operator+` is a friend function of the class, the name of the class and the scope resolution operator in the heading of the function, in Line 11, are not needed. The correct statements are:
    ```cpp
    friend discover operator+(const discover&,
                             const discover&);        //Line 3
    ```
    ```cpp
    discover operator+(const discover& a,
                       const discover& b)        //Line 11
    ```
- 21. A reference to an object of the class `istream`.
- 23. Suppose that a class, say `temp`, overloads the pre- and postincrement operator `++`, and `tempObj` is an object of the class `temp`. Then, the statement `++tempObj;` is compiled as `tempObj.operator++();`, and the statement `tempObj++;` is compiled as `tempObj.operator++(0);`. The dummy parameter distinguishes between the pre- and post-increment operator functions. Similar conventions for the pre- and post-increment operators.
- 25. None.
- 27. One.
- 29. The answer to this question is available at the Web site accompanying this book.
- 31. When the class has pointer data members.
- 33. Error in Line 4. A template instantiation can be for only a built-in type or a user-defined type. The word “type” between the angular brackets must be replaced either with a built-in type or a user-defined type.
- 35. a. 12 b. Sunny Day
- 37.
    ```cpp
    template <class Type>
    void swap(Type &x, Type &y)
    {
        Type temp;
        temp = x;
        x = y;
        y = temp;
    }
    ```

## Chapter 14
- 1. a. false; b. true; c. true; d. false; e. true; f. false; g. false; h. true; i. false; j. true; k. false; l. true; m. false
- 3. The program will terminate with an error message.
- 5. If an exception is thrown in a try block, the remaining statements in that try block are ignored. The program searches the catch blocks in the order that they appear after the try block and looks for an appropriate exception handler. If the type of thrown exception matches the parameter type in one of the catch blocks, the code of that catch block executes, and the remaining catch blocks after this catch block are ignored.
- 7. At most one.
- 9. `throw expression;`
    where expression is a constant value, variable, or object.
- 11. The `catch` block has no associated `try` block, that is, the `catch` block does not follow any `try` block. Also, the `try` block has no associated `catch` block, that is, there is no `catch` block that follows the `try` block. The `cout` statement just before the `catch` block disassociates the `catch` block from the `try` block. The correct code is:
    ```cpp
    double radius;

    try
    {
        cout << "Enter the radius: ";
        cin >> radius;
        cout << endl;

        if (radius < 0.0)
            throw radius;

        cout << "Area: " << 3.1416 * radius * radius << endl;
    }
    catch (double x)
    {
        cout << "Negative radius: " << x << endl;
    }
    ```
- 13.
    - a. Leaving the `try` block.
    - b. Current balance: 975
         Balance must be greater than 1000.00
    - c. Current balance: -2000
         Balance must be greater than 1000.00
- 15.
    - a. Entering the `try` block.
         Exception: Lower limit violation.
         After the `catch` block
    - b. Entering the `try` block.
         Exception: 0
         After the `catch` block
    - c. Entering the `try` block.
         Exiting the `try` block.
         After the `catch` block
    - d. Entering the `try` block.
         Exception: 0
         After the `catch` block
- 17. invalid argument
- 19. A throw statement.
- 21. (Assume that the definition of the class `tornadoException` is in the header file tornadoException.h.)
    ```cpp
    #include <iostream>
    #include "tornadoException.h"

    using namespace std;

    int main()
    {
        int miles;

        try
        {
            cout << "Enter the miles: ";
            cin >> miles;
            cout << endl;

            if (miles < 5)
                throw tornadoException();
            else
                throw tornadoException(miles);
        }
        catch (tornadoException tE)
        {
            cout << tE.what() << endl;
        }

        return 0;
    }
    ```
- 23. A function specifies the exceptions it throws in its heading using the throw clause.
- 25. (1) Do nothing; (2) Partially process the exception and throw the same exception or a new exception; (3) Throw a new exception.

## Chapter 15
- 1. a. true; b. true; c. false; d. false; e. false; f. false; g. true; h. true
- 3. The case in which the solution is defined in terms of smaller versions of itself.
- 5. A function that calls another function and eventually results in the original function call is said to be indirectly recursive.
- 7.
    - a. The statements in Lines 2 and 3.
    - b. The statements in Lines 4 and 5.
    - c. Any nonpositive integer.
    - d. It is a valid call. The value of mystery(0) is 0.
    - e. It is an invalid call. It will result in infinite recursion.
    - f. It is a valid call. The value of mystery(-3) is 6.
- 9. a. 8 5 2  b. 7  c. 6 3  d. -85
- 11.
    - a. It does not produce any output.
    - b. 5 6 7 8 9
    - c. It does not produce any output.
    - d. It does not produce any output.
- 13. a. 2; b. 3; c. 5; d. 21
- 15. a. 10  b. 21  c. −23  d. 2  e. −56
- 17. $\operatorname{multiply}(m,n)=\begin{cases}0 & \text{if } n=0\\m & \text{if } n=1\\m+\operatorname{multiply}(m,n-1) & \text{otherwise}\end{cases}$

    The base cases are when $n=0$ or $n=1$. The general case is specified by the option otherwise.

## Chapter 16
- 1. a. true; b. false; c. false; d. false; e. false; f. true; g. true; h. false; i. false; j. true; k. true; l. false; m. false; n. true
- 3. `nullptr`
- 5. Before deletion, the link field of the third node stores the address of the fourth node. After deletion, the link field of the third node will store the address of the next node, which is the old fifth node. If there are no fifth node, then after deletion, the link field will store the value `nullptr`. Therefore, after deleting the fourth node, the link field of the third node is changed. So a pointer to the third node is needed.
- 7. a. false; b. true; c. true; d. true; e. true
- 9.
    ```text
    a. current->link->info = 52;
    b. current = temp->link;
    c. trail = current->link;
    d. temp = nullptr;
    e. temp->link->link->link->info = 36;
    f. while (current->info != 10)
           current = current->link;
    ```
- 11.
    ```text
    a. while (current != nullptr)
           current = current->link;

    b. temp = new nodeType;
       temp->info = 68;
       temp->link = last;
       trail->link = temp;

    c. delete last;
       trail->link = nullptr;
       last = trail;

    d. trail = temp->link;
       temp->link = trail->link;
       delete trail;
    ```
