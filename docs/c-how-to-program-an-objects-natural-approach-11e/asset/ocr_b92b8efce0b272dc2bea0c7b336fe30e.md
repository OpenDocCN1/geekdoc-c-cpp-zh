the lambda introducer [classNumber] specifies that the countClass lambda's parameter classNumber is used in this lambda's body—this is known as capturing the countClass variable. By default, capturing is done by value, so line 72's lambda captures a copy of classNumber's value. We'll say more about capturing lambdas and the std::ranges algorithms in Chapter 14. Lines 75–77 define constants for the three passenger classes. Lines 78–80 call the countClass lambda for each passenger class, and lines 82–84 display the counts.

```
```cpp
68  // passenger counts by class
69  auto countClass{
70      [](const auto& column, const int classNumber) {
71          return std::ranges::count_if(column,
72              [classNumber](int x) {return classNumber == x;});
73      };
74
75  constexpr int firstClass{1};
76  constexpr int secondClass{2};
77  constexpr int thirdClass{3};
78  const auto firstCount{countClass(pclass, firstClass)};
79  const auto secondCount{countClass(pclass, secondClass)};
80  const auto thirdCount{countClass(pclass, thirdClass)};
81
82  std::cout << "\nPassenger counts by class:\n"
83      << std::format("1st: {:>3}\n2nd: {:>3}\n3rd: {}\n\n",
84          firstCount, secondCount, thirdCount);
85
```
```

```
```text
Passenger counts by class:
1st: 323
2nd: 277
3rd: 709
```
```

# ## Basic Descriptive Statistics for the Cleaned Age Column

Let’s say you want to determine some statistics about people who survived. Lines 87–89 define a lambda that counts survivors using C++20's std::ranges::count_if algorithm counts. Recall that the survived column contains 1 or 0 to represent survived or died, respectively. These also are values that C++ can treat as true (1) or false (0), so the lambda in line 88

```
```cpp
[](auto x) {return x;}
```
```

simply returns the column value. If that value is 1, count_if counts that element. To determine how many people died, line 92 simply subtracts survivorCount from the survived vector's size. Line 94 calculates the percentage of people who survived.

```
```cpp
86  // percentage of people who survived
87  const auto survivorCount{
88      std::ranges::count_if(survived, [](auto x) {return x;})
89  };
90
```
```