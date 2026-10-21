
## 7.2.3 Instantiation

When a compiler can unambiguously deduce the argument, a user may leave the <> section while calling a template function.

```cpp
GenericBubbleSort(Array4);
/* Here, the arguments are deduced by the compiler */
```

In this statement, the middle section is missing. Here, the compiler can unambiguously deduce the arguments to be float and can generate and call a float version of the function.

Thus, although the program has only a single GenericBubbleSort() function, yet three calls have been made with different types. This is the advantage of using function templates.

When a real function for a specific type is generated from the generic function definition, it is called instantiation of that generic function.

Let us now discuss how GenericBubbleSort() works with all the three data types. The template that is defined is not actually a function. The definition of the GenericBubbleSort() given earlier does not define any function in the true sense.

The function definition is generated when statements such as the following are encountered.

```cpp
// Create char instance
GenericBubbleSort <char> (Array3);

// Create int instance
GenericBubbleSort <int> (Array2);

// Deduce float and generate float instance
GenericBubbleSort(Array4);
```

This is different from a normal function such as the BubbleSort(). When a normal function definition is encountered in the program, the function is generated even if it is not called in the program. However, the template functions are not defined when the template is defined. When a template function such as GenericBubbleSort <int> is called for the first time, the following happens:

1. The function is generated, that is, instantiated from the template definition for the respective type, that is, int.
2. The call statement is compiled.

What happens when the following statements are encountered in a program?

```cpp
GenericBubbleSort <char> (Array3);
GenericBubbleSort <char> (Array5);
```

The first call (Array3) compilation process generates the function from the template. Then, it compiles the call statement. The second call does not require the generation of function as it is already instantiated. It would only compile the call statement.

> Note The difference between a normal function and an instantiated function is that the normal function is generated when the function definition is compiled, whereas the instantiated function comes into existence when the first function call is compiled.

It is also possible that multiple copies of the same function are instantiated if they are called in different files. We will look at this issue when we discuss compilation models in Section 7.4.

```cpp
string DeptName;
string Designation;
public:
    employee(int TempNo = 0, string TempName = 0, string TempDept = 0, string TempDesi = 0)
    {
        EmpNo = TempNo;
        Name = TempName;
        DeptName = TempDept;
        Designation = TempDesi;
    }
    bool operator <(employee & OtherEmployee)
    {
        if(EmpNo > OtherEmployee.EmpNo)
            return false;
        else
            return true;
    }
    friend ostream & operator <<(ostream & TempOut, employee & TempEmployee);
};

ostream & operator <<(ostream & TempOut, employee & TempEmployee)
{
    TempOut << "Details of employee number" << TempEmployee.EmpNo << "\n";
    TempOut << "Name is" << TempEmployee.Name << "\n";
    TempOut << "Department is" << TempEmployee.DeptName << "\n";
    TempOut << "Designation is" << TempEmployee.Designation << "\n";
    return TempOut;
}

template <typename Type>
void GenericBubbleSort(Type TempGenericArray[])
{
    for(int i = 0; i < 9; i++)
    {
        for(int j = i + 1; j < 10; j++)
        {
            if(TempGenericArray[i] < TempGenericArray[j])
            {
                Type TempGeneric = TempGenericArray[i];
                TempGenericArray[i] = TempGenericArray[j];
                TempGenericArray[j] = TempGeneric;
            }
        }
    }
}

void main()
{
    employee UniEmployee[10] =
    {
        employee(1, "Lara", "Exam", "Professor"),
        employee(2, "Ponting", "Marksheet", "Clerk"),
        employee(3, "Laxman", "Accounts", "Head Clerk"),
        employee(4, "Flintoff", "Exam", "Clerk"),
        employee(5, "Murlidharan", "Accounts", "CAO"),
        employee(6, "Sarfaraz", "Exam", "Informer"),
        employee(7, "Dean Jones", "Exam", "Invigilator"),
        employee(8, "Madugalle", "Exam", "Examiner"),
        employee(9, "Ganguly", "Marksheet", "Repeater"),
        employee(10, "Nafees", "Accounts", "Clerk")
    };
    GenericBubbleSort <employee> (UniEmployee);
    for(int i = 0; i < 10; i++)
    {
        cout << " " << UniEmployee[i] << ", ";
    }
}
```

