
## explicit Constructor

The IntCell constructor is explicit. You should make all one-parameter constructors explicit to avoid behind-the-scenes type conversions. Otherwise, there are some lenient rules that will allow type conversions without explicit casting operations. Usually, this is unwanted behavior that destroys strong typing and can lead to hard-to-find bugs. As an example, consider the following:

```
IntCell obj;    // obj is an IntCell
obj = 37;       // Should not compile: type mismatch
```

The code fragment above constructs an IntCell object and then performs an assignment statement. But the assignment statement should not work, because the right-hand side of the assignment operator is not another IntCell. obj's write method should have been used instead. However, C++ has lenient rules. Normally, a one-parameter constructor defines an implicit type conversion, in which a temporary object is created that makes an assignment (or parameter to a function) compatible. In this case, the compiler would attempt to convert

```
obj = 37;       // Should not compile: type mismatch
```

into

```
IntCell temporary = 37;
obj = temporary;
```

Notice that the construction of the temporary can be performed by using the one-parameter constructor. The use of explicit means that a one-parameter constructor cannot be used to generate an implicit temporary. Thus, since IntCell's constructor is declared explicit, the compiler will correctly complain that there is a type mismatch.

## Constant Member Function

A member function that examines but does not change the state of its object is an accessor. A member function that changes the state is a mutator (because it mutates the state of the object). In the typical collection class, for instance, isEmpty is an accessor, while makeEmpty is a mutator.

In C++, we can mark each member function as being an accessor or a mutator. Doing so is an important part of the design process and should not be viewed as simply a comment. Indeed, there are important semantic consequences. For instance, mutators cannot be applied to const objects. By default, all member functions are mutators. To make a member function an accessor, we must add the keyword const after the closing parenthesis that ends the parameter type list. The const-ness is part of the signature. const can be used with many different meanings. The function declaration can have const in three different contexts. Only the const after a closing parenthesis signifies an accessor. Other uses are described in Sections 1.5.3 and 1.5.4.

In the IntCell class, read is clearly an accessor: it does not change the state of the IntCell. Thus it is made a constant member function at line 9. If a member function is marked as an accessor but has an implementation that changes the value of any data member, a compiler error is generated.3

## 1.4.3 Separation of Interface and Implementation

The class in Figure 1.6 contains all the correct syntactic constructs. However, in C++ it is more common to separate the class interface from its implementation. The interface lists the class and its members (data and functions). The implementation provides implementations of the functions.

Figure 1.7 shows the class interface for IntCell, Figure 1.8 shows the implementation, and Figure 1.9 shows a main routine that uses the IntCell. Some important points follow:

## Preprocessor Commands

The interface is typically placed in a file that ends with .h. Source code that requires knowledge of the interface must #include the interface file. In our case, this is both the implementation file and the file that contains main. Occasionally, a complicated project will have files including other files, and there is the danger that an interface might be read twice in the course of compiling a file. This can be illegal. To guard against this, each header file uses the preprocessor to define a symbol when the class interface is read. This is shown on the first two lines in Figure 1.7. The symbol name, IntCell_H, should not appear in any other file; usually, we construct it from the filename. The first line of the interface file

```
1 #ifndef IntCell_H
2 #define IntCell_H
3
4 /**
5 * A class for simulating an integer memory cell.
6 */
7 class IntCell
8 {
9 public:
10 explicit IntCell( int initialValue = 0 );
11 int read( ) const;
12 void write( int x );
13
14 private:
15 int storedValue;
16 };
17
18 #endif
```

**Figure 1.7** IntCell class interface in file IntCell.h

3 Data members can be marked mutable to indicate that const-ness should not apply to them.

```cpp
#include "IntCell.h"
/**
 * Construct the IntCell with initialValue
 */
IntCell::IntCell( int initialValue ) : storedValue{ initialValue }
{
}
/**
 * Return the stored value.
 */
int IntCell::read( ) const
{
    return storedValue;
}
/**
 * Store x.
 */
void IntCell::write( int x )
{
    storedValue = x;
}
```

**Figure 1.8** IntCell class implementation in file IntCell.cpp

