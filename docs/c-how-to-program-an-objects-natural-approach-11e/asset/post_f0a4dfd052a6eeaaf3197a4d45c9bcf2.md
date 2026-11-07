
The three-argument version adds the **common range**’s elements by default. The four-argument version receives as its last argument a **binary function** that customizes how to perform the calculation. That argument can be supplied as:

- a **function pointer to a binary function** that takes two parameters of the **common range**’s element type and returns a result of that type,
- a binary function object in which the **operator()** function takes two parameters of the **common range**’s element type and returns a result of that type, or
- a **lambda** that takes two parameters of the **common range**’s element type and returns a result of that type.

This example calls **accumulate** with a function pointer, then a function object, then a lambda.

```cpp
// fig14_16.cpp
// Demonstrating function objects.
#include <array>
#include <algorithm>
#include <functional>
#include <iostream>
#include <iterator>
#include <numeric>
```

**Fig. 14.16** Demonstrating function objects.

### Function sumSquares

Lines 12–14 define a function **sumSquares** that takes two arguments of the same type and returns a value of that type—the requirements for the **binary function** that **accumulate** can receive as an argument. The sumSquares function returns the sum of its first argument total and the square of its second argument value.

```cpp
// binary function returns the sum of its first argument total
// and the square of its second argument value
int sumSquares(int total, int value) {
    return total + value * value;
}
```

### Class SumSquaresClass

Lines 19–25 define class SumSquaresClass.³¹ Its overloaded **operator()** has two int parameters and returns an int. This meets the requirements for the binary function that accumulate can call when processing a **common range** of ints. Function **operator()** returns the sum of its first argument total and the square of its second argument value.

31. This class handles only int values, but could be implemented as a class template that handles many types—we’ll define custom class templates in Chapter 15.

```cpp
// class SumSquaresClass defines overloaded operator()
// that returns the sum of its first argument total
// and the square of its second argument value
class SumSquaresClass {
public:
    // add square of value to total and return result
    int operator()(int total, int value) {
        return total + value * value;
    }
};
```

### Calling Algorithm accumulate

We call accumulate three times:

- Lines 36–37 call **accumulate** with a pointer to sumSquares as its last argument.
- Lines 44–45 call **accumulate** with a **SumSquaresClass** function object as the last argument. **SumSquaresClass{}** in line 45 creates a temporary **SumSquaresClass** object and calls its constructor. That function object is then passed to **accumulate**, which calls the **SumSquaresClass** object's **operator()** function.
- Lines 50–51 call **accumulate** with an equivalent lambda. The lambda performs the same tasks as the function **sumSquares** and the overloaded **operator()** function in **SumSquaresClass**.

```cpp
int main() {
    std::array integers{1, 2, 3, 4};
    std::ostream_iterator<int> output{std::cout, " "};

    std::cout << "array integers contains: ";
    std::ranges::copy(integers, output);

    // calculate sum of squares of elements of array integers
    // using binary function sumSquares
    int result{std::accumulate(integers.cbegin(), integers.cend(),
        0, sumSquares)};

    std::cout << "\n\nSum of squares\n"
        << "via binary function sumSquares: " << result;

    // calculate sum of squares of elements of array integers
    // using binary function object
    result = std::accumulate(integers.cbegin(), integers.cend(),
        0, SumSquaresClass{});

    std::cout << "\n\nvia a SumSquaresClass function object: " << result;

    // calculate sum of squares array
    result = std::accumulate(integers.cbegin(), integers.cend(),
        0, [](auto total, auto value){return total + value * value;});

    std::cout << "\n\nvia a lambda: " << result << "\n";
}
```

```text
array integers contains: 1 2 3 4

Sum of squares
via binary function sumSquares: 30
via a SumSquaresClass function object: 30
via a lambda: 30
```

Each call to **accumulate** uses its function argument as follows:

- On the first call to its function argument, **accumulate** passes its third argument’s value (0 in this example) and the value of `integers`’ first element (1 in this example). This calculates and returns the result of 0 + 1 * 1, which is 1.
- On the second call to its function argument, **accumulate** passes the prior result (1) and the value of `integers`’ next element (2). This calculates and returns the result of 1 + 2 * 2, which is 5.
- On the third call to its function argument, **accumulate** passes the prior result (5) and the value of `integers`’ next element (3). This calculates and returns the result of 5 + 3 * 3, which is 14.
- On the last call to its function argument, **accumulate** passes the prior result (14) and the value of `integers`’ next element (4). This calculates and returns the result of 14 + 16, which is 30.

At this point, **accumulate** reaches the end of the common range specified by its first two arguments, so it returns the result (30) of the last call to its function argument.

## 14.6 Projections

When working on objects containing multiple data items, each C++20 **std::ranges algorithm** can use a projection to select a narrower part of each object to process. Consider Employee objects that each have a first name, a last name and a salary. Rather than sorting Employee objects based on all three data members, you can sort them using only their salaries. Figure 14.17 sorts an array of Employee objects by salary—first in ascending order, then in descending order. Lines 11–22 define class Employee. Lines 25–29 provide an overloaded operator<< function for Employees to output them conveniently.

```cpp
// Fig14_17.cpp
// Demonstrating projections with C++20 range algorithms.
#include <array>
#include <algorithm>
#include <format>
#include <iostream>
#include <iterator>
#include <string>
#include <string_view>
```

**Fig. 14.17** | Demonstrating projections with C++20 range algorithms.

```cpp
class Employee {
public:
    Employee(std::string_view first, std::string_view last, int salary)
        : m_first{first}, m_last{last}, m_salary{salary} {}
    std::string getFirst() const { return m_first; }
    std::string getLast() const { return m_last; }
    int getSalary() const { return m_salary; }
private:
    std::string m_first;
    std::string m_last;
    int m_salary;
};

// operator<< for an Employee
std::ostream& operator<<(std::ostream& out, const Employee& e) {
    out << std::format("{:10}{:10}{}",
        e.getLast(), e.getFirst(), e.getSalary());
    return out;
}
```

**Fig. 14.17** | Demonstrating projections with C++20 range algorithms.

### Defining and Displaying an array<Employee>

Lines 32–36 define an array<Employee>, initializing it with three Employees. Line 41 displays the Employees, so we can confirm later that they’re sorted properly.

```cpp
int main() {
    std::array<Employee> employees{
        Employee{"Jo-woon", "Woo", 5000},
        Employee{"Amaia", "Jones", 7600},
        Employee{"Titania", "Makaya", 3587}
    };

    std::ostream_iterator<Employee> output{std::cout, "\n"};

    std::cout << "Employees:\n";
    std::ranges::copy(employees, output);
}
```

```text
Employees:
Woo       Jo-woon   5000
Jones     Amaia     7600
Makaya    Titania   3587
```

### Using a Projection to Sort the array<Employee> in Ascending Order

Lines 45–46 call the `std::ranges::sort` algorithm, passing three arguments:

- The first argument (employees) is the range to sort.
- The second argument ({}) is the binary predicate function that sort uses to compare elements when determining their sort order. The notation {} indicates
