
832 Chapter 14 Reusing Code in C++

You can use your choice of generic type name in the Type position; the name rules are the same as for any other identifier. Popular choices include T and Type; in this case, we'll use the later. When a template is invoked, Type will be replaced with a specific type value, such as int or string. Within the template definition, you can use the generic type name to identify the type to be stored in the stack. For the Stack, that would mean using Type over the old declaration formerly used by the typedef identifier Item. For example,

```
Item items [MAX]; // holds stack items
```

becomes the following:

```
Type items [MAX]; // holds stack items
```

Similarly, you can replace the class methods of the original class with template member functions. Each function heading will be prefaced with the same template announcement:

```
template <class Type>
```

Again, you should replace the typedef Item with the generic type name. One more change is that you need to change the class qualifier from Stack:: to Stack<Type>::. For example,

```
bool Stack::push(const Item & item)
{
...
}
```

becomes the following:

```
template <class Type> // or template <typename Type>
bool Stack<Type>::push(const Type & item)
{
}
```

If you define a method within the class declaration (an inline definition), you can omit the template preface and the class qualifier.

Listing 14.13 shows the combined class and member function templates. It's important to realize that these templates are not class and member function definitions. Rather, they are instructions to the C++ compiler how to generate class and member function definitions. A particular specialization of a template, such as a stack for handling string objects, could be an instantiation or a specialization. Placing the template member functions in a separate implementation file won't work. (For while, the standard did provide the keyword export to allow such a separate implementation file. But not many vendors implemented it. C++11 discontues that use of export but reserves the keyword for future use.) Because templates are not functions, can't be compiled separately. Templates have to be used in conjunction with requests for particular instantiations of templates. The simplest way to make this work is to place all the template information in a header file and to include the header file in the file that will use the templates.

# Class Templates

Listing 14.13 stacktp.h

```cpp
// stacktp.h -- a stack template
#ifndef STACKTP_H_
#define STACKTP_H_
template <class Type>
class Stack {
private:
    enum { MAX = 10 };          // constant specific to class
    Type items[MAX];            // holds stack items
    int top;                    // index for top stack item
public:
    Stack();
    bool nonempty();
    bool isfull();
    bool push(const Type & item); // add item to stack
    bool pop(Type & item);        // pop top into item
};

template <class Type>
Stack<Type>::Stack() {
    top = 0;
}

template <class Type>
bool Stack<Type>::isNotEmpty() {
    return top == 0;
}

template <class Type>
bool Stack<Type>::isfull() {
    return top == MAX;
}

template <class Type>
bool Stack<Type>::push(const Type &item) {
    if (top < MAX) {
        items[top++] = item;
        return true;
    }
    else
      return false;
}

template <class Type>
bool Stack<Type>::pop(Type & item)
{
  if (top > 0)
  {
    item = items[--top];
    return true;
  }
  else
  return false;
}
#endif
```

# Using a Template Class

Merely including a template in a program doesn't generate a template class. You have to ask for an instantiation. To do this you declare an object of the template class type, replacing the generic type with the particular type you want. For example, here's how you would create stacks, one for stacking ints and one for stacking string objects:

```cpp
Stack<int> kernels; // create a stack of ints
Stack<string> colons; // create a stack of string objects
```

Seeing these two declarations, the compiler will follow the Stack<Type> template to generate two separate classes and two sets of methods. The Stack<int> class declaration will replace Type throughout int, and the Stack<string> class declaration will replace Type throughout string. Of course, the algorithms you use have be consistent with the types. The Stack class, for example, assumes that you can assign one item to another. This assumption is true for basic types, structures and classes (unless you make the assignment operator private) but for arrays.

Generic type identifiers as Type in the example are called type parameters, meaning that they acting like variables, but instead of assigning a numeric value to a parameter, you assign a type to it. So in the kernel declaration, the type parameter Type has the int value.

Notice that you have to provide the desired type explicitly. This is different from ordinary function templates, for which the compiler can use the argument types to a function to figure out what kind of function to generate:

```cpp
template <class T>
void simple(T t) { cout << t << '\n'; }
```

```cpp
#include <iostream>
#include <string>
#include <cctype>
#include "stacktp.h"
using namespace std;

template <class T>
void simple(T t) { cout << t << '\n'; }

int main() {
    Stack<int> kernels;
    Stack<string> colons;

    kernels.push(10);
    kernels.push(20);
    colons.push("hello");
    colons.push("world");

    int i;
    string s;

    kernels.pop(i);
    cout << i << endl;

    colons.pop(s);
    cout << s << endl;

    simple(10);
    simple("hello");

    return 0;
}
```

