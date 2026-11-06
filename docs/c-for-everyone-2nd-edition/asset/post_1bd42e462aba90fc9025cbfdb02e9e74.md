
![](img/23fb3582e93ebc95909e1de029c3d388_443_0.png)

### SELF CHECK

- 29. What is the rule of thumb for finding classes?
- 30. You are to write a program that plays chess. Might `ChessBoard` be an appropriate class? How about `MovePiece`?
- 31. In an e-mail system, messages are stored in a mailbox. Draw a UML diagram that shows the appropriate aggregation relationship.
- 32. You are implementing a system to manage a library, keeping track of which books are checked out by whom. Should the `Book` class aggregate `Patron` or the other way around?
- 33. In a library management system, what would be the relationship between classes `Patron` and `Author`?

**Practice It** Now you can try these exercises at the end of the chapter: R9.23, R9.24, R9.26.

### Programming Tip 9.3: Make Parallel Vectors into Vectors of Objects

![](img/23fb3582e93ebc95909e1de029c3d388_443_1.png)

Sometimes, you find yourself using vectors of the same length, each of which stores a part of what conceptually should be an object. In that situation, it is a good idea to reorganize your program and use a single vector whose elements are objects.

For example, suppose an invoice contains a series of item descriptions and prices. One solution is to keep two vectors:

```cpp
vector<string> descriptions;
vector<double> prices;
```

Each of the vectors will have the same length, and the *ith slice*, consisting of `descriptions[i]` and `prices[i]`, contains data that needs to be processed together. These vectors are called **parallel vectors** (see Figure 5).

Parallel vectors become a headache in larger programs. The programmer must ensure that the vectors always have the same length and that each slice is filled with values that actually belong together. Moreover, any function that operates on a slice must get all of the vectors as arguments, which is tedious to program.

The remedy is simple. Look at the slice and find the *concept* that it represents. Then make the concept into a class. In this example, each slice contains the description and price of an *item*; turn this into a class.

> Avoid parallel vectors by changing them into vectors of objects.

```cpp
class Item
{
public:

private:
   string description;
   double price;
};
```

![](img/23fb3582e93ebc95909e1de029c3d388_443_2.png)

**Figure 5** Parallel Vectors

![](img/23fb3582e93ebc95909e1de029c3d388_444_0.png)

**Figure 6** Eliminating Parallel Vectors

You can now eliminate the parallel vectors and replace them with a single vector:

```cpp
vector<Item> items;
```

Each slot in the resulting vector corresponds to a slice in the set of parallel vectors (see Figure 6).

## 9.8 Separate Compilation

The code of complex programs is distributed over multiple files.

When you write and compile small programs, you can place all your code into a single source file. When your programs get larger or you work in a team, that situation changes. You will want to split your code into separate source files. There are two reasons why this split becomes necessary. First, it takes time to compile a file, and it seems silly to wait for the compiler to keep translating code that doesn’t change. If your code is distributed over several source files, then only those files that you change need to be recompiled. The second reason becomes apparent when you work with other programmers in a team. It would be very difficult for multiple programmers to edit a single source file simultaneously. Therefore, the program code is broken up so that each programmer is solely responsible for a separate set of files.

If your program is composed of multiple files, some of these files will define data types or functions that are needed in other files. There must be a path of communication between the files. In C++, that communication happens through the inclusion of header files.

A header file contains

- Definitions of classes.
- Definitions of constants.
- Declarations of nonmember functions.

Header files contain the definitions of classes and declarations of nonmember functions.

Note the set of directives that bracket the header file:

```cpp
#ifndef CASHREGISTER_H
#define CASHREGISTER_H

#endif
```

Suppose a file includes two header files: cashregister.h, and another header file that itself includes cashregister.h. The effect of the directives is to skip the file when it is encountered the second time. If we did not have that check, the compiler would complain when it saw the definition for the CashRegister class twice. (Sadly, it doesn't check whether the definitions are identical.)

The source file for the CashRegister class simply contains the definitions of the member functions (including constructors).

Note that the source file cashregister.cpp includes its own header file cashregister.h. The compiler needs to know how the CashRegister class is defined in order to compile the member functions.

**ch09/cashregister.cpp**

```cpp
#include "cashregister.h"

CashRegister::CashRegister()
{
   clear();
}

void CashRegister::clear()
{
   item_count = 0;
   total_price = 0;
}

void CashRegister::add_item(double price)
{
   item_count++;
   total_price = total_price + price;
}

double CashRegister::get_total() const
{
   return total_price;
}

int CashRegister::get_count() const
{
   return item_count;
}
```

Note that the function comments are in the header file, because comments are a part of the interface, not the implementation.

The cashregister.cpp file does not contain a *main* function. There are many potential programs that might make use of the CashRegister class. Each of these programs will need to supply its own *main* function, as well as other functions and classes.

Here is a simple test program that puts the CashRegister class to use. Its source file includes the cashregister.h header file.

**ch09/registertest2.cpp**

```cpp
#include <iostream>
#include <iomanip>
#include "cashregister.h"

using namespace std;

/**
    Displays the item count and total price of a cash register.
    @param reg the cash register to display
*/
void display(CashRegister reg)
{
    cout << reg.get_count() << " $" << fixed << setprecision(2)
         << reg.get_total() << endl;
}

int main()
{
    CashRegister register1;
    register1.clear();
    register1.add_item(1.95);
    display(register1);
    register1.add_item(0.95);
    display(register1);
    register1.add_item(2.50);
    display(register1);
    return 0;
}
```

To build the complete program, you need to compile both the registertest2.cpp and cashregister.cpp source files (see Figure 7). The details depend on your compiler. For example, with the GNU compiler, you issue the command

```bash
g++ -o registertest registertest2.cpp cashregister.cpp
```

![](img/23fb3582e93ebc95909e1de029c3d388_447_0.png)

You have just seen the simplest and most common case for designing header and source files. There are a few additional technical details that you should know.

- A header file should include all headers that are necessary for defining the class. For example, if a class uses the string class, include the `<string>` header as well. Anytime you include a header from the standard library, also include the directive `using namespace std;`

**item.h**

```cpp
#include <string>
using namespace std;

class Item
{
    ...
private:
    string description;
};
```

- Place shared constants into a header file. For example,

**volumes.h**

```cpp
const double CAN_VOLUME = 0.355;
```

- To share a nonmember function, place the function declaration into a header file and the definition of the function into the corresponding source file.

**cube.h**

```cpp
double cube_volume(double side_length);
```

**cube.cpp**

```cpp
#include "cube.h"

double cube_volume(double side_length)
{
    double volume = side_length * side_length * side_length;
    return volume;
}
```

![](img/23fb3582e93ebc95909e1de029c3d388_448_0.png)

### SELF CHECK

- 34. Suppose the cash register is enhanced to carry out direct debits from bank accounts, and a member function declaration `BankAccount()` is added to the CashRegister class. Which header file do you need to include in `cashregister.h`?
- 35. In the enhancement described in Self Check 34, what additional file do you need to include in `cashregister.cpp`?
- 36. In the enhancement described in Self Check 34, what additional file do you need to include in the `bankaccount.h` file?
- 37. Suppose we want to move the display function from `registertest2.cpp` to the `cashregister.h` and `cashregister.cpp` files. Explain how those files need to change.
- 38. Where is the header file located that you include with the `#include <iostream>` directive?

### Practice It

Now you can try these exercises at the end of the chapter: R9.28, R9.29, P9.20.
