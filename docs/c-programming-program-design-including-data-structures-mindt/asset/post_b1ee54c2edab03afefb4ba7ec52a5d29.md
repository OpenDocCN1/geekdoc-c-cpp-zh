
- 7. The thrown value then may not be accessible in the `catch` block exception handling code.

- 9. The object being thrown can be either a specific object or an anonymous object.

- 11. The `cout` statement in Line 12 separates the catch block from the try block. Therefore, the catch block has no associated try block and the try block has no associated catch block. The catch block in Line 13 has no parameters. The correct code is:

```cpp
double salary = 78000;                         //Line 1
double raise;                                  //Line 2

try                                            //Line 3
{                                              //Line 4
    cout << "Enter the raise: ";               //Line 5
    cin >> raise;                              //Line 6
    cout << endl;                              //Line 7

    if (raise < 0.0)                           //Line 8
        throw raise;                           //Line 9

    cout << "Salary increase: $"               //Line 10
         << salary * raise / 100 << endl;
    cout << "Exiting the try block." << endl;  //Line 11
}                                              //Line 12
catch (double x)                               //Line 13
{                                              //Line 14
    cout << "Negative raise: " << x << endl;   //Line 15
}                                              //Line 16
```

(In a and b, the user input is shaded.)

- a. **Enter the raise:** `5`

  Salary increase: $3900  
  Exiting the try block.

  **Enter the raise:** `-4`  
  Negative raise: -4

- 13. (In the following, the user input is shaded.)

  - a. **Enter the number of items:** `25`  
    **Enter the cost of one item:** `5.50`  
    Total cost: $137.50

  - b. **Enter the number of items:** `-55`  
    Negative number of items: -55  
    Number of items must be nonnegative.

  - c. **Enter the number of items:** `37`  
    **Enter the cost of one item:** `-4.5`  
    Negative unit cost: -4.50  
    Unit cost must be nonnegative.

  - d. Enter the number of items: `-10`  
    Negative number of items: -10  
    Number of items must be nonnegative.

- 15.
  - a. 55
  - b. Exiting the try block.
  - c. Exception: Division by 0
  - d. Exception: Total score is out of range.

- 17.
  - a. `class out_of_range`
  - b. `class length_error`
  - c. `class runtime_error`

19. A throw statement.

21. (Assume that the definition of the class `tornadoException` is in the header file `tornadoException.h`.)

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

23. A function specifies the exceptions it throws in its heading using the `throw` clause.

25. (1) Do nothing; (2) Partially process the exception and throw the same exception or a new exception; (3) Throw a new exception.

## Chapter 15

- 1. a. true; b. true; c. false; d. false; e. false; f. false; g. true; h. true

- 3. A definition in which something is defined in terms of a smaller version of itself.

- 5. Because a base case stops the recursion.

- 7.
  - a. The statements from Line 3 to Line 6.
  - b. The statements in Lines 7 and 8.
  - c. It is a valid call. The value of `recFunc(58)` is 32.
  - d. It is a valid call. The value of `recFunc(-24)` is 24.
  - e. It is a valid call. The value of `recFunc(0)` is 0.

- 9.
  - a. `8 5 2`
  - b. `7`
  - c. `6 3`
  - d. `-85`

- 11.
  - a. `4 12 28`
  - b. `5 15 34 72 148`
  - c. `2 8 21 47 98`
  - d. It does not produce any output.

- 13.
  - a. `0`
  - b. `4`
  - c. `8`
  - d. `162`

- 15.
  - a. `10`
  - b. `21`
  - c. `-23`
  - d. `2`
  - e. `-56`

- 17.

  $$
  \operatorname{multiply}(m,n)=
  \begin{cases}
  0 & \text{if } n=0\\
  m & \text{if } n=1\\
  m+\operatorname{multiply}(m,n-1) & \text{otherwise}
  \end{cases}
  $$

  The base cases are when $n=0$ or $n=1$. The general case is specified by the option otherwise.

- 19. A selection control structure.

## Chapter 16

- 1. a. true; b. false; c. false; d. false; e. false; f. true; g. true; h. false; i. false; j. true; k. true; l. false; m. false; n. true

- 3. `nullptr`

- 5. Before deletion, the link field of the third node stores the address of the fourth node. After deletion, the link field of the third node will store the address of the next node, the old fifth node. If there was no fifth node, after deletion the link field will store the value `nullptr`. Therefore, after deleting the fourth node, the link field of the third node is changed. So a pointer to the third node is needed.

- 7. a. true; b. true; c. false; d. true; e. true; f. false

9.

```cpp
a.  p->link->info = 24;
b.  q = current->link;
c.  first = first->link;
d.  trail = p->link;
e.  p = nullptr;
f.  temp->link->info = 54;
g.  while (first->info != 5)
        first = first->link;
```

11.

```cpp
a.  while (first != nullptr)
        first = first->link;

b.  q = new nodeType;
    q->info = 17;
    q->link = current->link;
    current->link = q;

c.  q = temp->link;
    q->link = nullptr;
    delete last;
    last = q;

d.  q = p->link;
    p->link = current;
    delete q;

e.  q = current->link;
    q->link = temp->link;
    temp->link = q;
    current->link = temp;
```

- 13. `65  5  78`

- 15. `39  26  78`

- 17. `nodeType head, p, q;`

```cpp
head = new nodeType;
head->info = 72;
head->link = nullptr;
p = new nodeType;
p->info = 43;
p->link = head;
head = p;
p = head->link;
q = new nodeType;
q->info = 8;
q->link = nullptr;
p->link = q;
q = new nodeType;
q->info = 12;
q->link = p;
head->link = q;

p = head;
while (p != nullptr)
{
    cout << p->info << " ";
    p = p->link;
}
cout << endl;
```

The output of this code is: **43 12 72 8**

- 19.
  - a. The function begin returns an iterator to the first node of a linked list.
  - b. The function end returns an iterator one past the last node of a linked list.

- 21. **The item to be deleted is not in the list.**

  `90 15 65 36 30 27`

- 23. The answer to this question is available at the website accompanying this book.

- 25. The answer to this question is available at the website accompanying this book.

## Chapter 17

- 1. a. true; b. false; c. false; d. true; e. false; f. true; g. false; h. false; i. true; j. true; k. true; l. false; m. false; n. false

- 3.
  - a. 8
  - b. 7
  - c. `dec = stack.top();`
  - d. `stack.pop();`

- 5. 13

  `32 32 13 16 28`

  `temp = 16`

- 7. `secretNum = 226`

- 9.
  - a. 16
  - b. -4
  - c. 39
  - d. 12
  - e. 15

- 11.
  - a. `x * y + z - t`
  - b. `x * (y + z) - w / u`
  - c. `(x - y) * (z / u) - (t + s)`
  - d. `x * (y - (z + w))`

- 13. `1 16 27 16 5`

15. If the stack is nonempty, the statement `stack.top();` returns the top element of the stack and the statement `stack.pop();` removes the top element of the stack.

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
