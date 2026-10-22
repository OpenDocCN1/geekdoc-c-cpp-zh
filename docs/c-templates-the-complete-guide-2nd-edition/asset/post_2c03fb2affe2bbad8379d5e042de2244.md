
equal.

2 Before C++17, type T also had to be copyable to be able to pass in arguments, but since C++17 you can pass temporaries (rvalues, see Appendix B) even if neither a copy nor a move constructor is valid.

3 For example, if one argument type is defined in namespace std (such as std::string), according to the lookup rules of C++, both the global and the max() template in std are found (see Appendix C).

4 A “one-entity-fits-all” alternative is conceivable but not used in practice (it would be less efficient at run time). All language rules are based on the principle that different entities are generated for different template arguments.

5 The terms instance and instantiate are used in a different context in object-oriented programming—namely, for a concrete object of a class. However, because this book is about templates, we use this term for the “use” of templates unless otherwise specified.

6 For example, The Visual C++ compiler in some versions (such as Visual Studio 2013 and 2015) allow undeclared names that don’t depend on template parameters and even some syntax flaws (such as a missing semicolon).

7 Deduction can be seen as part of overload resolution—a process that is not based on selection of return types either. The sole exception is the return type of conversion operator members.

8 In C++, the return type also cannot be deduced from the context in which the caller uses the call.

9 Prior to C++11, default template arguments were only permitted in class templates, due to a historical glitch in the development of function templates.

10 Again, in C++11 you had to use typename std::decay<...>::type instead of std::decay_t<...> (see Section 2.8 on page 40).

11 In general, a conforming compiler isn’t even permitted to reject this code.

## Chapter 2
## Class Templates

Similar to functions, classes can also be parameterized with one or more types. Container classes, which are used to manage elements of a certain type, are a typical example of this feature. By using class templates, you can implement such container classes while the element type is still open. In this chapter we use a stack as an example of a class template.

### 2.1 Implementation of Class Template Stack

As we did with function templates, we declare and define class Stack<> in a header file as follows: Click here to view code image

*basics/stack1.hpp*

```
#include <vector>
#include <cassert>

template<typename T>
class Stack {
private:
std::vector<T> elems; // elements
public:

void push(T const& elem); // push element
void pop(); // pop element
T const& top() const; // return top element
bool empty() const { // return whether the stack is empty
return elems.empty();
}
};
template<typename T>
void Stack<T>::push (T const& elem)
{
elems.push_back(elem); // append copy of passed elem}
```

```
template<typename T>
void Stack<T>::pop ()
{
assert(!elems.empty());
elems.pop_back(); // remove last element
}
```

```
template<typename T>
T const& Stack<T>::top () const
{
assert(!elems.empty());
return elems.back(); // return copy of last element
}
```

As you can see, the class template is implemented by using a class template of the C++ standard library: vector<>. As a result, we don’t have to implement memory management, copy constructor, and assignment operator, so we can concentrate on the interface of this class template.

### 2.1.1 Declaration of Class Templates

Declaring class templates is similar to declaring function templates: Before the declaration, you have to declare one or multiple identifiers as a type parameter(s). Again, T is usually used as an identifier: Click here to view code image

```
template<typename T>
class Stack {
...;
};
```

Here again, the keyword class can be used instead of typename: Click here to view code image

```
template<class T>
class Stack {
...;
};
```

Inside the class template, T can be used just like any other type to declare members and member functions. In this example, T is used to declare the type of the elements as vector of Ts, to declare push() as a member function that uses a T as an argument, and to declare top() as a function that returns a T: Click here to view code image

```
template<
typename T>
class Stack {
```

```
private:
std::vector<T> elems; // elements

public:
void push(T const& elem); // push element
void pop(); // pop element
T const& top()
const; // return top element
bool empty() const { // return whether the stack is empty
return elems.empty();
}
};
```

The type of this class is `Stack<T>`, with T being a template parameter. Thus, you have to use `Stack<T>` whenever you use the type of this class in a declaration except in cases where the template arguments can be deduced. However, inside a class template using the class name not followed by template arguments represents the class with its template parameters as its arguments (see Section 13.2.3 on page 221 for details).

