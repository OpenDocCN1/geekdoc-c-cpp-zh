
```cpp
template <typename Type = int> // This is incorrect
```

Surprisingly, this is allowed in class templates. This is because the default argument to template functions was proposed too late to the standardization committee to accept.

## Efficiency

We have seen the usefulness of templates. One of the aims of the designers of templates is efficiency. Let us see how efficient it is to use templates. The first problem with templates is that it may bloat the code in an unexpected way.

Suppose we have the following three arrays:

```cpp
int IntArray[10];
short ShortArray[10];
char CharArray[10];
```

and the calls `GenericBubbleSort(IntArray)`, `GenericBubbleSort(ShortArray)`, `GenericBubbleSort(CharArray)`, then three distinct functions are generated. A single function with `int` as an argument can actually serve the purpose. If we have to solve a problem with such data types, it is not advisable to use template functions.

Another point to be noted is that every manipulation related to templates is done at compile time. Hence, there is almost no run-time overhead when templates are used.

## Flexibility

Flexibility is an important advantage of using function templates, which can be used for built-in as well as user-defined types. It has already been mentioned that the algorithms may need the operators to be overloaded if they are to be used with objects as parameters. Algorithms can be flexible only if proper operators are overloaded meaningfully for a given object. For example, `BubbleSort(CompArray, size)` is useful and correct only if `<` and `=` are defined.

## 7.3 Class Templates

We have seen generic functions and their uses so far. Similarly, generic classes, which take data types as parameters, are also possible in C++. It is possible to define a stack class, which has all possible functionality of a stack. The objects of the stack class can be defined as follows:

```cpp
Stack <int> MyIntStack;
```

Here, the content of the stack class is of type integer. It is also possible to have `Stack <char>`, `Stack <employee>`, etc. How can such a functionality be built? Program 7.9 uses the same stack used in Program 3.2 in Chapter 3, but now with generic type elements.

### Program 7.9 Generic stack class

```cpp
//GenericStackClass.cpp
#include <iostream>
using namespace std;
template <typename ElementType>
```

Deducing a type is not possible for class templates. We must have the type explicitly specified while defining a class.

`template <typename ElementType>` precedes the class definition for the class to use `ElementType` as a generic type in its body.

- The definition `Stack MyStack` changes to `Stack <int> MyStack`.
- The `int` element type argument to `push` and the return type of `pop` have been replaced here by `ElementType`.

It is also possible to have char Stack and employee Stack similar to the int stack. It can be observed that the program will not have any change in the Stack class definition.

It is to be noted that it is not possible to have automatic argument deduction in class templates because the compiler cannot deduce a type from the object declaration such as `Stack Mystack`. It is not similar to a function call where there are arguments and deductions that may tell a compiler the data type for the Type.

### 7.3.1 Defining Functions of Class Templates outside the Class

If the functions `push()` and `pop()` are defined outside the class, class `Stack` will have to be defined in the following way:

```cpp
template <typename ElementType>
class Stack
{
private:
    int StackPointer;
    ElementType StackArray[10];
public:
    Stack()
    {
        StackPointer = 0;
    }
    void push(ElementType);
    ElementType pop();
};
```

```cpp
template <typename ElementType>
void Stack <ElementType>::push(ElementType value)
{
    if(StackPointer == 9)
    {
        cout << "Stack overflow! Cannot insert";
    }
    else
    {
        StackArray[StackPointer] = value; StackPointer++;
    }
}
```

```cpp
template <typename ElementType>
ElementType Stack <ElementType>::pop()
{
    if(StackPointer == 0)
        cout << "Stack underflow! Cannot pop";
    else
    {
        StackPointer--;
        return StackArray[StackPointer];
    }
}
```

The syntax for the function header seems cryptic at first sight. The function header is preceded by `template <...>`, which is the same as the template specification that preceded the class definition earlier. The class name (e.g., `Stack`) should also indicate the type variables used in the class (e.g., `int`) using the same `<>` pair to indicate names, that is, `Stack <int>`. Note that the template specification contains `typename` (it has been mentioned already that it can even be the keyword `class` instead of `typename`) followed by the type variable name (e.g., `typename ElementType`). The class section will only have the type (e.g., `ElementType` in Program 7.9).

In Program 7.10, the function has been moved outside the template class and the Employee stack has been introduced.

### Program 7.10 Employee stack

