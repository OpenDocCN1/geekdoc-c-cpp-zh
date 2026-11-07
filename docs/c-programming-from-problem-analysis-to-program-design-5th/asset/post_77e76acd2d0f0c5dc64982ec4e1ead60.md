
- 21. One.

- 23. Answer to this question is available at the Web site accompanying this book.

- 25. Error in Line 4. A template instantiation can be for only a built-in type or a user-defined type. The word “type” between the angular brackets must be replaced either with a built-in type or a user-defined type.

- 27. a. 12 b. Sunny Day

- 29.

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

## Chapter 16

- 1. a. false; b. true; c. true; d. false

- 3. The program will terminate with an error message.

- 5. If an exception is thrown in a try block, the remaining statements in that try block are ignored. The program searches the catch blocks in the order that they appear after the try block and looks for an appropriate exception handler. If the type of thrown exception matches the parameter type in one of the catch blocks, the code of that catch block executes, and the remaining catch blocks after this catch block are ignored.

- 7.
  - a. Leaving the try block.
  - b. Current balance: 975
    Balance must be greater than 1000.00
  - c. Current balance: −2000
    Balance must be greater than 1000.00

- 9.
  - a. Entering the try block.
    Exception: Lower limit violation.
    After the catch block
  - b. Entering the try block.
    Exception: 0
    After the catch block
  - c. Entering the try block.
    Exiting the try block.
    After the catch block
  - d. Entering the try block.
    Exception: 0
    After the catch block

- 11. A throw statement.

- 13. (Assume that the definition of the class `tornadoException` is in the header file `tornadoException.h`.)

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

- 15. A function specifies the exceptions it throws in its heading using the `throw` clause.

## Chapter 17

- 1. a. true; b. true; c. false; d. false; e. false

- 3. The case in which the solution is defined in terms of smaller versions of itself.

- 5. A function that calls another function and eventually results in the original function call is said to be indirectly recursive.

- 7.
  - a. The statements in Lines 2 and 3.
  - b. The statements in Lines 4 and 5.
  - c. Any nonnegative integer.
  - d. It is a valid call. The value of `mystery(0)` is 0.
  - e. It is a valid call. The value of `mystery(5)` is 15.
  - f. It is an invalid call. It will result in infinite recursion.

- 9.
  - a. 2
    5
    8
  - b. 7
  - c. 3
    6
  - d. −85

- 11.
  - a. It does not produce any output.
  - b. 5 6 7 8 9
  - c. It does not produce any output.
  - d. It does not produce any output.

- 13. a. 2; b. 3; c. 5; d. 21

- 15.

$$\operatorname{multiply}(m,n)=\begin{cases}0 & \text{if } n=0\\m & \text{if } n=1\\m+\operatorname{multiply}(m,n-1) & \text{otherwise}\end{cases}$$

The base cases are when $n = 0$ or $n = 1$. The general case is specified by the option otherwise.

## Chapter 18

- 1. a. false; b. false; c. false; d. false

- 3. NULL

- 5. Before deletion, the link field of the third node stores the address of the fourth node. After deletion, the link field of the third node will store the address of the next node, which is the old fifth node. If there was no fifth node, then after deletion, the link field will store the value NULL. Therefore, after deleting the fourth node, the link field of the third node is changed. So a pointer to the third node is needed.

- 7. a. true; b. true; c. false; d. false; e. true

- 9.
  - a. `A = A->link;`
  - b. `list = A->link->link;`
  - c. `B = B->link->link;`
  - d. `list = NULL;`
  - e. `B->link->info = 35;`
  - f.
    ```cpp
    newNode = new nodeType;
    newNode->info = 10;
    newNode->link = A->link;
    A->link = newNode;
    ```
  - g.
    ```cpp
    p = A->link;
    A->link = p->link;
    delete p;
    ```

- 11. This is an invalid code. The statement `s->info = B;` is invalid because B is a pointer and s->info is an int.

- 13. 10 18 13

- 15. `nodeType head, p, q;`

```cpp
head = new nodeType;
head->info = 72;
head->link = NULL;
p = new nodeType;
p->info = 43;
p->link = head;
head = p;
p = head->link;
q = new nodeType;
q->info = 8;
q->link = NULL;
p->link = q;
q = new nodeType;
q->info = 12;
q->link = p;
head->link = q;

p = head;
while (p != NULL)
{
    cout << p->info << " ";
    p = p->link;
}
cout << endl;
```

The output of this code is: 43 12 72 8

