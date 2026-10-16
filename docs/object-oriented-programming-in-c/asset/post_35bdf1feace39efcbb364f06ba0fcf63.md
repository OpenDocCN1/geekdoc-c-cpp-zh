
```
int len;        // length of string
public:
    .....        // member functions
    .....        // to initialize and
    .....        // manipulate strings
};
```

We shall consider an example to illustrate the application of overloaded operators to strings. The example shown in Program 7.4 overloads two operators, + and <= just to show how they are implemented. This can be extended to cover other operators as well.

## MATHEMATICAL OPERATIONS ON STRINGS

```
#include <string.h>
#include <iostream.h>

class string
{
    char *p;
    int len;
public:
    string() {len = 0; p = 0;}                // create null string
    string(const char * s);                  // create string from arrays
    string(const string & s);                // copy constructor
    ~ string(){delete p;}                    // destructor

    // + operator
    friend string operator+(const string &s, const string &t);

    // <= operator
    friend int operator<=(const string &s, const string &t);
    friend void show(const string s);
};
string :: string(const char *s)
{
    len = strlen(s);
    p   = new char[len+1];
    strcpy(p,s);
}

string :: string(const string & s)
{
    len = s.len;
    p   = new char[len+1];
    strcpy(p,s.p);
}
```

```
// overloading + operator
string operator+(const string &s, const string &t)
{
    string temp;
    temp.len = s.len + t.len;
    temp.p = new char[temp.len+1];
    strcpy(temp.p,s.p);
    strcat(temp.p,t.p);
    return(temp);
}
// overloading <= operator
int operator<=(const string &s, const string &t)
{
    int m = strlen(s.p);
    int n = strlen(t.p);
    if(m <= n) return(1);
    else return(0);
}
void show(const string s)
{
    cout << s.p;
}

int main()
{
    string s1 = "New ";
    string s2 = "York";
    string s3 = "Delhi";
    string t1,t2,t3;
    t1 = s1;
    t2 = s2;
    t3 = s1+s3;
    cout << "\nt1 = "; show(t1);
    cout << "\nt2 = "; show(t2);
    cout << "\n";
    cout << "\nt3 = "; show(t3);
    cout << "\n\n";
```

```
if(t1 <= t3)
{
    show(t1);
    cout << " smaller than ";
    show(t3);
    cout << "\n";
}
else
{
    show(t3);
    cout << " smaller than ";
    show(t1);
    cout << "\n";
}

return 0;
}
```

The following is the output of Program 7.4

t1 = New
t2 = York

t3 = New Delhi

New smaller than New Delhi

## 7.7 Rules for Overloading Operators

Although it looks simple to redefine the operators, there are certain restrictions and limitations in overloading them. Some of them are listed below:

- 1. Only existing operators can be overloaded. New operators cannot be created.
- 2. The overloaded operator must have at least one operand that is of user-defined type.
- 3. We cannot change the basic meaning of an operator. That is to say, we cannot redefine the plus(+) operator to subtract one value from the other.
- 4. Overloaded operators follow the syntax rules of the original operators. They cannot be overridden.
- 5. There are some operators that cannot be overloaded. (See Table 7.1.)
- 6. We cannot use friend functions to overload certain operators. (See Table 7.2.) However, member functions can be used to overload them.
- 7. Unary operators, overloaded by means of a member function, take no explicit arguments and return no explicit values, but, those overloaded by means of a friend function, take one reference argument (the object of the relevant class).
- 8. Binary operators overloaded through a member function take one explicit argument and those which are overloaded through a friend function take two explicit arguments.
- 9. When using binary operators overloaded through a member function, the left hand operand must be an object of the relevant class.
- 10. Binary arithmetic operators such as +, -, *, and / must explicitly return a value. They must not attempt to change their own arguments.

### Table 7.1 Operators that cannot be overloaded

|  |  |
|---|---|
| Sizeof | Size of operator |
| . | Membership operator |
| .* | Pointer-to-member operator |
| :: | Scope resolution operator |
| ?: | Conditional operator |

### Table 7.2 Where a friend cannot be used

|  |  |
|---|---|
| = | Assignment operator |
| () | Function call operator |
| [] | Subscripting operator |
| -> | Class member access operator |

## 7.8 Type Conversions

We know that when constants and variables of different types are mixed in an expression, C applies automatic type conversion to the operands as per certain rules. Similarly, an assignment operation also causes the automatic type conversion. The type of data to the right of an assignment operator is automatically converted to the type of the variable on the left. For example, the statements

```
int m;
float x = 3.14159;
m = x;
```

convert x to an integer before its value is assigned to m. Thus, the fractional part is truncated. The type conversions are automatic as long as the data types involved are built-in types.

What happens when they are user-defined data types?

Consider the following statement that adds two objects and then assigns the result to a third object.

```
v3 = v1 + v2;        // v1, v2 and v3 are class type objects
```

When the objects are of the same class type, the operations of addition and assignment are carried out smoothly and the compiler does not make any complaints. We have seen, in the case of class objects, that the values of all the data members of the right-hand object are simply copied into the corresponding members of the object on the left-hand. What if one of the operands is an object and the other is a built-in type variable? Or, what if they belong to two different classes?

Since the user-defined data types are designed by us to suit our requirements, the compiler does not support automatic type conversions for such data types. We must, therefore, design the conversion routines by ourselves, if such operations are required.

Three types of situations might arise in the data conversion between incompatible types:

- 1. Conversion from basic type to class type.
- 2. Conversion from class type to basic type.
- 3. Conversion from one class type to another class type.

We shall discuss all the three cases in detail.

### Basic to Class Type

The conversion from basic type to class type is easy to accomplish. It may be recalled that the use of constructors was illustrated in a number of examples to initialize objects. For example, a constructor was used to build a vector object from an int type array. Similarly, we used another constructor to build a string type object from a char* type variable. These are all examples where constructors perform a defacto type conversion from the argument's type to the constructor's class type.

Consider the following constructor:

```
string :: string(char *a)
{
    length = strlen(a);
    P = new char[length+1];
    strcpy(P,a);
}
```

This constructor builds a string type object from a char* type variable a. The variables length and p are data members of the class string. Once this constructor has been defined

where V1 is an object of type vector. Both the statements have exactly the same effect. When the compiler encounters a statement that requires the conversion of a class type to a basic type, it quietly calls the casting operator function to do the job.

The casting operator function should satisfy the following conditions:

- It must be a class member.
- It must not specify a return type.
- It must not have any arguments.

Since it is a member function, it is invoked by the object and, therefore, the values used for conversion inside the function belong to the object that invoked the function. This means that the function does not need an argument.

In the string example described in the previous section, we can do the conversion from string to char* as follows:

```
string :: operator char*()
{
    return(p);
}
```

### One Class to Another Class Type

We have just seen data conversion techniques from a basic to class type and a class to basic type. But there are situations where we would like to convert one class type data to another class type.

Example:

```
objX = objY;    // objects of different types
```

objX is an object of class X and objY is an object of class Y. The class Y type data is converted to the class X type data and the converted value is assigned to the objX. Since the conversion takes place from class Y to class X, Y is known as the source class and X is known as the destination class.

Such conversions between objects of different classes can be carried out by either a constructor or a conversion function. The compiler treats them the same way. Then, how do we decide which form to use? It depends upon where we want the type-conversion function to be located in the source class or in the destination class.

We know that the casting operator function

```
operator typename()
```
