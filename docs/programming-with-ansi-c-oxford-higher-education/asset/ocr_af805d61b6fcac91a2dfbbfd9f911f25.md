# PROGRAM 7.12 Using typename for unambiguously specifying a type

```
//Typename.cpp
#include <iostream>
using namespace std;

int ptr;
template <class Type>

void Min()
{
    typename Type::Test * ptr;
    // Type::Test *ptr;
    // Other code, which does not concern us here
}

class TestTypeName1
{
public:
    typedef int Test;
};

class TestTypeName2
{
public:
    typedef char Test;
};

void main()
{
    Min <TestTypeName1>();
    Min <TestTypeName2>();
}
```

# How the Program Works

Here, we have two classes, TestTypeName1 and TestTypeName2, both of which define a type Test. Min() is a function template with a single Type argument. We have called this function twice, first with the argument TestTypeName1 and the second time with TestTypeName2. When Type is instantiated by TestTypeName1, Type::Test is an integer and when Type is instantiated by TestTypeName2, it is a char. The user here wants to define a variable of type Test. This means that if TestTypeName1 is the argument, then the variable is int, and if TestTypeName2 is the argument, then the variable is char. To define that we cannot write the statement,

```
Test Variable;
```

as it would confuse the compiler that there are two different options

We need to write the following statement as it would not create any ambiguity:

```
Type::Test Variable;
```

We have to refer to it as TestTypeName1::Test if we want to have the Test data type of the first class (which is actually an int). Likewise, we have to write TestTypeName2::Test, which is actually a char, when we are referring to the type of the second class TestTypeName2. The Type contains that type, so the ambiguity no longer exists.

Note that the scope resolution operator is used here to avoid confusion about the Test we are referring to, because we have two different data types having the same name. The name we have used with the class name and the scope resolution operator is known as the qualified name.