- 17. Item to be deleted is not in the list.
  18 38 2 15 45 25

- 19. Answer to this question is available at the Web site accompanying this book.

- 21. Answer to this question is available at the Web site accompanying this book.

## Chapter 19

- 1. The two basic operations on a stack are push, to add an element to a stack, and pop, to remove an element from a stack.

- 3. x = 3
  y = 9
  13
  4
  7

- 5. a. 26; b. 45; c. 8; d. 29

- 7. a. A * B + C
  b. (A + B) * (C - D)
  c. (A - B - C) * D

- 9. 10 20 30 40 50

- 11. If the stack is nonempty, the statement `stack.top();` returns the top element of the stack, and the statement `stack.pop();` removes the top element of the stack.

- 13.

```cpp
template <class elemType>
elemType second(stackType<elemType> stack)
{
    elemType temp1, temp2;

    if (stack.isEmptyStack())
    {
        cout << "Stack is empty." << endl;
        exit(0); //terminate the program
    }

    temp1 = stack.top();
    stack.pop();

    if (stack.isEmptyStack())
    {
        cout << "Stack has only one element." << endl;
        exit(0); //terminate the program
    }

    temp2 = stack.top();
    stack.push(temp1);

    return temp2;
}
```

- 15. Queue Element = 0
  Queue Element = 14
  Queue Element = 22
  Sorry, the queue is empty
  Sorry, the queue is empty
  Stack Element = 32
  Stack Elements: 64 28 0
  Queue Elements: 30

- 17.
  - a. queueFront = 50; queueRear = 0.
  - b. queueFront = 51; queueRear = 99.

- 19.
  - a. queueFront = 25; queueRear = 76.
  - b. queueFront = 26; queueRear = 75.

- 21. 51

- 23.

```cpp
template <class Type>
void reverseStack(stackType<Type> &s)
{
    linkedQueueType<Type> q;
    Type elem;

    while (!s.isEmptyStack())
    {
        elem = s.top();
        s.pop();
        q.addQueue(elem);
    }

    while (!q.isEmptyQueue())
    {
        elem = q.front();
        q.deleteQueue();
        s.push(elem);
    }
}
```

- 25.

```cpp
template <class Type>
int queueType<Type>::queueCount()
{
    return count;
}
```

- 27. Answer to this question is available at the Web site accompanying this book.

- 29. Answer to this question is available at the Web site accompanying this book.

*This page intentionally left blank*

Note: Page numbers in boldface indicate key terms.

## A

- & (ampersand), 369, 812
- * (asterisk), 794, 796, 812
- \\ (backslash), 69, 73
- , (comma), 85
- {} (curly braces), 78, 85, 212
- " (double quotes), 458, 510, 513
- = (equal sign), 1153
- / (forward slash), 32
- − (minus sign), 654
- () (parentheses), 187, 327, 801
- . (period), 129, 655
- + (plus sign), 654
- # (pound sign), 145, 257, 880, 1154
- ; (semicolon), 85, 651, 836
- [] (square brackets), 495
- ~ (tilde), 677
- _ (underscore), 33, 34, 86, 453

- abs function, 321, 325
- abstract classes
  - described, **836**
  - overview, 835–843
- abstract data types. *See* ADTs (abstract data types)
- abstraction, 678. *See also* abstract classes
- accessor functions, **664**, 665–669
- action statements, 189
- actual parameter lists, 327, 363
- addFirst function, 381
- addQueue function, 1166, 1168–1170, 1175, 1179–1182, 1197
- address of operator, **795–796**, 844–846
- addressOfX function, 845, 846
- ADTs (abstract data types)
  - described, **678**
  - linked lists and, 1037–1050, 1058–1059, 1072–1074
  - OOP and, relationship of, 757
  - overview, 678–680
  - queues and, 1165, 1167, 1185, 1188, 1192, 1196
  - structs and, 681
  - templates and, 927
- aggregate operations, **497**
- aggregation. *See* composition
- Aiken, Howard, 3
- algebra, 320
- algorithm(s)
  - arrays and, 507–510
  - control structures and, 287–288
  - described, **12**
  - generic, **1290**
  - linked lists and, 1059–1060, 1070, 1077
  - modifying, **1291**
  - mutating, **1291**
  - non-modifying, **1290**
  - numeric, 1292
  - problem analysis-coding-execution cycle and, 12–20
  - stacks and, 1154–1156, 1161–1165
  - STL and, 1289–1292
