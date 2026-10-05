
# 304 CHAPTER 7 Constructors and Other Tools

## Display 7.6 Static Members (part 1 of 2)

```cpp
#include <iostream>
using namespace std;

class Server
{
public:
    Server(char letterName);
    static int getTurn();
    void serveOne();
    static bool stillOpen();
private:
    static int turn;
    static int lastServed;
    static bool nowOpen;
    char name;
};

int Server::turn = 0;
int Server::lastServed = 0;
bool Server::nowOpen = true;

int main() {
    Server s1('A'), s2('B');
    int number, count;
    do {
        cout << "How many in your group? ";
        cin >> number;
        cout << "Your turns are: ";
        for (count = 0; count < number; count++) {
            cout << Server::getTurn() << ' ';
        }
        cout << endl;
        s1.serveOne();
        s2.serveOne();
    } while (Server::stillOpen());

    cout << "Now closing service. ";

    return 0;
}

Server::Server(char letterName) : name(letterName) {
/*Intentionally empty*/
}
```

## Display 7.6 Static Members (part 2 of 2)

> Since getTurn is static, only static members can be referenced in here.

```cpp
int Server::getTurn() {
    turn++;
    return turn;
}
bool Server::stillOpen() {
    return nowOpen;
}
void Server::serveOne() {
    if (nowOpen && lastServed < turn) {
        lastServed++;
        cout << "Server " << name << " now serving " << lastServed << endl;
    }
    if (lastServed >= turn) //Everyone served
        nowOpen = false;
}
```

### Sample Dialogue

- How many in your group? 3
Your turns are: 1 2 3
Server A now serving 1
Server B now serving 2
How many in your group? 2
Your turns are: 4 5
Server A now serving 3
Server B now serving 4
How many in your group? 0
Your turns are:
Server A now serving 5
Now closing service.

Notice that the keyword static is used in the member function declaration but is not used in the member function definition.
The program in Display 7.6 is the outline of a scenario that has one queue of clients waiting for service and two servers to service this single queue. You can come up with a number of system programming scenarios to flesh this out to a realistic example.

## 306 CHAPTER 7 Constructors and Other Tools

For a simple-minded model just to learn the concepts, think of the numbers produced by as those little slips of paper handed out to customers in a delicessen or ice cream shop. The two servers are then two clerks who wait on customers. One perhaps detail of this shop is that customers arrive in groups but are waited at a time (perhaps to order their particular kind of sandwich or ice cream flavor).

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_335_0.png)

## Self-Test Exercise

8. Could the function defined as follows be added to the class Server in Drawing 7.6 as a static function? Explain your answer.

```cpp
void Server::showStatus()
{
    cout << "Currently serving " << turn << endl;
    cout << "server name " << name << endl;
}
```

## Nested and Local Class Definitions

The material in this section is included for reference value and, except for a brief passing reference in Chapter 17, it is not used elsewhere in this book.
You can define a class within a class. Such a class within a class is called a nested class. The general layout is oblique:

nested class

```cpp
class OuterClass
{
public:
    ...
private:
    class InnerClass
    {
        ...
    };
};
```

A nested class can be either public or private. If it is private, as in our sample layout, then it cannot be used outside of the outer class. Whether the nested class is public or private, it can be used in member function definitions of the outer class.
Since the nested class is in the scope of the outer class, the name of the nested class, like InnerClass in our sample layout, may be used for something else outside of the outer class. If the nested class is public, the nested class can be used as a type outside of the outer class. However, outside of the outer class, the type name of the nested class is OuterClass::InnerClass.

## 307 Vectors—A Preview of the Standard Template Library

We will not have occasion to use such nested class definitions in this book. However, in Chapter 17 we do suggest one possible application for nested classes.
A class definition can also be defined within a function definition. In such cases the class is called a local class, since its meaning is confined to the function definition. A local class may not contain static members. We will not have occasion to use local classes in this book.

local class

## 7.3 Vectors—A Preview of the Standard Template Library

> LEWIS CARROLL, Alice’s Adventures in Wonderland

vector

Vectors can be thought of arrays that can grow (and shrink) in length while your program is running. In C++, once your program creates an array, it cannot change the length of the array. Vectors serve the same purpose as arrays except that they can change length while the program is running.
Vectors formed from template in the Standard Template Library (STL). We discuss templates in Chapter 16 and discuss the STL in Chapter 17. However, it is easy to learn basic uses of vectors before you learn about templates and the STL in detail. You do not need to know a great deal about classes to use vectors. You can cover this section on vectors after reading Chapter 6. You do not have to read the previous sections of this chapter before covering this.

## Vector Basics

Like an array, a vector has a base type, and like an array, a vectors stores a collection of values by its type. However, the syntax for a vector and a vector variable declaration is different from the syntax for arrays.
You declare a, v, for a vector with base type int as follows:

declaring a vector variable

```cpp
vector<int>;
```

The notation vector<Base_Type> is a template class, which means you can plug in any type for Base_Type and will produce a class for vectors with that base type. You can simply think of this as specifying the base type for a vector in the same sense as you specify a base type for an array. You can use any type, including classes, as the base type for a vector. The notation vector<int> is a class name and so the previous

template class

> ²The suggestion is in the subsection of Chapter 17 entitled “Friend Classes and Similar Alternatives."

## CHAPTER 7 Constructors and Other Tools

declaration of v as a vector type vector<int> includes a call to the default constructor for the class vector<int> that creates a vector object that is empty (has no elements).

Vector elements are indexed with 0, the same as arrays. The square brackets notation can be used to read or change these elements, just as with an array. For example, the following changes the value of the ith element of the vector v and then outputs that changed value. (i is an int.)

```cpp
v[i] = 42;
cout << "The answer is " << v[i];
```

There is, however, a restriction on this use of square notation with vectors that is unlike the same notation with arrays. You can use v[i] to change the value of the ith element. You cannot initialize the ith using v[i]; you can only change an element that has already been given value. To add to a vector for the first time, you normally use the member function push_back.

You add elements to a vector in order, first at position 0, to position 1, 2, and so so. The member function push_back adds an element in the next available position. For example, the following gives initial values to elements 0, 1, and 2 of the vector sample:

```cpp
vector<double> sample;
sample.push_back(0.0);
sample.push_back(1.1);
sample.push_back(2.2);
```

## Vectors

Vectors are used very much like arrays, but a vector does not have a fixed size. If it needs more capacity to store another element, its capacity is automatically increased. Vectors are defined in the library vector, which places them in the std namespace. Thus, a file that uses vectors would include the following lines:

```cpp
#include <vector>
using namespace std;
```

The vector class for a Base_Type is written vector<Base_Type>. Two sample declarations are as follows:

```cpp
vector<int> v; //default constructor producing an empty vector.
vector<AClass> record(20); //constructor uses the
//default constructor for AClass to initialize 20 elements.
```

Elements are added to a vector using the member function push_back, as illustrated here:

```cpp
v.push_back(42);
```

Once an element position has received its first element, either with push_back or with a constructor initialization, that element position can be accessed using square bracket notation, just like an array element.
