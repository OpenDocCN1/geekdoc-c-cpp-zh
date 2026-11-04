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

# Step 5: Create the Main Program

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

# Step 6: Compile and Run