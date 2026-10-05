
# CHAPTER 6

## Structures and Classes

12. Your Community Supported Agriculture (CSA) farm delivers a box of fresh fruits and vegetables to your house once a week. For this Programming Project, define the class BoxOfProduce that contains exactly three bundles of fruits or vegetables. You can represent the fruits or vegetables as an array of type string. Add accessor and mutator functions to get or set the fruits or vegetables stored in the array. Also write an output function that displays the complete contents of the box on the console.

Next, write a main function that creates a BoxOfProduce with three items randomly selected from this list:

- Broccoli
- Tomato
- Kiwi
- Kale
- Tomatillo

This list should be stored in a text file that is read in by your program. For now you can assume that the list contains exactly five types of fruits or vegetables.

Do not worry if your program randomly selects duplicate produce for the three items. Next, the main function should display the contents of the box and allow the user to substitute any one of the five possible fruits or vegetables for any of the fruits or vegetables selected for the box. After the user is done with substitutions output the final contents of the box to be delivered.

# Constructors and Other Tools

## 7.1 CONSTRUCTORS 276

- Constructor Definitions 276
- Pitfall: Constructors with No Arguments 281
- Explicit Constructor Calls 282
- Tip: Always Include a Default Constructor 283
- Example: BankAccount Class 285
- Class Type Member Variables 292

## 7.3 VECTORS—A PREVIEW OF THE STANDARD TEMPLATE LIBRARY 307

- Vector Basics 307
- Pitfall: Using Square Brackets beyond the Size 309
- Tip: Vector Assignment Is Well Behaved 311
- Efficiency Issues 311

## 7.2 MORE TOOLS 295

- The const Parameter Modifier 295
- Pitfall: Inconsistent Use of const 297
- Inline Functions 301
- Static Members 303
- Nested and Local Class Definitions 306

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_304_0.png)

# Constructors and Other Tools

Give us the tools, and we will finish the job.

> WINSTON CHURCHILL, Radio broadcast (February 9, 1941)

# Introduction

This chapter presents a number of tools to use when programming with classes. The most important of these tools are class constructors, a kind of function to initialize objects of the class.

Section 7.3 introduces vectors as an example of classes and a preview of the Standard Template Library (STL). Vectors are similar to arrays but can grow and shrink in size. The STL is an extensive library of predefined classes. Section 7.3 may be covered now or later. The material in Chapters 8 through 18 does not require the material in Chapter 7.3, so you may postpone covering vectors (Section 7.3) if you wish. Sections 7.1 and 7.2 do not use the material in Chapter 5 but do use the material in Chapter 6. Section 7.3 requires Chapters 1 through 6 as well as Section 7.1.

# 7.1 Constructors

Well begun is half done.

> Proverb

Often you want to initialize some or all the member variables for an object when you declare the object. As we will see later in this book, there are other initializing actions you may also want to take, but initializing variables is the most common sort of initialization. C++ includes special provisions for initializations. When you define a class you can define a special kind of member function known as a constructor. A constructor is a member function that is automatically called when an object of that class is declared. A constructor is used to initialize the values of all member variables and to any other sort of initialization that may be needed.

constructor

![](img/f4b6fc3d28ec32a6e3350e2846d6e0d1_305_0.png)

# Constructor Definitions

You define a constructor the same way that you define any other member function, for two points:

- 1. A constructor must have the same name as the class. For example, if the class is named BankAccount, then any definition for this class must be BankAccount.

- 2. A constructor does not return a value.

# Constructors 276

You define a constructor the same way that you define any other member function, for two points:

- 1. A constructor must have the same name as the class. For example, if the class is named BankAccount, then any definition for this class must be BankAccount.

- 2. A constructor does not return a value.

# Constructors 277

You define a constructor the same way that you define any other member function, for two points:

- 1. A constructor must have the same name as the class. For example, if the class is named BankAccount, then any definition for this class must be BankAccount.

- 2. A constructor does not return a value.

# Constructors 278

You define a constructor the same way that you define any other member function, for two points:

- 1. A constructor must have the same name as the class. For example, if the class is named BankAccount, then any definition for this class must be BankAccount.

- 2. A constructor does not return a value.

# Constructors 279

You define a constructor the same way that you define any other member function, for two points:

- 1. A constructor must have the same name as the class. For example, if the class is named BankAccount, then any definition for this class must be BankAccount.

- 2. A constructor does not return a value.

# Constructors 280

You define a constructor the same way that you define any other member function, for two points:

- 1. A constructor must have the same name as the class. For example, if the class is named BankAccount, then any definition for this class must be BankAccount.

- 2. A constructor does not return a value.

# Constructors 281

Pitfall: Constructors with No Arguments

```cpp
class BankAccount {
public:
    BankAccount(); // A default constructor
};
```

Explicit Constructor Calls

For example, if you have a constructor with arguments, you can call it like this:

```cpp
BankAccount account; // Calling the constructor own```

# Constructors 282

# Constructors 283

You define a constructor the same way that you define any other member function, for two points:

- 1. A constructor must have the same name as the class. For example, if the class is named BankAccount, then any definition for this class must be BankAccount.

- 2. A constructor does not return a value.

# Constructors 284

Example: BankAccount Class

```cpp
class BankAccount {
public:
    BankAccount() : balance(0) {} // Default constructor
    BankAccount(double b) : balance(b) {} // Parameterized constructor
private:
    double balance;
};
```

# Constructors 285

Class Type Member Variables

```cpp
class BankAccount {
public:
    BankAccount() : balance(0) {}
    BankAccount(double b) : balance(b) {}
private:
    double balance; // Class type member variable
};
```

# Constructors 292

Class Type Member Variables

```cpp
#include <iostream>
#include <string>

class Student {
public:
    Student() : name("Unknown"), gpa(0.0) {}
    Student(std::string n, double g) : name(n), gpa(g) {}
    void display() const {
        std::cout << "Name: " << name << ", GPA: " << gpa << std::endl;
    }
private:
    std::string name;
    double gpa;
};

int main() {
    Student s1;
    Student s2("Alice", 3.8);
    Student s3("Bob", 3.5);
    s1.display();
    s2.display();
    s3.display();
    return 0;
}
```
