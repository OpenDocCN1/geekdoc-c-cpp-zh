
If you define a constructor with no parameters, it is an explicit default constructor. It is also possible to define a constructor that takes parameters and still make it a default constructor using default arguments, which we will discuss in a moment.

If you define a constructor that has at least one required parameter, then the compiler will not generate a default constructor. You must define an explicit default constructor if you want one.

## Default Arguments in Function Declarations

Constructors in C++, and functions in general, can have default arguments specified for some or all of their parameters as part of their declaration (similar to C#'s optional arguments). In C++ functions, all parameters with default arguments must occur to the right of any parameter without a default argument in the function declaration. C++ does not support C-style named arguments, but you can accomplish something similar using the [named parameter idiom](#).

Why mention default arguments here? Well, it turns out that if you have a constructor in which all the parameters have default arguments, that constructor is a default constructor. It makes sense, since if you have a constructor with the signature `Vehicle(VehicleType type = VehicleType::Car, double odometerReading = 0.0);` then you can call that constructor with empty parentheses, and those default arguments will be used. If you define a default constructor, you can have only one, regardless whether it has no parameters, or whether its parameters all have default arguments.

This principle goes further still. No two functions with the same name that are declared in the same scope can have the same parameter types in exactly the same positions. You guessed it: Parameters with default arguments are disregarded for the purpose of distinct function signatures.

It all makes sense because default arguments make it impossible to distinguish between `double Add(double a, double b = 0.0);` and `double Add(double a, int b = 0);` given that both could be called as `double dbl = Add(5.0);`. The compiler cannot know which you intended in that case, so it simply fails to compile and displays an error message.

## Parameterized Constructors

A parameterized constructor has one or more parameters. A parameterized constructor where all of the parameters have default arguments is also the default constructor for a class. There is nothing special about parameterized constructors in C++.

## Conversion Constructors

A conversion constructor has at least one parameter. If there is more than one, then those additional parameters must have default arguments.

If you do not want a constructor to be a conversion constructor, you can mark it with the function specifier: explicit. Let’s look at an example:

```cpp
#include <string>

class SomeClass
{
public:
        SomeClass(const wchar_t* value) :
                m_strValue(value),
                m_intValue()
        {
        }

        explicit SomeClass(int value) :
                m_strValue(),
                m_intValue(value)
        {
        }

        ~SomeClass(void) { }

        const wchar_t* GetStringValue(void)
        {
                return m_strValue.c_str();
        }

        int GetIntValue(void) { return m_intValue; }

private:
        std::wstring        m_strValue;
        int                 m_intValue;
};

void DoSomething(void)
{
    // Normal constructor use.
    SomeClass sc1 = SomeClass(L"Hello World");

    // Fine because the const wchar_t* constructor
    // is a conversion constructor.
    SomeClass sc2 = L"Hello World";

    // Normal constructor use.
    SomeClass sc3 = SomeClass(1);

    //// Illegal since the int constructor is not a
    //// conversion constructor.
    //SomeClass sc4 = 1;

    // ...
}
```

As you can see, the conversion constructor lets us construct sc2 by directly setting it equal to a string value. The compiler sees that statement, checks to see if SomeClass has a conversion constructor that will receive the sort of value, and proceeds to call the appropriate SomeClass constructor. If we tried that with the commented-out sc4 line, the compiler would fail because we used explicit to tell the compiler that the constructor, which takes int, should not be treated as a conversion constructor, but instead should be like any other parameterized constructor.

Conversion constructors can be useful, but they can also lead to bugs. For example, you could accidentally create a new object and assign it to an existing variable when you merely mistyped a variable name and really meant an assignment. The compiler won’t complain if there is a valid conversion constructor, but will complain if there isn’t. So keep that in mind and remember to mark single parameter constructors as explicit, except when you have a good reason for providing a conversion constructor.

```cpp
        int        m_value;
};

class B : virtual public A
{
public:
        explicit B(int) :
                A(CallingMsg(L"A")),
                m_b(InitializingIntMsg(2, L"m_b")),
                m_a(InitializingIntMsg(5, L"m_a"))
        {
                wcout << L"Constructing B. m_a is " <<
                        m_a << L" and m_b is " << m_b << L"." << endl;
        }
        virtual ~B(void)
        {
                wcout << L"Destroying B." << endl;
        }

private:
        int        m_a;
        int        m_b;
};

class C
{
public:
        explicit C(int) :
                m_c(InitializingIntMsg(0, L"m_c"))
        {
                wcout << L"Constructing C. m_c is " <<
                        m_c << L"." << endl;
        }
        virtual ~C(void)
        {
                wcout << L"Destroying C." << endl;
        }

private:
        int        m_c;
};

class D
{
public:
        explicit D(int) :
                m_d(InitializingIntMsg(3, L"m_d"))
        {
                wcout << L"Constructing D. m_d is " <<
                        m_d << L"." << endl;
        }
        virtual ~D(void)
        {
                wcout << L"Destroying D." << endl;
        }

private:
```

```cpp
wcout << endl << "Break between Y and Z." << endl
     << endl;

{
        Z someZ(CallingMsg(L"Z"));
        wcout << L"Z::GetSomeInt returns " <<
        someZ.GetSomeInt() << L"." << endl;
}
return 0;
}
```

The first thing we’ve done is define two helper functions that write messages, so we can easily follow the order in which things are happening. You will notice that each of the classes has a constructor that takes int, though only Y and Z put it to use. A, B, C, and D do not even specify a name for the int in their int parameter constructors; they just specify that there is an int parameter. This is perfectly legal C++ code, and we’ve been using it all along with our custom parameter names in main.

Class A has two constructors: a default constructor and a parameterized constructor that takes an int. The remaining classes have only parameterized constructors, each of which takes an int.

- Class B inherits from A virtually.
- Class C inherits from nothing.
- Class D inherits from nothing.
- Class Y inherits from B virtually, from D directly, and from C virtually, in that order.
- Class Z also inherits from D directly, from B virtually, and from C directly, in that order.

Let’s look at the output this program gives us and then discuss what is happening and why.

```text
Calling Y constructor.
Initializing DEFAULT m_value.
DEFAULT Constructing A. m_value is '5'.
Calling B constructor.
Initializing m_a.
Initializing m_b.
Constructing B. m_a is '5' and m_b is '2'.
Calling C constructor.
Initializing m_c.
Constructing C. m_c is '0'.
Calling D constructor.
Initializing m_d.
Constructing D. m_d is '3'.
Initializing m_someInt.
Constructing Y. m_someInt is '0'.
Y::GetSomeInt returns '0'.
Destroying Y.
Destroying D.
Destroying C.
Destroying B.
Destroying A.

Break between Y and Z.

Calling Z constructor.
Calling A constructor.
Initializing m_value.
Constructing A. m_value is '20'.
Calling B constructor.
Initializing m_a.
Initializing m_b.
Constructing B. m_a is '5' and m_b is '2'.
Calling D constructor.
Initializing m_d.
Constructing D. m_d is '3'.
Calling C constructor.
Initializing m_c.
Constructing C. m_c is '0'.
Initializing m_someInt.
Constructing Z. m_someInt is '0'.
Z::GetSomeInt returns '0'.
Destroying Z.
Destroying C.
Destroying D.
Destroying B.
Destroying A.
```

In our main function, first we create an object of type Y within its own scope. We then call its GetSomeInt member function. This helps ensure that the compiler will not optimize away the creation of Y in a release build in case you mess around with the code. It also serves as a marker between construction and destruction.

We then exit the scope of Y, triggering its destruction. After this, we write another marker string to separate the instantiation of a Y instance from the instantiation of the Z instance that follows. We create the Z instance in its own scope so we can follow its construction and destruction the same way as with Y.

So what do we see? Quite a lot. Let's focus on Y first.

When we call the Y constructor, the first thing it does is call the default constructor for A. This might seem terribly wrong for several reasons, but it is, in fact, right. The Y constructor says to follow this order:

1. Initialize base class C.
2. Initialize Y's member variable m_someInt.
3. Initialize base class D.
4. Initialize base class B.

Instead, we wind up with this order:

1. Initialize base class A via its default constructor.
2. Initialize base class B.
3. Initialize base class C.
4. Initialize base class D.
5. Initialize Y's member variable m_someInt.

Since we know B inherits virtually from A, and that B is the only source of inheritance from A, we can conclude that B is given priority over the others and that A is given priority over B.
