
- Observe that the size of the whole structure becomes different, as in a class.
- The code displays the changes made.

## 9.3 Union

Union is another user-defined data type in C++. Union groups various objects and members of different types and bytes together. Structure and union may seem similar because of their syntax, but they vary in their memory allocation to members. A union will give data variables memory space equal to the space occupied by the data variable with the largest size of that respective union.

The syntax for a union is as follows:

```cpp
union UnionName
{
    //members
};
```

### Features

- Defined using the keyword `union`, and members are accessed using the dot operator.
- Memory allocation for a union is determined by the largest member.
- It has data members and functions that are similar to the variables and functions used elsewhere in C++.
- Data members can be initialized and overwritten if the value changes because the same memory space is affected.
- Accessing of members is done using the selector or dot operator.
- A pointer to a union in C++ is used as follows: `->`.

### Code: Working with Union

```cpp
#include <iostream>
using namespace std;

union OurUnion {
    int x;
    char c;
};

int main()
{
    union OurUnion u1;
    u1.x = 85;
    u1.c = 'H';
    cout << "The value is : " << u1.x << endl;
    cout << "The value is : " << u1.c << endl;
    cout << "Size of union  : " << sizeof(u1) << endl;
    return 0;
}
```

### Output:

```text
The value is : 72
The value is : H
Size of union : 4
```

### Code Debriefing

- In this code, we create a union with a few variables.
- Then, the object of our union is made to access the members.
- Observe that the size of the whole union changes, as in a structure.
- The code displays the changes made.

### Code: Implementation of a Union Data Type

```cpp
#include <iostream>
using namespace std;

union OurUnion {
    int x;
    char c;
    char name[12];
};

int main()
{
    union OurUnion u1;
    u1.x = 8588;
    u1.c = 'H';

    union OurUnion u2;
    u2.x = 590;
    u2.c = 'S';

    cout << "The value is x : " << u1.x << endl;
    cout << "The value is c : " << u1.c << endl;
    cout << "Size of union  : " << sizeof(u1) << endl;
    cout << "The value is x : " << u2.x << endl;
    cout << "The value is c : " << u2.c << endl;
    cout << "Size of union  : " << sizeof(u2) << endl;

    return 0;
}
```

### Output:

```text
The value is x : 8250
The value is c : H
Size of union : 12
The value is x : 595
The value is c : S
Size of union : 12
```

### Code Debriefing

- In this code, we create a union with a few variables and assigned values using the dot operator.
- Then, the object of our union is made to access the members.
- Observe that the size of the whole union changes, as in a structure.
- The code displays the changes made.

## 9.4 Differences Between Structure and Union

Now that we have seen these two user-defined data types in C++, let us consider how these two data types differ from one another. The following table will help learners determine when and where structure and union can be used in their C++ program.

**Table 9.1 Structures & Unions Difference Table**

| Structure | Union |
|---|---|
| Structure is a user-defined data type in C++ that groups different data types together. | Union helps us to group various objects and members of different types and bytes together. |
| Memory allocation for a structure in C++ occurs contiguously. | Memory allocation for a union is determined by the largest member. |
| Data members cannot be initialized inside a structure. This can be done by declaring a structure. | Data members can be initialized and overwritten if the value changes, as the same amount of memory space is affected. |
| All data members are assigned a unique memory space in a structure. | All data members share the memory space equal to the member with the largest size. |
| All data members can be initialized for a structure. | Only the first data member can be initialized for a union. |
| All data members can be accessed together for a structure. | Accessing of data members can be done only one at a time. |

## 9.5 Enum in C++

User-defined data types help our C++ programs to be more flexible and user friendly. They make it easier for the user to understand the language the computer wants to speak. Enumeration (enum) is a unique data type in C++ that allows us to define data types and name elements of our choice to be considered integral constants.

The syntax for enumeration is as follows:

```cpp
enum datatypename { enum values list.... };
```

### Code: Using Enumeration

```cpp
#include <iostream>
using namespace std;

int main()
{
    enum Gender { max, checo = 9, lewis, kimi, mick, ocon };
    int i;
    for (i = checo; i <= ocon; i++)
        cout << i << " ";
    return 0;
}
```

### Output:

```text
9 10 11 12 13
```

### Code Debriefing

- In this code, we use enum with items.
- The for loop traverses the data structure and displays each member as an index number.
- The index is +1, and this can be changed depending on the requirements.

## Practical Questions

1. Write a program in C++ for processing admission reports. Use a structure that has elements representing information such as roll number, name, date of birth (use a nested structure), and branch allotted. The functions processing the members of a structure must be a part of a structure. The format of the report is as follows:

    | Roll.no. | Name | Date of Birth | Branch Allotted |
    |---|---|---|---|
    | XX | xxx | dd/mm/yy | xxxxxxxxxx |

2. Write a program in C++ that processes the date of birth using structures. Include the ability to process multiple students’ dates of birth.

3. Write a program in C++ to process complex numbers. It has to perform addition, subtraction, multiplication, and division of complex numbers. Print the results in x+ iy form.

4. Consider the following structure declaration:

```cpp
struct institution {
    struct teacher {
        int empl_no;
        char name[20];
    };
    struct student {
        int roll_no;
        char name[15];
    };
};
```

What are the values for `sizeof(institution)`, `sizeof(teacher)`, and `sizeof(student)`?

## MCQ-Based

1. What is the correct output of the given code?

```cpp
#include <iostream>
#include <math.h>
using namespace std;

struct st {
    int A = NULL;
    int B = abs(EOF + EOF);
} S;

int main()
{
    cout << S.A << " " << S.B;
    return 0;
}
```

- a. 0 2
- b. 0 0
- c. 2 0
- d. Error

2. What is the correct output of the given code?

```cpp
#include <iostream>
using namespace std;

typedef struct {
    int A = 10;
    int B = 20;
} S;

int main()
{
    cout << S.A << " " << S.B;
    return 0;
}
```

- a. Error
- b. 10 20
- c. 10 0
- d. 0 0

3. What is the correct output of the given code?

```cpp
#include <iostream>
using namespace std;

typedef struct {
    int A;
    char* STR;
} S;

int main()
{
    S ob = { 10, "india" };

    S* ptr;
    ptr = &ob;

    cout << ptr->A << " " << ptr->STR;
    return 0;
}
```

- a. 10 india
- b. Blank output
- c. Garbage value
- d. India 10

4. What is the correct output of the given code?

```cpp
#include <iostream>
using namespace std;

int main()
{
    typedef struct {
        int A;
        char* STR;
    } S;

    S ob = { 10, "india" };
    S* ptr;
    ptr = &ob;

    cout << ptr->A << " " << ptr->STR;
    return 0;
}
```

- a. 10 in
- b. 10 d
- c. 10 india
- d. 10 n

5. What is the correct output of the given code?

```cpp
#include <iostream>
using namespace std;

struct st {
    int A;
```

7. What is the correct output of the given code?

```cpp
#include <iostream>
using namespace std;

struct st1 {
    int A = 10;
    struct st2 {
        char ch = 'A';
    } S;
} SS;

int main()
{
    struct st1* PTR = &SS;
    int X = 0;
    X = PTR->A + PTR->S.ch;
    cout << X;
    return 0;
}
```

- a. 65
- b. 75
- c. 97
- d. 107

8. What will be the output of the following code?

```cpp
#include <iostream>
#include <string.h>
using namespace std;

int main() {
    struct student {
        int num;
        char name[25];
    };

    student stu;
    stu.num = 123;
    strcpy(stu.name, "john");
    cout << stu.num << endl;
    cout << stu.name << endl;
    return 0;
}
```
