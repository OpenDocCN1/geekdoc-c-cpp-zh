
# Part 12: Assembling Everything: Smaller than normal Undertakings

In this part, we'll apply the ideas we've advanced all through this book to make a few smaller than normal undertakings in C++. These tasks will assist with building up how you might interpret programming basics and permit you to rehearse critical thinking abilities in a tomfoolery and intelligent way.

# Building Basic Games

Speculating Game: Make a program that produces an irregular number somewhere in the range of 1 and 100 and requests that the client surmise the number. Give criticism to the client (e.g., "Excessively high" or "Excessively low") and monitor the quantity of endeavors. Permit the client to play once more assuming they need it.

Rock, Paper, Scissors: Execute the exemplary round of Rock, Paper, Scissors. Brief the client to pick one of the three choices, then, at that point, produce an irregular decision for the PC. Decide the champ in light of the guidelines of the game and show the outcome.

# Making Intuitive Projects

Plan for the day Director: Foster a program that permits clients to deal with a plan for the day. Clients ought to have the option to add errands, mark undertakings as finished, eliminate undertakings, and show the ongoing rundown of assignments. Execute a menu-based interface for communicating with the plan for the day.

Straightforward Mini-computer: Construct an essential number cruncher program that can perform math tasks like expansion, deduction, duplication, and division. Permit clients to enter two numbers and pick an activity to perform. Show the outcome to the client.

# Tackling Fun Issues with C++

Fibonacci Succession: Compose a program that produces the Fibonacci grouping up to a predefined number of terms. Show the arrangement to the client and compute the amount of the succession.

Palindrome Checker: Make a program that checks assuming a given string is a palindrome (peruses similar advances and in reverse). Overlook spaces, accentuation, and capitalization while deciding whether a string is a palindrome.

End

In this section, we've investigated a few scaled down projects that you can execute to rehearse your C++ programming abilities. These activities range from straightforward games to intelligent projects and critical thinking difficulties. By chipping away at these undertakings, you'll support how you might interpret programming ideas as well as gain active involvement with building certifiable applications with C++. Have a good time coding!

# Section 13: High level Subjects in C++

In this part, we'll investigate a few high level subjects in C++ that go past the nuts and bolts canvassed before in this book. These points will develop how you might interpret the language and acquaint you with further developed ideas and procedures.

# Formats

Formats in C++ permit you to compose nonexclusive code that can work with any information type. They are especially valuable for making information designs and calculations that are autonomous of explicit information types.

Duplicate code

```cpp
template<typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}
```

# STL (Standard Format Library)

The Standard Format Library (STL) is a strong assortment of classes and works that give normal information designs and calculations in C++. It incorporates compartments like vectors, records, and guides, as well as calculations for arranging, looking, and controlling information.

Duplicate code

```cpp
#include <vector>
#include <algorithm>

std::vector<int> numbers = {3, 1, 4, 1, 5, 9, 2, 6};

std::sort(numbers.begin(), numbers.end());
```

# Lambda Articulations

Lambda articulations permit you to characterize unknown capabilities inline, making it more straightforward to compose short, one-off capabilities without the requirement for isolated capability announcements.

Duplicate code

```cpp
auto total = [](int a, int b) { return a + b; };

std::cout << total(3, 5) << std::endl; //Result: 8
```

# Simultaneousness

C++ offers help for multi-stringing and offbeat programming through libraries like <thread> and <future>. These highlights permit you to make programs that can play out various assignments at the same time, further developing execution and responsiveness.

Duplicate code

```cpp
#include <iostream>
#include <thread>

void welcome() {
    std::cout << "Hello!" << std::endl;
}

int main() {
    std::thread t(welcome);
    t.join();
    return 0;
}
```

# Shrewd Pointers

Shrewd pointers are objects that act like pointers however give extra features like memory management. They help with preventing memory leaks.

```cpp
#include <memory>

#::shared_ptr<int> ptr = std::make_shared<int>(10);
```

End

In this part, we've investigated a few high level subjects in C++, including formats, Standard Format Library (STL), lambda articulations, simultaneousness, and shrewd pointers. These points will develop how you might interpret the language and de testing. As you proceed with your journey with C++, make sure to explore further developed ideas and techniques.

# Part 14: C++ Best Practices and Improvement

In this part, we've dive into best practices and advancement methods for writing effective and viable C++ code. Following these practices will assist you with creating top notch programming that is obvious, maintainable, and robust.

# 1. Utilize Significant Variable Names

Pick descriptive names for factors, works, and classes to make your code more obvious.

# 2. Follow Coding Standards

Stick to a steady coding style and organizing patterns. This further develops code coherence and makes collaboration easier.

# 3. Limit Global Factors

Limit the utilization of global factors, as they can create hidden dependencies and make testing difficult.

# 4. Avoid Magic Numbers

Replace numeric literals with named constants or specifications to further develop code meaningfulness and maintainability.

# 5. Error Handling

Implement appropriate error handling with components, for example, exceptions or error codes, to nimbly handle unexpected circumstances and prevent crashes.

# 6. Use Smart Pointers

Use smart pointers (e.g., std::unique_ptr and std::shared_ptr) to manage memory naturally and avoid memory leaks.

# 7. Avoid Premature Optimization

Center around writing clear and viable code first. Just advance execution segments of code after profiling and identifying bottlenecks.

# 8. Use Standard Library

Use the features and calculations provided by the C++ Standard Library (STL) whenever the situation allows. It is widely tested, efficient, and compact.

# 9. Profile and Benchmark

Identify execution bottlenecks by profiling your code and use benchmarks to quantify the effect of advancements.

# 10. Document Your Code

Write clear and brief comments to archive your code, including explanations of logic, behavior, and any non-obvious design choices.

# 11. Test Driven Development (TDD)

Adopt a test-driven development approach to ensure that your code acts true to form and stays right after changes.

# 12. Modularize Your Code

Break down your code into smaller, reusable modules (functions, classes, or libraries) to advance code reusability and viability.

# 13. Continuous Integration and Continuous Deployment (CI/CD)

Automate the build, test, and deployment cycles to ensure that changes to your codebase are routinely tested and delivered in a controlled way.

# 14. Learn from Others

Focus on code written by experienced C++ designers, participate in code reviews, and contribute to open-source projects to learn new methods and best practices.