### How the Program Works

We will explore only one important point in this section. The GenericBubbleSort() does not change at all. Why? Let us see.

The advantage of the generic sort is that it does not depend on the type of data sent to it. If proper operator overloading is provided, GenericBubbleSort() can work for any data type, even for user-defined objects. Such algorithms can prove to be very useful when one needs to work with multiple data types. STL contains many such algorithms.

It is important to note that the meaning of < for the bubbleSort must be preserved. Semantics (i.e., the meaning) of < here is that the left-hand side (LHS) of the '<' operator must be logically less than the right-hand side (RHS). This is done by defining the employee with the smaller ID value to be logically less than one with the greater ID value. This may be acceptable in some cases, but does not always hold good.

### Dealing with built-in types

Sometimes, operator overloading is not possible. For example, when dealing with a built-in data type where overloading an operator is out of question or with a class designed by others where one may not have an access to that class. Program 7.3 is an example that illustrates the problem with built-in C-type string.

In this program, a max function has been defined to find the maximum of the two values passed to it. Three different instantiations are generated from the template. Observe what happens when the Max function is called.

### PROGRAM 7.3 Finding the maximum of two generic arguments

```cpp
//SemanticIn00.cpp
#include <iostream>
#include <string>
using namespace std;

template <typename T>
bool Max(T First, T Second)
{
    return(First > Second);
}

int main()
{
    string sAddress = "West Indies";
    string sName = "Brian Charles Lara";
    int i1 = 5;
    int i2 = 7;
    char cAddress[] = "West Indies";
    char cName[] = "Brian Charles Lara";

    // Instance 1
    if(Max(i1, i2))
        cout << "i1 is bigger\n";
    else
        cout << "i2 is bigger\n";

    // Instance 2
    if(Max(sName, sAddress))
        cout << "sName is bigger\n";
    else
        cout << "sAddress is bigger\n";

    // Instance 3
    if(Max(cName, cAddress))
        cout << "cName is bigger\n";
    else
        cout << "cAddress is bigger\n";
}
```

Output

```text
i2 is bigger
sAddress is bigger
cName is bigger
```

> Note Strings are compared in a lexicographical manner. Thus, West Indies is bigger than Brian Charles Lara, as 'B' appears before 'W' in the dictionary. This holds true even when the number of characters in the second string is more than that of the first one.

### How the Program Works

The output is surprising. The comparison of the two strings yields the correct output but the comparison of two character arrays does not. Why? cName and cAddress are the names of the character arrays and are pointers to the first elements of the respective array. When they both are compared, the pointer value, that is, the address is compared; so, the item defined next becomes larger. Hence, cName, which is defined after cAddress, gets a larger address value. On the contrary, the < operator is overloaded in string class, and hence the behaviour there is more meaningful. The < operator yields true if the string on the LHS is lexically smaller than that on the RHS; otherwise, it returns false.

How can this problem be solved? If there is a class, it can be solved by providing an appropriate operator overloading to eliminate this. Unfortunately, that is not possible if the type is built-in (such as C-type arrays) or if the class is defined by others (where the source code is not available to modify the class). The answer to this problem is to overload the template itself for that particular type. We will see an improved version of this program using this solution in Program 7.8.

## 7.2.6 Function Templates with Multiple Arguments

It is possible to have templates with more than one argument. Other arguments can be generic or normal. Program 7.4 is a simple search program for searching an element in the array. Here, we need to pass two arguments, the array and the element to be searched, both of which are bound to be of generic type.
