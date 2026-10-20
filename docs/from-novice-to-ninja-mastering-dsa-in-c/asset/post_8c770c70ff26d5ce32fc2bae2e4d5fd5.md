
```cpp
class Dog : public Animal {
public:
    void bark() {
        cout << "Dog is barking." << endl;
    }
};
```

In this example, Dog is a derived class that inherits the eat function from the Animal base class. This relationship allows Dog to both use the existing functionality of Animal and introduce its own unique behaviours.

Polymorphism allows objects of different types to be treated as objects of a common type. This is achieved through two mechanisms: function overloading and virtual functions.

## Function Overloading

```cpp
class Calculator {
public:
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
};
```

Here, the add function is overloaded to handle both integer and floating-point additions. The appropriate version is selected based on the types of arguments provided.

## Virtual Functions

```cpp
// Base class with a virtual function
class Shape {
public:
    virtual void draw() {
        cout << "Drawing a shape." << endl;
    }
};

// Derived class overriding the virtual function
class Circle : public Shape {
public:
    void draw() override {
        cout << "Drawing a circle." << endl;
    }
};
```

In this case, the Shape class has a virtual function draw, which is overridden by the Circle class. This allows dynamic binding, enabling the correct function to be called based on the actual type of the object.

## Benefits and Considerations

Inheritance and polymorphism promote code reuse, extensibility, and a more natural representation of real-world relationships. However, improper use of inheritance, also known as the "diamond problem" in multiple inheritance scenarios, can lead to ambiguity and maintenance challenges.

## Encapsulation and Abstraction: Securing and Simplifying Complexity

Encapsulation and abstraction are fundamental concepts in Object-Oriented Programming (OOP) that contribute to the creation of robust, modular, and easy-to-understand code. They play a crucial role in managing the complexity of software systems.

### Encapsulation: Data Hiding and Access Control

Encapsulation involves bundling the data (attributes) and methods (functions) that operate on the data into a single unit known as a class. It facilitates the concept of data hiding, where the implementation details of a class are hidden from the outside world, and access to the internal state is controlled through public interfaces.

```cpp
class BankAccount {
private:
    double balance;

public:
    // Public member functions for controlled access
    void deposit(double amount) {
        // Implementation details
        balance += amount;
    }

    void withdraw(double amount) {
        // Implementation details
        if (amount <= balance) {
            balance -= amount;
        } else {
            cout << "Insufficient funds." << endl;
        }
    }

    double getBalance() const {
        // Accessor function for read-only access
        return balance;
    }
};
```

In this example, the balance data member is private, and access to it is provided through controlled member functions like deposit, withdraw, and getBalance. This encapsulation protects the internal state and ensures that modifications to it are performed with proper validation.

### Abstraction: Managing Complexity

Abstraction involves simplifying complex systems by modelling classes based on real-world entities and focusing on essential properties and behaviours. It allows programmers to work with high-level concepts without delving into the intricate details of the implementation.

```cpp
class Shape {
public:
    // Pure virtual function for abstraction
    virtual void draw() const = 0;
};
```

In this example, the Shape class is an abstraction representing a generic shape. By declaring a pure virtual function draw, the class becomes abstract, and its derived classes (e.g., Circle, Rectangle) must provide concrete implementations. This enables high-level modelling without specifying the details of each shape until needed.

### Benefits and Considerations

Encapsulation and abstraction provide several benefits:

- **Modularity**: Encapsulation allows the creation of self-contained and modular units, making it easier to manage and maintain code.
- **Security**: Encapsulation protects the internal state of an object, preventing unintended access and modifications.
- **Flexibility**: Abstraction allows programmers to work with high-level concepts, promoting code adaptability to changing requirements.

However, it's essential to strike a balance, as overuse of abstraction can lead to overly complex class hierarchies, making the code difficult to understand.

A destructor is a special member function with the same name as the class, preceded by a tilde (~). It is called automatically when an object goes out of scope or is explicitly deleted. Destructors are crucial for releasing resources, such as freeing memory or closing files, associated with an object.

```cpp
class BankAccount {
public:
    // Constructor
    BankAccount() {
        balance = 0.0;
        cout << "BankAccount object created." << endl;
    }

    // Destructor
    ~BankAccount() {
        cout << "BankAccount object destroyed." << endl;
    }

    // Member function to display balance
    void displayBalance() {
        cout << "Balance: " << balance << endl;
    }

private:
    double balance;
};
```

In this example, the BankAccount class has a constructor that initializes the balance and a destructor that prints a message when the object is destroyed.

## Implicit and Explicit Constructor Calls

Constructors can be implicitly called when objects are created, and they can also be explicitly invoked. Explicit calls are useful in scenarios where dynamic memory allocation or additional setup is required.

```cpp
Car myCar;    // Implicit call to the default constructor
Car anotherCar("Toyota", 2022);  // Explicit call to the parameterized constructor

BankAccount* accountPtr = new BankAccount();  // Explicit dynamic object creation
delete accountPtr;  // Explicit call to the destructor
```

## Copy Constructors

A copy constructor is a special constructor that creates an object by copying the contents of another object. It is called when objects are passed by value, returned by value, or explicitly copied.

```cpp
class Student {
public:
    // Copy constructor
    Student(const Student& other) {
        this->name = other.name;
        this->age = other.age;
        cout << "Copy constructor called." << endl;
    }

    // Constructor
    Student(string name, int age) : name(name), age(age) {
        cout << "Student object created." << endl;
    }

    // Destructor
    ~Student() {
        cout << "Student object destroyed." << endl;
    }

private:
    string name;
    int age;
};
```

In this example, the Student class has a copy constructor that creates a new object by copying the data from another Student object.

## Operator Overloading: Extending the Language's Vocabulary

Operator overloading in C++ allows user-defined classes to define their behaviour for standard operators. This feature enhances the expressiveness of classes by enabling them to work seamlessly with operators, making code more intuitive and readable.

### Overloading Unary Operators

Unary operators operate on a single operand. To overload a unary operator, define a member function for the class with the operator keyword followed by the operator to be overloaded.

```cpp
class ComplexNumber {
public:
    double real;
    double imag;

    // Overloading the unary minus (-) operator
    ComplexNumber operator-() const {
        ComplexNumber result;
        result.real = -real;
        result.imag = -imag;
        return result;
    }
};
```

In this example, the unary minus operator (-) is overloaded to negate the real and imaginary parts of a complex number.

### Overloading Binary Operators

Binary operators work on two operands. To overload a binary operator, define a member function for the class with the operator keyword and two parameters.

```cpp
class Point {
public:
    double x;
    double y;

    // Overloading the binary plus (+) operator
    Point operator+(const Point& other) const {
        Point result;
        result.x = x + other.x;
        result.y = y + other.y;
        return result;
    }
};
```

In this example, the binary plus operator (+) is overloaded to add two points.

### Overloading Comparison Operators

Comparison operators (==, !=, <, >, <=, >=) can be overloaded to define custom comparison logic for user-defined types.

```cpp
class Date {
public:
    int day;
```