If, for example, you have to declare your own copy constructor and assignment operator, it typically looks like this: [Click here to view code image](#)

```
template<typename T>
class Stack {
...
Stack (Stack const&); // copy constructor
Stack& operator= (Stack const&); // assignment operator
...
};
```

which is formally equivalent to: [Click here to view code image](#)

```
template<typename T>
class Stack {
...
Stack (Stack<T> const&); // copy constructor
Stack<T>& operator= (Stack<T> const&); // assignment operator
...
};
```

but usually the <T> signals special handling of special template parameters, so it’s usually better to use the first form.

However, outside the class structure you’d need: [Click here to view code image](#)

```
template<typename T>
bool operator== (Stack<T> const& lhs, Stack<T> const& rhs); Note that in places where the name and not the type of the class is required, only Stack may be used. This is especially the case when you specify the name of constructors (not their arguments) and the destructor.

Note also that, unlike nontemplate classes, you can’t declare or define class templates inside functions or block scope. In general, templates can only be defined in global/namespace scope or inside class declarations (see Section 12.1 on page 177 for details).

### 2.1.2 Implementation of Member Functions

To define a member function of a class template, you have to specify that it is a template, and you have to use the full type qualification of the class template. Thus, the implementation of the member function push() for type Stack<T> looks like this: Click here to view code image

```
template<typename T>
void Stack<T>::push (T const& elem)
{
  elems.push_back(elem); // append copy of passed elem
}
```

In this case, push_back() of the element vector is called, which appends the element at the end of the vector.

Note that pop_back() of a vector removes the last element but doesn’t return it. The reason for this behavior is exception safety. It is impossible to implement a completely exception-safe version of pop() that returns the removed element (this topic was first discussed by Tom Cargill in [CargillExceptionSafety] and is discussed as Item 10 in [SutterExceptional]). However, ignoring this danger, we could implement a pop() that returns the element just removed. To do this, we simply use T to declare a local variable of the element type: Click here to view code image

```
template<typename T>
T Stack<T>::pop ()
{
  assert(!elems.empty());
  T elem = elems.back(); // save copy of last element
  elems.pop_back(); // remove last element
  return elem; // return copy of saved element
}
```

Because back() (which returns the last element) and pop_back() (which removes the last element) have undefined behavior when there is no element in the vector, we decided to check whether the stack is empty. If it is empty, we assert, because it is a usage error to call pop() on an empty stack. This is also

```
stringStack.pop();
}
```

By declaring type Stack<int>, int is used as type T inside the class template. Thus, intStack is created as an object that uses a vector of ints as elements and, for all member functions that are called, code for this type is instantiated. Similarly, by declaring and using Stack<std::string>, an object that uses a vector of strings as elements is created, and for all member functions that are called, code for this type is instantiated.

Note that code is instantiated only for template (member) functions that are called. For class templates, member functions are instantiated only if they are used. This, of course, saves time and space and allows use of class templates only partially, which we will discuss in Section 2.3 on page 29.

In this example, the default constructor, push(), and top() are instantiated for both int and strings. However, pop() is instantiated only for strings. If a class template has static members, these are also instantiated once for each type for which the class template is used.

An instantiated class template’s type can be used just like any other type. You can qualify it with const or volatile or derive array and reference types from it. You can also use it as part of a type definition with typedef or using (see Section 2.8 on page 38 for details about type definitions) or use it as a type parameter when building another template type. For example: Click here to view code image

```
void foo(Stack <int> const& s) // parameter s is int stack
{
using IntStack = Stack <int>; // IntStack is another name for Stack<int>
Stack< int> istack[10]; // istack is array of 10 int stacks
IntStack istack2[10]; // istack2 is also an array of 10 int stacks (same type)
...
}
```

Template arguments may be any type, such as pointers to floats or even stacks of ints: Click here to view code image

```
Stack< float*> floatPtrStack; // stack of float pointers
Stack<Stack< int>> intStackStack; // stack of stack of ints
```

The only requirement is that any operation that is called is possible according to this type.

Note that before C++11 you had to put whitespace between the two closing template brackets: Click here to view code image
