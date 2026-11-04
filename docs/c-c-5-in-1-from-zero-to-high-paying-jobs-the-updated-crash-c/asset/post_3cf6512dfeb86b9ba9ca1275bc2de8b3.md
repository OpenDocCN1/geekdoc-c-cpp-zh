
Save your source file and compile it using your C++ compiler. If you're using the command line, navigate to the directory containing your source file and run the command:

```
g++ -o basic_calculator basic_calculator.cpp
```

Then run the compiled executable:

```
./basic_calculator
```

### Step 10: Input and Output

Enter two numbers when prompted and observe the program displaying the sum, difference, product, and quotient of those numbers.

Congratulations! You've successfully created a basic C++ program that performs arithmetic operations on user-input numbers.

```
#include <iostream>
#include "student.h" // Include the header file

void Student::SetDetails(std::string n, int a, char g) {
    name = n;
    age = a;
    grade = g;
}

void Student::DisplayDetails() {
    std::cout << "Name: " << name << std::endl;
    std::cout << "Age: " << age << std::endl;
    std::cout << "Grade: " << grade << std::endl;
}
```

### Step 5: Create the Main Program

In another source file (such as `main.cpp`), include the header file for the `Student` class and create a `main` function to test the class:

```
#include <iostream>
#include "student.h" // Include the header file

int main() {
    Student student1; // Create an instance of Student

    // Set details using the SetDetails method
    student1.SetDetails("Alice", 18, 'A');

    // Display the details using the DisplayDetails method
    std::cout << "Student Details:" << std::endl;
    student1.DisplayDetails();

    return 0;
}
```

### Step 6: Compile and Run

You should see the program outputting the student's details:

```
Student Details:
Name: Alice
Age: 18
Grade: A
```

Congratulations! You've successfully implemented the `Student` class with methods to set and display student details using object-oriented programming in C++.

## Exercise 3: File Handling

Write a program that reads data from a text file containing a list of numbers and calculates their average.

### Step 1: Set Up Your Development Environment

Ensure you have a C++ compiler and a text editor or an Integrated Development Environment (IDE) installed on your computer.

### Step 2: Create a New C++ Source File

Open your preferred text editor or IDE and create a new C++ source file.
Save the file with a `.cpp` extension, such as `average_calculator.cpp`.

### Step 3: Include Necessary Headers

Include the necessary header for input and output operations:

```
#include <iostream>
#include <fstream> // For file handling
```

### Step 4: Create the Main Program

Write the `main` function to read data from a text file and calculate the average:

```
int main() {
    std::ifstream inputFile("numbers.txt"); // Open the file
    double sum = 0.0;
    int count = 0;
    double number;

    if (!inputFile) {
        std::cerr << "Error opening file." << std::endl;
        return 1;
    }

    while (inputFile >> number) {
        sum += number;
        count++;
    }

    inputFile.close(); // Close the file

    if (count > 0) {
        double average = sum / count;
        std::cout << "Average: " << average << std::endl;
    } else {
        std::cout << "No numbers found in the file." << std::endl;
    }

    return 0;
}
```

### Step 5: Prepare the Input File

Create a text file named `numbers.txt` in the same directory as your source file. Fill the file with a list of numbers, one per line.

For example:

```
10.5
20.7
15.0
```

### Step 6: Compile and Run

Compile your source file using your C++ compiler. If you're using the command line, navigate to the directory containing your source file and run the command:

```
g++ -o average_calculator average_calculator.cpp
```

Then run the compiled executable:

```
./average_calculator
```

### Step 7: Observe Output

You should see the program outputting the calculated average based on the numbers in the `numbers.txt` file.

Congratulations! You've successfully created a C++ program that reads data from a text file and calculates the average of the numbers.

## Exercise 4: Templates and Functions

Implement a generic function template that finds the maximum element in an array of any data type.

### Step 1: Set Up Your Development Environment

Ensure you have a C++ compiler and a text editor or an Integrated Development Environment (IDE) installed on your computer.

### Step 2: Create a New C++ Source File

