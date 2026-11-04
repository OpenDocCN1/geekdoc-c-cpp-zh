
```cpp
int main() {
    LinkedList list;
    list.insert(10);
    list.insert(20);
    list.insert(30);
    list.insert(40);
    
    std::cout << "Original list: ";
    list.display();
    
    list.remove(20);
    list.remove(30);
    
    std::cout << "List after removals: ";
    list.display();
    return 0;
}
```

## Step 5: Implement the Constructor and Methods

Implement the constructor and methods of the `LinkedList` class:

```cpp
LinkedList::LinkedList() {
    head = nullptr;
}

void LinkedList::insert(int value) {
    Node* newNode = new Node;
    newNode->data = value;
    newNode->next = head;
    head = newNode;
}

void LinkedList::remove(int value) {
    if (head == nullptr) {
        return;
    }

    if (head->data == value) {
        Node* temp = head;
        head = head->next;
        delete temp;
        return;
    }

    Node* current = head;
    while (current->next != nullptr &&
    current->next->data != value) {
        current = current->next;
    }

    if (current->next != nullptr) {
        Node* temp = current->next;
        current->next = temp->next;
        delete temp;
    }
}

void LinkedList::display() {
    Node* current = head;
    while (current != nullptr) {
        std::cout << current->data << " ";
        current = current->next;
    }
    std::cout << std::endl;
}
```

## Step 6: Create the Main Program

Write the `main` function to test the `LinkedList` class:

```cpp
int main() {
    LinkedList list;

    list.insert(10);
    list.insert(20);
    list.insert(30);
    list.insert(40);

    std::cout << "Original list: ";
    list.display();

    list.remove(20);
    list.remove(30);

    std::cout << "List after removals: ";
    list.display();

    return 0;
}
```

## Step 7: Compile and Run

Compile your source file using your C++ compiler. If you're using the command line, navigate to the directory containing your source file and run the command:

```
g++ -o linked_list linked_list.cpp
```

Then run the compiled executable:

```
./linked_list
```

## Step 8: Observe Output

You should see the program outputting the original linked list and the list after removals.

Congratulations! You've successfully created a C++ program that implements a singly linked list data structure with methods to insert, delete, and display elements.

## Exercise 7: Polymorphic Shapes

Create a base class `Shape` with virtual methods to calculate area and perimeter. Derive classes like `Rectangle`, `Circle`, and `Triangle`. Calculate and display area and perimeter for objects of each shape.

Here's a step-by-step guide to creating a C++ program that implements a polymorphic shapes scenario with a base class `Shape` and derived classes `Rectangle`, `Circle`, and `Triangle`: Step 1: Set Up Your Development Environment

Ensure you have a C++ compiler and a text editor or an Integrated Development Environment (IDE) installed on your computer.

### Step 2: Create a New C++ Source File

Open your preferred text editor or IDE and create a new C++ source file. Save the file with a `.cpp` extension, such as `polymorphic_shapes.cpp`.

### Step 3: Define the Base Class `Shape`

Define the `Shape` class with virtual methods to calculate the area and perimeter:

```cpp
class Shape {
public:
    virtual double calculateArea() const = 0;
    virtual double calculatePerimeter() const = 0;
};
```

### Step 4: Create Derived Classes

Create derived classes `Rectangle`, `Circle`, and `Triangle`, each implementing the virtual methods:

```cpp
        double calculatePerimeter() const override {
            return 2 * 3.14159 * radius;
        }
};

class Triangle : public Shape {
private:
    double sideA, sideB, sideC;

public:
    Triangle(double a, double b, double c) : sideA(a), sideB(b), sideC(c) {}

    double calculateArea() const override {
        // Calculate area using Heron's formula
        double s = (sideA + sideB + sideC) / 2;
        return sqrt(s * (s - sideA) * (s - sideB) * (s - sideC));
    }

    double calculatePerimeter() const override {
        return sideA + sideB + sideC;
    }
};
```

```cpp
class Rectangle : public Shape {
private:
    double width;
    double height;

public:
    Rectangle(double w, double h) : width(w), height(h) {}

    double calculateArea() const override {
        return width * height;
    }

    double calculatePerimeter() const override {
        return 2 * (width + height);
    }
};

class Circle : public Shape {
private:
    double radius;

public:
    Circle(double r) : radius(r) {}
```

Write a command-line calculator program that accepts mathematical expressions as input and evaluates them using appropriate precedence rules.

Here's a step-by-step guide to creating a C++ command-line calculator program that accepts mathematical expressions as input and evaluates them using appropriate precedence rules:

### Step 1: Set Up Your Development Environment

Ensure you have a C++ compiler and a text editor or an Integrated Development Environment (IDE) installed on your computer.

### Step 2: Create a New C++ Source File

Open your preferred text editor or IDE and create a new C++ source file.
Save the file with a `.cpp` extension, such as `calculator.cpp`.

### Step 3: Include Necessary Headers

Include the necessary header for input and output operations:

```cpp
#include <iostream>
#include <stack>
#include <sstream>
#include <cctype>
#include <cmath>
```

### Step 4: Create Helper Functions

Define helper functions to check if a character is an operator and to calculate the result of an operation:

```c
bool isOperator(char c) {
    return c == '+' || c == '-' || c == '*' || c == '/';
}

double calculate(double a, double b, char op) {
    switch (op) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/': return a / b;
        default: return 0.0;
    }
}
```

### Step 5: Create the Main Program

Write the `main` function to accept input and evaluate the mathematical expression:

```cpp
int main() {
    std::string expression;
    std::cout << "Enter a mathematical
expression: ";
    std::getline(std::cin,
expression);

    std::stack<double> values;
    std::stack<char> operators;

    std::istringstream
input(expression);
    char current;

    while (input >> current) {
        if (std::isdigit(current)) {
            double value;
            input.putback(current);
            input >> value;
            values.push(value);
        } else if
(isOperator(current)) {
            while (!operators.empty()
&& isOperator(operators.top())) {
                char op =
operators.top();
                operators.pop();
                double b =
values.top();
                values.pop();
                double a =
values.top();
                values.pop();
                values.push(calculate(a, b, op));
            }
            operators.push(current);
        }
    }

    while (!operators.empty()) {
        char op = operators.top();
        operators.pop();
        double b = values.top();
        values.pop();
        double a = values.top();
        values.pop();
        values.push(calculate(a, b,
op));
    }
```

### Step 6: Compile and Run

Compile your source file using your C++ compiler. If you're using the command line, navigate to the directory containing your source file and run the command:

```
g++ -o calculator calculator.cpp
```

Then run the compiled executable:

```
./calculator
```

### Step 7: Enter Expression

Enter a mathematical expression using appropriate operators and operands. For example:

```
Enter a mathematical expression: 3 + 4 * 2 / ( 1 - 5 ) ^ 2
```

### Step 8: Observe Output

You should see the program outputting the result of the evaluated expression.

Congratulations! You've successfully created a C++ command-line calculator program that evaluates mathematical expressions using appropriate precedence rules.

## Exercise 9: Template Stack

Implement a generic stack using templates in C++. Test the stack with different data types such as integers, doubles, and strings.
