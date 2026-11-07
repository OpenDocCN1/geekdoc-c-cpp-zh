
functions) of the derived class through the public or protected members of the base class.

- 21. In a public inheritance, the public members of the base class are public members of the derived class. They can be accessed by the member functions (and friend functions) of the derived class. The protected members of the base class are protected members of the derived class. They can be accessed by the member functions (and friend functions) of the derived class. The private members of the base class are hidden in the derived class. They cannot be directly accessed in the derived class. They can be accessed by the member functions (and friend functions) of the derived class through the public or protected members of the derived class.

- 23. The protected members of a base class can be directly accessed by the member functions of the derived class, but they cannot be directly accessed in a program that uses that class. The public members of a class can be directly accessed by the member functions of any derived class as well as in a program that uses that class.

- 25. 
  a. 
```cpp
class yourClass: protected base
{
}
```

  b. The members setXYZ, setX, getX, setY, getY, mystryNum, and print, z, setZ, and secret are protected members of the class yourClass. The private members x and y of the class base are hidden in class yourClass and they can be accessed in class yourClass only through the protected and public members of class base.

- 27. 
  a. Because the memberAccessSpecifier is not specified, it is a private inheritance.

  b. All members of the class base become private members in class derived.

- 29. 
  a.

```cpp
void base::print() const
{
    cout << "num = " << num << ", x = " << x;
}

double base::compute(int n)
{
    return n + manipulate(n, n);
}

double base::manipulate(int a, int b)
{
    return num * a + x * b;
}
```

```cpp
cout << "Perimeter: " << 2 * (*length + *width) << endl;
Output: Area: 19.50, Perimeter: 19.00
```

- 13. Trip total cost: $550.00

- Highest trip cost: $275.00

- 15. In Line 6, the operator `delete` deallocates the memory space to which `nextPtr` points. So the expression `*nextPtr`, in Line 9, does not have a valid value.

- 17. 12 37 78 62 62 13

- 19. `numPtr = 1058` and `gpaPtr = 2024`

- 21. The operator `delete` deallocates the memory space to which a pointer points.

- 23. 
  a. `sales = new double[50];`

  b.
```cpp
for (int i = 0; i < 50; i++)
    cin >> sales[i];
```

  c.
```cpp
int maxIndex = 0;
for (int i = 1; i < 50; i++)
    if (sales[maxIndex] < sales[i])
        maxIndex = i;
```

  d. `delete [] sales;`

- 25. Because at compile time dynamic arrays have no first and last elements, the functions `begin` and `end` cannot be called on dynamic arrays.

- 27. In a shallow copy of data, two or more pointers point to the same memory space. In a deep copy of data, each pointer has its own copy of the data.

- 29.
```cpp
int *myList;
int *yourList;

myList = new int[5];
myList[0] = 8;
for (int i = 1; i < 5; i++)
    myList[i] = i * myList[i - 1];

yourList = new int[5];
for (int i = 0; i < 5; i++)
    yourList[i] = 2 * myList[i];
```

- 31. The copy constructor makes a copy of the actual variable.

- 33. Classes with pointer data members should include the destructor, overload the assignment operator, and explicitly provide the copy constructor by including it in the class definition and providing its definition.

- 35. 5

```text
small: --
x: 2, y = 3
*-*-*-*-*-*-*-*-*-*-*

17
small: --
x: 3, y = 5
noSmall-- z: 9
```

- 37. Yes.

- 39. 
  a. Because `employeeType` is an abstract class, you cannot instantiate an object of this class. Therefore, this statement is illegal.

  b. This statement is legal.

  c. This statement is legal.

## Chapter 13

- 1. a. true; b. false; c. true; d. false; e. false; f. false; g. false; h. false; i. true; j. false; k. false; l. true; m. true

- 3. b

- 5. A friend function of a class is a nonmember function of the class, but has access to all the members (public or non-public) of the class.

- 7. d; Because the left operand of `<<` is a stream object, which is not of the user-defined class type.

- 9. a. One; b. Two

- 11. `object1.operator+(object2)`

- 13. a. bool; b. bool

- 15. 
  a.
```cpp
friend strange operator+(const strange&,
                          const strange&);
```

  b.
```cpp
friend bool operator==(const strange&,
                       const strange&);
```

  c.
```cpp
friend strange operator++(strange&, int);
```

- 17. In Line 4, the formal parameter of the function `operator+` should be of type `myClass`. The correct statement is

```cpp
myClass operator+(const myClass& obj);  // Line 4
```

- 19. In Line 3, the return type of the function `operator<` should be bool. The correct statement is

```cpp
friend bool operator<(const mystery& a,
                      const mystery& b);  // Line 3
```

In Lines 3 and 10, the return type of the function `operator*` should be `findErrors`. In Line 3, the type of the objects `a` and `b` must be `findErrors`. Also, since `operator*` is a friend function of the class, the name of the class and the scope resolution operator in the heading of the function, in Line 10, are not needed. In Lines 13 and 14, to access the instance variables of the object `a`, we need to use the object `a` and the dot operator. The correct statements are as follows:

```cpp
friend findErrors operator*(const findErrors& a,
                             const findErrors& b);    // Line 3
findErrors operator*(const findErrors& a,
                     const findErrors& b)             // Line 10

temp.first = a.first * b.first;                       // Line 13
temp.second = a.second * b.second;                    // Line 14
```

A reference to an object of the class `istream`.

The function that overloads the pre-increment operator has no parameter, while the function that overloads the post-increment operator has one (dummy) parameter.

- 27. a. None; b. One

```cpp
class complexType
{
    // overload the stream insertion and extraction operators
    friend ostream& operator<<(ostream&, const complexType&);
    friend istream& operator>>(istream&, complexType&);

public:
    void setComplex(const double& real, const double& imag);
    // set the complex number according to the parameters
    // Postcondition: realPart = real; imaginaryPart = imag

    complexType(double real = 0, double imag = 0);
    // constructor
    // initialize the complex number according to the parameters
    // Postcondition: realPart = real; imaginaryPart = imag

    complexType operator+(const complexType&
                          otherComplex) const;
    // overload +
    complexType operator*(const complexType&
                          otherComplex) const;
    // overload *

    complexType operator~() const;

    double operator!() const;

    bool operator==(const complexType& otherComplex) const;
    // overload ==
};
```

```cpp
private:
    double realPart;          // variable to store the real part
    double imaginaryPart;     // variable to store the imaginary part
};

// Definitions of operator- and operator!
complexType complexType::operator-() const
{
    complexType temp = *this;

    temp.imaginaryPart = -temp.imaginaryPart;

    return temp;
}

double complexType::operator!() const
{
    return (pow((realPart * realPart +
                 imaginaryPart * imaginaryPart), 0.5));
}
```

- 31. When the class has pointer data members.

- 33. Error in Line 4. A template instantiation can be for only a built-in type or a user-defined type. The word “type” between the angle brackets must be replaced either with a built-in type or a user-defined type.

- 35. a. 12; b. Sunny Day

- 37.
```cpp
template <class Type>
void swap(Type &x, Type &y)
{
    Type temp;
    temp = x;
    x = y;
    y = temp;
}
```

- 39. These statements generate and output a random integer between 10 and 25.

## Chapter 14

- 1. a. false; b. true; c. true; d. false; e. true; f. false; g. false; h. true; i. false; j. true; k. false; l. true; m. false

- 3. The program will terminate with an error message.

- 5. At most one.
