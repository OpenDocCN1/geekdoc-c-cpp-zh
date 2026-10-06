
# 10.5 Function Objects — 439

Tab. 10.8: STL Function Objects in Standard Library.

| STL Function Object | Type | Description |
|---|---|---|
| Plus<T> | Numeric | Input two operands with a type of T, return their sum |
| Minus<T> | Numeric | Input two operands with a type of T, return the result of subtracting the second operand from the first operand |
| Multiples<T> | Numeric | Input two operands with a type of T, return their product |
| Divide<T> | Numeric | Input two operands with a type of T, return the result of dividing the second operand by the first operand |
| Modulus<T> | Relation | Input two operands x and y with a type of T, return result of x%y |
| Negative<T> | Relation | Input an operand x and y with a type of T, return its opposite number |
| Equal<T> | Relation | Input two operands x and y with a type of T, return true if x=y |
| Not_equal_to<T> | Relation | Input two operands x and y with a type of T, return true if x!=y |
| Greater<T> | Relation | Input two operands x and y with a type of T, return true if x>y |
| Less<T> | Relation | Input two operands x and y with a type of T, return true if x<y |
| Greater_equal<T> | Relation | Input two operands x and y with a type of T, return true if x>=y |
| Less_equal<T> | Relation | Input two operands x and y with a type of T, return true if x<=y |
| Logical_and<T> | Logical | Input two operands x and y with a type of T, return the result of logical and: x&&y |
| Logical_or<T> | Logical | Input two operands x and y with a type of T, return the result of logical or: x||y |
| Logical_not<T> | Logical | Input an operand x with a type of T, return the result of not: !x |

STL defines a number of function objects, including arithmetic operations, boolean operations, and logical operations (as shown in Table 10.8). All of them are defined as inline functions to maximize performance. You can also use the function object provide by STL to implement the same functionalities. Here is the program: Example 10.15:
```cpp
// 10_15.cpp
#include <iostream>
#include <numeric>
#include <functional>

using namespace std;

int main() {
    int A[] = {1, 2, 3, 4, 5};
    const int N = sizeof(A)/sizeof(int);
    cout << "The result by multiplying all elements in A is " << accumulate(A, A + N, 1, multiplies<int>()) << endl;
}
```

STL defines two basic classes of function objects, one for unary functions and for binary functions for design. For advanced topics please refer to related materials. Everything is the same except we changed.

## 2. Function Adapters

### 10.6 Application — Improving the HR Management of a Small Company

In this section, we demonstrate how to use STL's vectors to simplify storing objects. There are three files in the program: employee.h, func.cpp, and 10_16.cpp. 10_16.cpp is derived from Example 9.16: Improving the HR management program.

```cpp
// 10_16.cpp
#include <iostream>
#include "employee.h"
#include <vector>

using namespace std;

int main() {
    manager m1;
    technician t1;
    salesmanager sm1;
    salesman s1;
    char namestr[20];

    // The employee names will be saved in namestr temporary
    vector<employee*> vchar; // Define vector container
    vchar.push_back(&m1);
    vchar.push_back(&t1);
    vchar.push_back(&sm1);
    vchar.push_back(&s1);

    int i;
    for(i=0; i<4; i++) {
        cout << "Please input the name of next employee:";
        cin >> namestr;
        vchar[i]->SetName(namestr); // Set name of every employee
        vchar[i]->promote(); // Promote
    }

    cout << "Please input the part-time technicians " << t1.GetName() << " working hours this week:";
    int ww;
    cin >> ww;
    t1.SetWorkHours(ww); // Set working hours

    cout << "Please input the sales manager " << sm1.GetName() << " total sales this month of his department:";
    float sl;
    cin >> sl;
    sm1.Setales(sl); // Set total sales

    cout << "Please input the salesman " << s1.GetName() << " sales month:";
    cin >> sl;
    s1.Setales(sl); // Set sales

    for(i=0; i<4; i++) {
        vchar[i]->pay(); // Calculate salary
        cout << vchar[i]->GetName() << " ID " << vchar[i]->GetIndivualEmpNo() << " Level " << vchar[i]->GetGrade() << ", salary this month " << vchar[i]->GetaccumPay() << endl;
    }
}
```

Results:
Please input the name of next employee: Zhang
Please input the name of next employee: Wang
Please input the name of next employee: Li
Please input the name of next employee: Zhao
Please input the part-time technicians Wang's working hours this week:40
Please input the sales manager Li's total sales this month of his depart: 40000
Please input the salesman Zhao's sales this month: 40000
Zhang ID 1000 Level 4, salary this month 8000
Wang ID 1001 Level 3, salary this month 4000
Li ID 1002 Level 3, salary this month 7000
Zhao ID 1003 Level 1, salary this month 1600

## 10.7 Summary

This chapter introduced the concepts of containers, container iterators, iterators, iterator adapters, generic algorithms, function objects, and function adapters; and discussed a number of collections (vectors, deques, and lists) and container iterators (stacks, queues, priority queues). This chapter also discussed four generic algorithms, iterators, and function objects, and demonstrates how to use STL. STL is a powerful tool for simplifying the development.

## Exercises

- 10.1 What are the two types of containers? What are the five types of iterators? What are three types of container adapters? What mechanism does STL use to access the elements in containers?
- 10.2 Write a program to use the fill function in STL to set a certain range of container to a certain value, then use the generator to generate a sequence of value.
- 10.3 Write a program to use swap(), iter_swap(), and swap_ranges() to swap elements in an array.
- 10.4 What are the two types of containers? What are the five types of iterators? What are three types of container adapters? What mechanism does STL use to access the elements in containers?
- 10.5 What are the two types of containers? What are the five types of iterators? What are three types of container adapters? What mechanism does STL use to access the elements in containers?
- 10.6 What are the two types of containers? What are the five types of iterators? What are three types of container adapters? What mechanism does STL use to access the elements in containers?
- 10.7 The length of a deque is variable. The method size() returns the number of elements in a deque, and the method max_size() returns the available size of the deque.

*(Note: The OCR text provided contained significant repetitions and garbled sections in the exercises area; I have cleaned the logical flow based on the context of the preceding pages.)*
