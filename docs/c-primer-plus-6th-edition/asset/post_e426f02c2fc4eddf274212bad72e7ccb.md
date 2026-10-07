
```cpp
double Student::operator[](int i) const
{
    return ArrayDb::operator[](i);
}
```

```cpp
// private method
ostream & Student::arr_out(ostream & os) const
{
    int i;
    int lim = ArrayDb::size();
    if (lim > 0) {
        for (i = 0; i < lim; i++) {
            os << ArrayDb::operator[](i) << " ";
            if (i % 5 == 4)
                os << endl;
        }
        if (i % 5 != 0)
            os << endl;
    } else {
        os << " empty array ";
        return os;
    }
}
```

```cpp
// friends
// use String version of operator>>(
istream & operator>>(istream & is, Student & stu)
{
    is >> (string &)stu;
    return is;
}
```

```cpp
// use string friend getline(ostream &, const string &)
istream & getline(istream & is, Student & stu)
{
    getline(is, (string &)stu);
    return is;
}
```

```cpp
// use string version of operator<<(ostream & os, const Student & stu)
{
    os << "Scores for " << (const string &)stu << ":\n";
    stu.arr_out(os); // use private method for scores
    return os;
}
```

Again, because the example reuses the string and valarray code, relatively new code is needed, aside from the private helper method.

## Using the Revised Student Class

Once again, it's time to test a new class. Note that the two versions of the Student class have exactly the same public interface, so you can test the two versions with exactly the same program. The only difference is that you have to include student.i instead of student.h, and you have to link the program with studenti.cpp instead of student.cpp. Listing 14.6 shows the program. Be sure to compile it along with student.cpp.

Listing 14.6 use_stui.cpp

```cpp
// use_stui.cpp -- using a class with private inheritance
// compile with studenti.cpp
#include <iostream>
#include "studenti.h"

using std::cin;
using std::cout;
using std::endl;

void set(Student & sa, int n);

const int pupils = 3;
const int quizzes = 5;

int main()
{
    Student ada[pupils] =
    {Student(quizzes), Student(quizzes), Student(quizzes)};

    int i;
    for (i = 0; i < pupils; i++)
        set(ada[i], quizzes);
    cout << "\nStudent List:\n";
    for (i = 0; i < pupils; i++)
        cout << ada[i].Name << endl;
    cout << "\nResults:\n";
    for (i = 0; i < pupils; i++)
        {
            cout << endl << ada[i];
            cout << "  average: " << ada[i].Average() << endl;
        }

    cout << "  Done.\n";
    return 0;
}
```

```cpp
void set(Student & sa, int n)
{
    cout << "Please enter the student's name: ";
    getline(cin, sa);
    cout << "Please enter " << n << " quiz scores:\n";
    for (int i = 0; i < n; i++)
        cin >> sa(i);
        while (cin.get() != '\n')
            continue;
    }
}
```

Here is a sample run of the program in Listing 14.6:

Please enter the student's name: Gil Bays
Please enter 5 quiz scores:
92 94 96 93 95

Please enter the student's name: Pat Boone
Please enter 5 quiz scores:
83 89 72 78 95

Please enter the student's name: Fleur O'Day
Please enter 5 quiz scores:
92 89 96 74 64

Student List:
Gil Bays
Pat Boone
Fleur O'Day

Results:
Scores for Gil Bays:
92 94 96 93 95
average: 94

Scores for Pat Boone:
83 89 72 78 95
average: 83.4

Scores for Fleur O'Day:
92 89 96 74 64
average: 83
Done.

The same input as before leads to the same output that the containment version produces.

Chapter 14 Reusing Code in C++

## Containment or Private Inheritance?

Given that you model a has-a relationship with containment or with private inheritance, which should you use? Most C++ programmers prefer containment. First, it's easier to follow. When you look at the class declaration, you see explicitly named objects representing the contained classes, and your code can refer to these objects by name. Using inheritance makes the relationship more abstract. Second, inheritance can raise problems, particularly if a class inherits from more than one class. You may have to deal with issues as separate base classes having methods with the same name or of separate classes sharing a common ancestor. All in all, you're less likely to run into trouble using containment. If a class needs three string objects, you can declare separate string members by using the containment approach. But inheritance limits you to a single object. (It is difficult to tell objects apart when they are nameless.)

However, private inheritance offers features beyond those provided by containment. Suppose, for example, that a class has protected members, which could be either data members or functions. Such members are available to derived classes but not to the world at large. If you include such a class in another by composition, the new class is part of the world at large, not a derived class. Hence it can't access protected members. But using inheritance makes the new class a derived class, so it can access protected members.

Another situation that calls for using inheritance is if you need to redefine functions. Again, this is a privilege accorded to a derived class but not to a containing class. With private inheritance, the redefined functions would be just within the class, not publicly.

> **Tip**: In general, you should use containment to model a has-a relationship. You should use private inheritance if the new class needs to access protected members in the original class or if it needs to redefine virtual functions.

## Protected Inheritance

Protected inheritance is a variation of private inheritance. It uses the keyword protected when listing a base class:

```cpp
class Student : protected std::string,
    protected std::vector<double>
{...
```

With protected inheritance, public and protected members of a base class become protected of the derived class. As with private inheritance, the interface for the base class is available to the derived class but not to the world. The main difference between private inheritance and protected inheritance occurs when you derive another class from the derived class. With private inheritance, this third-generation class doesn't get the base-class interface. The public-class methods become

## Private

 in the derived class, and private members and methods can't be directly accessed by the next level of derivation. With protected inheritance, public base-class methods become protected in the second generation and are available internally to the next level of derivation.

Table 14.1 summarizes public, private, and protected inheritance. The term implicit upcasting means that you can have a base-class pointer or reference refer to a derived class without using an explicit type.

Table 14.1 Varieties of Inheritance

| Property | Public Inheritance | Protected Inheritance | Private Inheritance |
| :--- | :--- | :--- | :--- |
| Public members become | Public members of the derived class | Protected members of the derived class | Private members of the derived class |
| Protected members become | Protected members of the derived class | Protected members of the derived class | Private members of the derived class |
| Private members become | Accessible only through the base-class interface | Accessible only through the base-class interface | Accessible only through the base-class interface |
| Implicit upcasting | Yes | Yes (but only the derived class) | No |

## Redefining Access with using

Public members of a base class become protected or private when you use protected or private derivation. Suppose you want to make a particular base-class method available publicly in the derived class. For example, suppose you want the student class to be able to use the valarray sum() method. You can declare a sum() method in the class declaration and then define the method this way:

```cpp
double Student::sum() const // public Student method
    return std::valarray<double>::sum(); // use privately-inherited method
}
```

Then an object can invoke Student::sum(), which, in turn, applies the valarray-double::sum() method to the embedded valarray object. The ArrayDb typedef is in scope, you can use ArrayDb instead of std::valarray<double>.

There is an alternative to wrapping one function in another: using a declaration (like using namespaces) to announce that a particular base-class member can be used by the derived class, even though the derivation is private. For example, suppose you want to be able to use the valarray min() and max() methods with the