```cpp
//EmpStack.cpp
#include <iostream>
#include <string>
using namespace std;

class employee
{
int EmpNo;
string Name;
string DeptName;
string Designation;
public:
employee(){};
employee(int TempNo, string TempName, string TempDept, string TempDesi)
{
EmpNo = TempNo;
Name = TempName;
DeptName = TempDept;
Designation = TempDesi;
}

friend ostream & operator <<(ostream &TempOut, employee &TempEmployee);
};

ostream & operator <<(ostream & TempOut, employee & TempEmployee)
{
TempOut << "Details of employee number" << TempEmployee.EmpNo << "\n";
TempOut << "Name is" << TempEmployee.Name << "\n";
TempOut << "Department is" << TempEmployee.DeptName << "\n";
TempOut << "Designation is" << TempEmployee.Designation << "\n";
return TempOut;
}

template <typename ElementType>
class Stack
{
private:
int StackPointer;
ElementType StackArray[10];
public:
Stack()
{
StackPointer = 0;
}
void push(ElementType);
ElementType pop();
};

template <typename ElementType>
void Stack <ElementType>::push(ElementType value)
{
if(StackPointer > 9)
{
cout << "Stack overflow! Cannot insert";
}
else
{
StackArray[StackPointer] = value; StackPointer++;
}
}

template <typename ElementType>
ElementType Stack <ElementType>::pop()
{
if(StackPointer == 0)
cout << "Stack underflow! Cannot pop";
else
{
StackPointer--;
return StackArray[StackPointer];
}
}

void main()
{
Stack <int> MyStack;
MyStack.push(1);
MyStack.push(2);
cout << MyStack.pop() << "\n";
cout << MyStack.pop() << "\n";
Stack <char> YourStack;
YourStack.push('n');
YourStack.push('o');
cout << YourStack.pop() << "\n";
cout << YourStack.pop() << "\n";
Stack <employee> EmpStack;
employee UniEmployee[10] =
{
employee(1, "Lara", "Exam", "Professor"),
employee(2, "Ponting", "Marksheet", "Clerk"),
employee(3, "Laxman", "Accounts", "Head Clerk"),
employee(4, "Flintoff", "Exam", "Clerk"),
employee(5, "Murlidharan", "Accounts", "CAO"),
employee(6, "Sarfaraz", "Exam", "Informer"),
employee(7, "Dean Jones", "Exam", "Invigilator"),
employee(8, "Madugalie", "Exam", "Examiner"),
employee(9, "Ganguly", "Marksheet", "Repeater"),
employee(10, "Nafees", "Accounts", "Clerk")
};

for(int i = 0; i < 10; i++)
{
    EmpStack.push(UniEmployee[i]);
}

for(int i = 0; i < 10; i++)
{
    cout << EmpStack.pop();
}
}
```

### How the Program Works

We will see how the real class is generated from a generic class and is used in the program.

### Constructing a class

Let us see how class stack is used as an int stack as well as a char stack. Similar to function templates, when a class template is defined, that is, when `template <typename ElementType>` is defined, it informs the compiler that the following class definition contains a generic data type called `ElementType`. This does not define the class, as no functions are generated and no elements are created. This also indicates that when the class is actually defined in the main program, the type of `ElementType` will be known.

The definition of stack in the program, `Stack <int> MyStack`, indicates that `int` is passed as a type to the template class. The compiler creates the class only when such an object is defined. It creates the integer version of `Stack` class template (known as `Stack <int>`) at that moment. It also creates an object of that class (`MyStack`). Thus, both the class and the object are created together.

### Generating the second class

When the compiler encounters `Stack <char> YourStack`, it creates another class, which is a char version of `Stack` and an object of that class (`YourStack`). This process (generating normal class from the template class) is known as instantiation. Here, it is known as class instantiation from a class template. Both `Stack <int>` and `Stack <char>` are known as specializations (instantiations). Now, if we have one more definition `Stack <char> YourStack2`, the compiler will not generate a new class, that is, it would not generate new specialization from `Stack` template as it has already instantiated `Stack <char>`. It would only create an object (`YourStack2`) of class `Stack <char>`.

### Explicit specialization

If `Stack <employee>` class is to behave differently from the `Stack` template, it can be defined as an explicit specialization as has been done with template functions.

Program 7.11 is an example of an explicit class specialization. Instead of inserting the complete employee object in the stack, the employee number of the employee object is inserted. When the element is popped, the array needs to be searched to get the employee object with the same employee number. This solution is storage efficient but will take more time to execute because of the search operation involved.

> Generating a normal class for a specific data type from a generic class is known as instantiation and the generated class is known as specialization.