```cpp
#include <iostream>
#include "IntCell.h"
using namespace std;

int main( )
{
    IntCell m;

    m.write( 5 );
    cout << "Cell contents: " << m.read( ) << endl;

    return 0;
}
```

**Figure 1.9** Program that uses IntCell in file TestIntCell.cpp

tests whether the symbol is undefined. If so, we can process the file. Otherwise, we do not process the file (by skipping to the #endif), because we know that we have already read the file.

## Scope Resolution Operator

In the implementation file, which typically ends in .cpp, .cc, or .c, each member function must identify the class that it is part of. Otherwise, it would be assumed that the function is in global scope (and zillions of errors would result). The syntax is ClassName::member. The :: is called the scope resolution operator.

## Signatures Must Match Exactly

The signature of an implemented member function must match exactly the signature listed in the class interface. Recall that whether a member function is an accessor (via the const at the end) or a mutator is part of the signature. Thus an error would result if, for example, the const was omitted from exactly one of the read signatures in Figures 1.7 and 1.8. Note that default parameters are specified in the interface only. They are omitted in the implementation.

## Objects Are Declared Like Primitive Types

In classic C++, an object is declared just like a primitive type. Thus the following are legal declarations of an IntCell object:

```
IntCell obj1; // Zero parameter constructor
IntCell obj2( 12 ); // One parameter constructor
```

On the other hand, the following are incorrect:

```
IntCell obj3 = 37; // Constructor is explicit
IntCell obj4( ); // Function declaration
```

The declaration of obj3 is illegal because the one-parameter constructor is explicit. It would be legal otherwise. (In other words, in classic C++ a declaration that uses the one-parameter constructor must use the parentheses to signify the initial value.) The declaration for obj4 states that it is a function (defined elsewhere) that takes no parameters and returns an IntCell.

The confusion of obj4 is one reason for the uniform initialization syntax using braces. It was ugly that initializing with zero parameter in a constructor initialization list (Fig. 1.6, line 8) would require parentheses with no parameter, but the same syntax would be illegal elsewhere (for obj4). In C++11, we can instead write:

```
IntCell obj1; // Zero parameter constructor, same as before
IntCell obj2{ 12 }; // One parameter constructor, same as before
IntCell obj4{ }; // Zero parameter constructor
```

The declaration of obj4 is nicer because initialization with a zero-parameter constructor is no longer a special syntax case; the initialization style is uniform.

```
#include <iostream>
#include <vector>
using namespace std;

int main( )
{
    vector<int> squares( 100 );

    for( int i = 0; i < squares.size( ); ++i )
        squares[ i ] = i * i;

    for( int i = 0; i < squares.size( ); ++i )
        cout << i << " " << squares[ i ] << endl;

    return 0;
}
```

![](img/e449061a0cac9cafaefd979fab665b33_37_0.png)

## 1.4.4 vector and string

The C++ standard defines two classes: the vector and string. vector is intended to replace the built-in C++ array, which comes no end of trouble. The problem with the built-in C++ array is that it does not behave like a first-class object. For instance, built-in arrays cannot be copied with *, a built-in array does not remember how many items it can store, and its indexing operator does not check that the index is valid. The built-in string is simply an array of characters, and thus has the liabilities of arrays plus a few more. For instance, == does not correctly compare two built-in strings.

The vector and string classes in the STL treat arrays and strings as first-class objects. A vector knows how large it is. Two string objects can be compared with ==, <, and so on. Both vector and string can be copied with =. If possible, you should avoid using the built-in C++ array and string. We discuss the built-in array in Chapter 3 in the context of showing how vector can be implemented.

vector and string are easy to use. The code in Figure 1.10 creates a vector that stores one hundred perfect squares and outputs them. Notice also that size is a method that returns the size of the vector. A nice feature of the vector that we explore in Chapter 3 is that it is easy to change its size. In many cases, the initial size is 0 and the vector grows as needed.

C++ has long allowed initialization of built-in C++ arrays:

```
int daysInMonth[] = { 31, 28, 31, 30, 31, 30, 31, 30, 31, 30, 31 };
```

It was annoying that this syntax was not legal for vectors. In older C++, vectors were either initialized with size 0 or possibly by specifying a size. So, for instance, we would write:
