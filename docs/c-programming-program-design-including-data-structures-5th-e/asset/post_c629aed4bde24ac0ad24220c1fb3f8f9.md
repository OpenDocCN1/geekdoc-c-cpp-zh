
Example 11-9 further illustrates how classes are designed and implemented. The class personType that is designed in Example 11-9 is very useful; we will use this class in subsequent chapters.

### EXAMPLE 11-9

The most common attributes of a person are the person’s first name and last name. The typical operations on a person’s name are to set the name and print the name. The following statements define a class with these properties.

```cpp
#include <string>

using namespace std;

class personType
{
public:
    void print() const;
        //Function to output the first name and last name
        //in the form firstName lastName.

    void setName(string first, string last);
        //Function to set firstName and lastName according
        //to the parameters.
        //Postcondition: firstName = first; lastName = last;

    string getFirstName() const;
        //Function to return the first name.
        //Postcondition: The value of firstName is returned.

    string getLastName() const;
        //Function to return the last name.
        //Postcondition: The value of lastName is returned.

    personType(string first = "", string last = "");
        //Constructor
        //Sets firstName and lastName according to the parameters.
        //The default values of the parameters are null strings.
        //Postcondition: firstName = first; lastName = last;

private:
    string firstName; //variable to store the first name
    string lastName;  //variable to store the last name
};
```

Figure 11-11 shows the UML class diagram of the class personType.

![](img/f97f778697507bb6fdd80c5991210cba_683_0.png)

**FIGURE 11-11** UML class diagram of the class `personType`

We now give the definitions of the member functions of the class `personType`.

```cpp
void personType::print() const
{
    cout << firstName << " " << lastName;
}

void personType::setName(string first, string last)
{
    firstName = first;
    lastName = last;
}

string personType::getFirstName() const
{
    return firstName;
}

string personType::getLastName() const
{
    return lastName;
}

//constructor
personType::personType(string first, string last)
{
    firstName = first;
    lastName = last;
}
```

## Static Members of a Class

**NOTE** This section may be skipped without any loss of continuation.

In Chapter 7, we described two types of variables, automatic and static. Recall that if a local variable of a function is static, it exists between function calls. Similar to static variables, a class can have static members, functions, or variables. Let us note the following about the static members of a class:

- If a function of a class is `static`, in the class definition it is declared using the keyword `static` in its heading.
- If a member variable of a class is `static`, it is declared using the keyword `static`, as discussed in Chapter 7 and also illustrated in Example 11–10.
- A `public static` member, function, or variable of a class can be accessed using the class name and the scope resolution operator.

Example 11–10 clarifies the effect of the keyword `static`.

### EXAMPLE 11-10

Consider the following definition of the class `illustrate`:

```cpp
class illustrate
{
public:
        static int count;    //public static variable

        void print() const;
                //Function to output x, y, and count.

        void setX(int a);
                //Function to set x.
                //Postcondition: x = a;

        static void incrementY();
                //static function
                //Function to increment y by 1.
                //Postcondition: y = y + 1

        illustrate(int a = 0);
                //constructor
                //Postcondition: x = a;
                //                         If no value is specified for a, x = 0;

private:
    int x;
    static int y;  // private static variable
};
```

Suppose that the `static` member variables and the definitions of the member functions of the `class illustrate` are as follows. (These statements are all placed in the implementation file. Also, notice that all `static` member variables are initialized, as shown below.)

```cpp
int illustrate::count = 0;
int illustrate::y = 0;

void illustrate::print() const
{
    cout << "x = " << x << ", y = " << y
         << ", count = " << count << endl;
}

void illustrate::setX(int a)
{
    x = a;
}

void illustrate::incrementY()
{
    y++;
}

illustrate::illustrate(int a)
{
    x = a;
}
```

Because the function `incrementY` is `static` and `public`, the following statement is legal:

```cpp
illustrate::incrementY();
```

Similarly, because the member variable `count` is `static` and `public`, the following statement is legal:

```cpp
illustrate::count++;
```

Next, we elaborate on `static` member variables a bit more. Suppose that you have a `class`, say, `myClass`, with member variables (`static` as well as non-static). When you create objects of type `myClass`, only non-static member variables of the `class myClass` become the member variables of each object. For each `static` member variable of a `class`, C++ allocates only one memory space. All `myClass` objects refer to the same memory space. In fact, `static` member variables of a `class` exist even when no object of that class type exists. You can access the `public static` member variables outside of the class, as explained earlier in this section.

Next, we explain how memory space is allocated for `static` and non-`static` member variables of a class.

Suppose that you have the class `illustrate`, as given in Example 11-10. Memory space then exists for the `static` member variables `y` and `count`.

Consider the following statements:

```cpp
illustrate illusObject1(3);    //Line 1
illustrate illusObject2(5);    //Line 2
```

The statements in Line 1 and Line 2 declare `illusObject1` and `illusObject2` to be `illustrate` type objects (see Figure 11-12).

![](img/f97f778697507bb6fdd80c5991210cba_686_0.png)

**FIGURE 11-12** `illusObject1` and `illusObject2`

Now, consider the following statements:

```cpp
illustrate::incrementY();
illustrate::count++;
```

After these statements execute, the objects and static members are as shown in Figure 11-13.

![](img/f97f778697507bb6fdd80c5991210cba_686_1.png)

**FIGURE 11-13** `illusObject1` and `illusObject2` after the statements `illustrate::incrementY();` and `illustrate::count++;` execute

The output of the statement:

```text
illusObject1.print();
```

is:

```text
x = 3, y = 1, count = 1
```

Similarly, the output of the statement:

```text
illusObject2.print();
```

is:

```text
x = 5, y = 1, count = 1
```

Now consider the statement:

```text
illustrate::count++;
```

After this statement executes, the objects and static members are as shown in Figure 11-14.

![](img/f97f778697507bb6fdd80c5991210cba_687_0.png)

**FIGURE 11-14** illusObject1 and illusObject2 after the statement `illustrate::count++;` executes

The output of the statements:

```text
illusObject1.print();
illusObject2.print();
```

is:

```text
x = 3, y = 1, count = 2
x = 5, y = 1, count = 2
```

The program in Example 11–11 further illustrates how static members of a class work.

### EXAMPLE 11-11

```cpp
#include <iostream>

#include "illustrate.h"

using namespace std;

int main()
{
    illustrate illusObject1(3);                         //Line 1
    illustrate illusObject2(5);                         //Line 2

    illustrate::incrementY();                           //Line 3
    illustrate::count++;                                //Line 4
    illusObject1.print();                               //Line 5
    illusObject2.print();                               //Line 6
    cout << "Line 7: *** Increment y using "
         << "illusObject1***" << endl;                 //Line 7

    illusObject1.incrementY();                          //Line 8
    illusObject1.setX(8);                                //Line 9
    illusObject1.print();                               //Line 10
    illusObject2.print();                               //Line 11

    cout << "Line 12: *** Increment y using "
         << "illusObject2***" << endl;                 //Line 12

    illusObject2.incrementY();                          //Line 13
    illusObject2.setX(23);                               //Line 14
    illusObject1.print();                               //Line 15
    illusObject2.print();                               //Line 16

    return 0;
}
```

### Sample Run

```text
x = 3, y = 1, count = 1
x = 5, y = 1, count = 1
Line 7: *** Increment y using illusObject1***
x = 8, y = 2, count = 1
x = 5, y = 2, count = 1
Line 12: *** Increment y using illusObject2***
x = 8, y = 3, count = 1
x = 23, y = 3, count = 1
```

The preceding program works as follows. The static member variables y and count are initialized to 0. The statement in Line 1 declares illusObject1 to be an object of the class illustrate and initializes its member variable x to 3. The statement in