834 Chapter 14 Reusing Code in C++

```cpp
#include <iostream>
#include <string>
#include <cctype>
#include "stacktp.h"
using namespace std;

template <class T>
void simple(T t) { cout << t << '\n'; }

int main() {
    Stack<int> kernels;
    Stack<string> colons;

    kernels.push(10);
    kernels.push(20);
    colons.push("hello");
    colons.push("world");

    int i;
    string s;

    kernels.pop(i);
    cout << i << endl;

    colons.pop(s);
    cout << s << endl;

    simple(10);
    simple("hello");

    return 0;
}
```

Wait, the OCR text had some repetitions and garble at the end. Let me re-clean the final output based on the logical flow of the provided text.

---

[content]
832 Chapter 14 Reusing Code in C++

You can use your choice of generic type name in the Type position; the name rules are the same as for any other identifier. Popular choices include T and Type; in this case, we'll use the later. When a template is invoked, Type will be replaced with a specific type value, such as int or string. Within the template definition, you can use the generic type name to identify the type to be stored in the stack. For the Stack, that would mean using Type over the old declaration formerly used by the typedef identifier Item. For example,

```
Item items [MAX]; // holds stack items
```

becomes the following:

```
Type items [MAX]; // holds stack items
```

Similarly, you can replace the class methods of the original class with template member functions. Each function heading will be prefaced with the same template announcement:

```
template <class Type>
```

Again, you should replace the typedef Item with the generic type name. One more change is that you need to change the class qualifier from Stack:: to Stack<Type>::. For example,

```
bool Stack::push(const Item & item)
{
...
}
```

becomes the following:

```
template <class Type> // or template <typename Type>
bool Stack<Type>::push(const Type & item)
{
}
```

If you define a method within the class declaration (an inline definition), you can omit the template preface and the class qualifier.

Listing 14.13 shows the combined class and member function templates. It's important to realize that these templates are not class and member function definitions. Rather, they are instructions to the C++ compiler how to generate class and member function definitions. A particular specialization of a template, such as a stack for handling string objects, could be an instantiation or a specialization. Placing the template member functions in a separate implementation file won't work. (For while, the standard did provide the keyword export to allow such a separate implementation file. But not many vendors implemented it. C++11 discontues that use of export but reserves the keyword for future use.) Because templates are not functions, can't be compiled separately. Templates have to be used in conjunction with requests for particular instantiations of templates. The simplest way to make this work is to place all the template information in a header file and to include the header file in the file that will use the templates.

# Class Templates

Listing 14.13 stacktp.h

```cpp
// stacktp.h -- a stack template
#ifndef STACKTP_H_
#define STACKTP_H_
template <class Type>
class Stack {
private:
    enum { MAX = 10 };          // constant specific to class
    Type items[MAX];            // holds stack items
    int top;                    // index for top stack item
public:
    Stack();
    bool nonempty();
    bool isfull();
    bool push(const Type & item); // add item to stack
    bool pop(Type & item);        // pop top into item
};

template <class Type>
Stack<Type>::Stack() {
    top = 0;
}

template <class Type>
bool Stack<Type>::isNotEmpty() {
    return top == 0;
}

template <class Type>
bool Stack<Type>::isfull() {
    return top == MAX;
}

template <class Type>
bool Stack<Type>::push(const Type &item) {
    if (top < MAX) {
        items[top++] = item;
        return true;
    }
    else
      return false;
}

template <class Type>
bool Stack<Type>::pop(Type & item)
{
  if (top > 0)
  {
    item = items[--top];
    return true;
  }
  else
  return false;
}
#endif
```

# Using a Template Class

Merely including a template in a program doesn't generate a template class. You have to ask for an instantiation. To do this you declare an object of the template class type, replacing the generic type with the particular type you want. For example, here's how you would create stacks, one for stacking ints and one for stacking string objects:

```cpp
Stack<int> kernels; // create a stack of ints
Stack<string> colons; // create a stack of string objects
```

Seeing these two declarations, the compiler will follow the Stack<Type> template to generate two separate classes and two sets of methods. The Stack<int> class declaration will replace Type throughout int, and the Stack<string> class declaration will replace Type throughout string. Of course, the algorithms you use have be consistent with the types. The Stack class, for example, assumes that you can assign one item to another. This assumption is true for basic types, structures and classes (unless you make the assignment operator private) but for arrays.

Generic type identifiers as Type in the example are called type parameters, meaning that they acting like variables, but instead of assigning a numeric value to a parameter, you assign a type to it. So in the kernel declaration, the type parameter Type has the int value.

Notice that you have to provide the desired type explicitly. This is different from ordinary function templates, for which the compiler can use the argument types to a function to figure out what kind of function to generate:

```cpp
template <class T>
void simple(T t) { cout << t << '\n'; }
```

834 Chapter 14 Reusing Code in C++

(Note: The OCR text became highly garbled/repeated at the end. I have reconstructed the logical content flow based on the provided pages.)
[/content]

Wait, I should provide the *final* version without my meta-commentary. Let me re-do the final output block properly.

[content]
832 Chapter 14 Reusing Code in C++

You can use your choice of generic type name in the Type position; the name rules are the same as for any other identifier. Popular choices include T and Type; in this case, we'll use the later. When a template is invoked, Type will be replaced with a specific type value, such as int or string. Within the template definition, you can use the generic type name to identify the type to be stored in the stack. For the Stack, that would mean using Type over the old declaration formerly used by the typedef identifier Item. For example,

```
Item items [MAX]; // holds stack items
```

becomes the following:

```
Type items [MAX]; // holds stack items
```

Similarly, you can replace the class methods of the original class with template member functions. Each function heading will be prefaced with the same template announcement:

```
template <class Type>
```

Again, you should replace the typedef Item with the generic type name. One more change is that you need to change the class qualifier from Stack:: to Stack<Type>::. For example,

```
bool Stack::push(const Item & item)
{
...
}
```

becomes the following:

```
template <class Type> // or template <typename Type>
bool Stack<Type>::push(const Type & item)
{
}
```

If you define a method within the class declaration (an inline definition), you can omit the template preface and the class qualifier.

Listing 14.13 shows the combined class and member function templates. It's important to realize that these templates are not class and member function definitions. Rather, they are instructions to the C++ compiler how to generate class and member function definitions. A particular specialization of a template, such as a stack for handling string objects, could be an instantiation or a specialization. Placing the template member functions in a separate implementation file won't work. (For while, the standard did provide the keyword export to allow such a separate implementation file. But not many vendors implemented it. C++11 discontues that use of export but reserves the keyword for future use.) Because templates are not functions, can't be compiled separately. Templates have to be used in conjunction with requests for particular instantiations of templates. The simplest way to make this work is to place all the template information in a header file and to include the header file in the file that will use the templates.

# Class Templates

Listing 14.13 stacktp.h

```cpp
// stacktp.h -- a stack template
#ifndef STACKTP_H_
#define STACKTP_H_
template <class Type>
class Stack {
private:
    enum { MAX = 10 };          // constant specific to class
    Type items[MAX];            // holds stack items
    int top;                    // index for top stack item
public:
    Stack();
    bool nonempty();
    bool isfull();
    bool push(const Type & item); // add item to stack
    bool pop(Type & item);        // pop top into item
};

template <class Type>
Stack<Type>::Stack() {
    top = 0;
}

template <class Type>
bool Stack<Type>::isNotEmpty() {
    return top == 0;
}

template <class Type>
bool Stack<Type>::isfull() {
    return top == MAX;
}

template <class Type>
bool Stack<Type>::push(const Type &item) {
    if (top < MAX) {
        items[top++] = item;
        return true;
    }
    else
      return false;
}

template <class Type>
bool Stack<Type>::pop(Type & item)
{
  if (top > 0)
  {
    item = items[--top];
    return true;
  }
  else
  return false;
}
#endif
```

# Using a Template Class

Merely including a template in a program doesn't generate a template class. You have to ask for an instantiation. To do this you declare an object of the template class type, replacing the generic type with the particular type you want. For example, here's how you would create stacks, one for stacking ints and one for stacking string objects:

```cpp
Stack<int> kernels; // create a stack of ints
Stack<string> colons; // create a stack of string objects
```

Seeing these two declarations, the compiler will follow the Stack<Type> template to generate two separate classes and two sets of methods. The Stack<int> class declaration will replace Type throughout int, and the Stack<string> class declaration will replace Type throughout string. Of course, the algorithms you use have be consistent with the types. The Stack class, for example, assumes that you can assign one item to another. This assumption is true for basic types, structures and classes (unless you make the assignment operator private) but for arrays.

Generic type identifiers as Type in the example are called type parameters, meaning that they acting like variables, but instead of assigning a numeric value to a parameter, you assign a type to it. So in the kernel declaration, the type parameter Type has the int value.

Notice that you have to provide the desired type explicitly. This is different from ordinary function templates, for which the compiler can use the argument types to a function to figure out what kind of function to generate:

```cpp
template <class T>
void simple(T t) { cout << t << '\n'; }
```