Open your preferred text editor or IDE and create a new C++ source file.
Save the file with a `.cpp` extension, such as `max_finder.cpp`.

### Step 3: Define the Generic Function Template

Define a generic function template that takes an array and its size as arguments and returns the maximum element:

```cpp
template <typename T>
T FindMax(const T arr[], int size) {
    T maxElement = arr[0];
    for (int i = 1; i < size; ++i) {
        if (arr[i] > maxElement) {
            maxElement = arr[i];
        }
    }
    return maxElement;
}
```

### Step 4: Create the Main Program

Write the `main` function to test the `FindMax` function template:

```
int main() {
    int intArray[] = {10, 3, 27, 5, 14};
    double doubleArray[] = {3.14, 1.618, 2.718, 0.577};

    int intMax = FindMax(intArray, 5);
    double doubleMax = FindMax(doubleArray, 4);

    std::cout << "Max integer: " << intMax << std::endl;
    std::cout << "Max double: " << doubleMax << std::endl;

    return 0;
}
```

### Step 5: Compile and Run

Compile your source file using your C++ compiler. If you're using the command line, navigate to the directory containing your source file and run the command:

```
g++ -o max_finder max_finder.cpp
```

Then run the compiled executable:

```
./max_finder
```

### Step 6: Observe Output

You should see the program outputting the maximum integer and maximum double values from the arrays.

Congratulations! You've successfully created a C++ program that implements a generic function template to find the maximum element in an array of any data type.

## Exercise 5: Exception Handling

Write a program that takes user input for dividing two numbers and handles exceptions for divide-by-zero and invalid input.

### Step 1: Set Up Your Development Environment

Ensure you have a C++ compiler and a text editor or an Integrated Development Environment (IDE) installed on your computer.

### Step 2: Create a New C++ Source File

Open your preferred text editor or IDE and create a new C++ source file.
Save the file with a `.cpp` extension, such as `divide_numbers.cpp`.

### Step 3: Include Necessary Headers

Include the necessary header for input and output operations:

```cpp
#include <iostream>
```

### Step 4: Create the Main Program

Write the `main` function to take user input for dividing two numbers and handle exceptions:

```cpp
int main() {
    double numerator, denominator;
    try {
        std::cout << "Enter numerator: ";
        std::cin >> numerator;
        std::cout << "Enter denominator: ";
        std::cin >> denominator;
        if (denominator == 0) {
            throw std::runtime_error("Division by zero is not allowed.");
        }
        double result = numerator / denominator;
        std::cout << "Result: " << result << std::endl;
    } catch (const std::exception& e) {
        std::cerr << "Exception: " << e.what() << std::endl;
    }
    return 0;
}
```

### Step 5: Compile and Run

Compile your source file using your C++ compiler. If you're using the command line, navigate to the directory containing your source file and run the command:

```
g++ -o divide_numbers divide_numbers.cpp
```

Then run the compiled executable:

```
./divide_numbers
```

### Step 6: Test Exception Handling

Enter various input values for the numerator and denominator, including zero for the denominator. Observe how the program handles exceptions for divide-by-zero and invalid input.

Congratulations! You've successfully created a C++ program that takes user input for dividing two numbers and handles exceptions for various scenarios.

## Exercise 6: Linked List Implementation

Implement a singly linked list data structure in C++. Create methods to insert, delete, and display elements in the list.

Here's a step-by-step guide to creating a C++ program that implements a singly linked list data structure with methods to insert, delete, and display elements:

### Step 1: Set Up Your Development Environment

Ensure you have a C++ compiler and a text editor or an Integrated Development Environment (IDE) installed on your computer.

### Step 2: Create a New C++ Source File

Open your preferred text editor or IDE and create a new C++ source file.
Save the file with a `.cpp` extension, such as `linked_list.cpp`.

### Step 3: Define the Node Structure

Define the structure for a linked list node:

```cpp
struct Node {
    int data;
    Node* next;
};
```

### Step 4: Create the LinkedList Class

Create a class for the linked list with methods to insert, delete, and display elements:
