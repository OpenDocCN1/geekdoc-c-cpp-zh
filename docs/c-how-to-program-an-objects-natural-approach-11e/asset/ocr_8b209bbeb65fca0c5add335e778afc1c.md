```
```text
s4 = happy birthday to you, have a great day!
```
```

# Testing Self-Assignment with the string Copy Assignment Operator

Line 66 uses string’s overloaded copy assignment (=) operator to demonstrate that it performs self-assignment properly, so s4 still has the same value after the self-assignment. When we build class MyArray later in the chapter, we’ll show how to properly implement self-assignment for objects that manage their own memory.

```
```cpp
// test overloaded copy assignment (=) operator with self-assignment
std::cout << "assigning s4 to s4\n";
s4 = s4;
std::cout << std::format("s4 = {}\n\n", s4);
```
```

```
```text
assigning s4 to s4
s4 = happy birthday to you, have a great day!
```
```

# Initializing a string with a string_view

Line 71 demonstrates string’s constructor that receives a string_view, in this case, copying the character data represented by the string_view (line 12) into the new string s5.

```
```cpp
// test string's string_view constructor
std::cout << "initializing s5 with string_view v\n";
std::string s5{v};
std::cout << std::format("s5 is {}\n\n", s5);
```
```

```
```text
initializing s5 with string_view v
s5 is hello
```
```

# string’s [] Operator

Lines 75–76 use string’s overloaded [] operator in assignments to create lvalues for replacing characters in s1. Lines 77–78 output s1’s new value. The [] operator returns the character at the specified location as a modifiable lvalue or a nonmodifiable lvalue (e.g., a const reference), depending on the context in which the expression appears. For example:

+   - When using [] on a non-const string, the function returns a modifiable *lvalue*, which you can place on the left of an assignment (=) operator to assign a new value to that location in the string, as in lines 77–78.
+   - When using [] on a const string, the function returns a nonmodifiable *lvalue* that you can use to obtain, but not modify, the value at that location in the string.

**The overloaded [] operator does not perform bounds checking. So, you must ensure that operations using this operator do not accidentally manipulate elements outside the string’s bounds.**