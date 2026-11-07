
## Checkpoint

- **1. (Code)** What does the following code do?

```cpp
MyArray& operator++();
```

**Answer:** This declares MyArray's unary overloaded preincrement operator (++).

- **2. (True/False)** You can use the standard library’s `for_each` algorithm to call a function that performs a task once for each element of a span.

**Answer:** True.

## 11.6.14 Overloading the Postincrement Operator

Overloading the postfix increment operator presents a challenge. The compiler must be able to distinguish between the signatures of the overloaded prefix and postfix increment operator functions. By convention, when the compiler sees a postincrement expression like `ints4++`, it generates the member-function call

```cpp
ints4.operator++(0)
```

The argument 0 is strictly a **dummy value** that the compiler uses to distinguish between the prefix and postfix increment operator functions. The same syntax differentiates the prefix and postfix decrement operator functions.

Line 48 of Fig. 11.4

```cpp
MyArray operator++(int);
```

declares MyArray's unary overloaded postincrement operator (++) with the int parameter that receives the dummy value 0. The parameter is not used, so it’s declared without a parameter name. To emulate the effect of the postincrement, we must return an **unincremented copy** of the MyArray object. So, the function’s definition (lines 135–139)

- uses the `MyArray` copy constructor to make a local copy of the original `MyArray`,
- calls the preincrement operator to add one to every element of the `MyArray`^32, then
- returns the unincremented local copy of the `MyArray` *by value*—this is another case in which compilers can use the named return value optimization (NRVO).

The extra local object created by the postfix increment (or decrement) operator can result in a performance problem, especially if the operator is used in a loop. For this reason, you should prefer the prefix increment and decrement operators.

```cpp
134 // postincrement every element, and return copy of original MyArray
135 MyArray MyArray::operator++(int) {
136     MyArray temp(*this);
137     ++(*this); // call preincrement operator++ to do the incrementing
138     return temp; // Return the temporary copy made before incrementing
139 }
140
```

32. Herb Sutter, “GotW #2 Solution: Temporary Objects,” May 13, 2013. Accessed April 18, 2023. https://herbsutter.com/2013/05/13/gotw-2-solution-temporary-objects/.

## Checkpoint

- **1. (Discussion)** By convention, when the compiler sees a postincrement expression like `ints4++`, it generates the member-function call `ints4.operator++(0)`. Why does the compiler provide the 0 argument?

**Answer:** The 0 argument is strictly a dummy value that the compiler uses to distinguish between the prefix and postfix increment operator functions.

- **2. (True/False)** The extra local object created by the prefix increment (or decrement) operator can result in a performance problem, especially if the operator is used in a loop. For this reason, you should prefer the postfix increment and decrement operators.

**Answer:** False. Actually, the postfix increment (or decrement) operator has this performance problem. For this reason, prefer the prefix increment and decrement operators.

## 11.6.15 Overloading the Addition Assignment Operator (+=)

Line 51 of Fig. 11.4

```cpp
MyArray& operator+=(int value);
```

declares MyArray’s **overloaded addition assignment operator** (`+=`), which adds a value to every element of a MyArray, then returns a reference to the modified object to enable cascaded calls. Like the preincrement operator, we use a span and the standard library function `for_each` to process every element in the MyArray. In this case, the lambda we pass as `for_each`’s last argument (line 146) uses the `operator+=` function’s value parameter in its body. The lambda introducer `[value]` specifies that the compiler should capture value for use in the lambda’s body.

```cpp
141  // add value to every element, then return updated MyArray
142  MyArray& MyArray::operator+=(int value) {
143      // use a span and for_each to increment every element
144      const std::span<int> items{m_ptr.get(), m_size};
145      std::for_each(std::begin(items), std::end(items),
146          [value](auto& item) {item += value;});
147      return *this;
148  }
149
```

## 11.6.16 Overloading the Binary Stream Extraction (>>) and Stream Insertion (<<) Operators

You can input and output fundamental-type data using the **stream extraction operator** (`>>`) and the **stream insertion operator** (`<<`). The C++ standard library overloads these operators for each fundamental type, including pointers and `char*` strings. You also can overload these to perform input and output for custom types.

Line 10 of Fig. 11.4

```cpp
friend std::istream& operator>>(std::istream& in, MyArray& a);
```

and line 58 of Fig. 11.4

```cpp
std::ostream& operator<<(std::ostream& out, const MyArray& a);
```

declare the non-member **overloaded stream-extraction operator (>>)** and **overloaded stream-insertion operator (<<)**. We declared **operator>>** in the class as a friend because it will access a MyArray’s private data directly for performance. The **operator<<** is not declared as a friend. As you’ll see, it calls MyArray’s toString member function to get a MyArray’s string representation, then outputs it.

### Implementing the Stream Extraction Operator

The overloaded stream-extraction operator (>>) (lines 152–160) takes as arguments an istream reference and a MyArray reference. It returns the istream reference argument to enable cascaded inputs, like

```cpp
std::cin >> ints1 >> ints2;
```

When the compiler sees an expression like `cin >> ints1`, it invokes **non-member function operator>>** with the call

```cpp
operator>>(std::cin, ints1)
```

We’ll say why this needs to be a **non-member function** momentarily. When this call completes, it returns a reference to `cin`, which would then be used in the `cin` statement above to input values into `ints2`. The function creates a span (line 153) representing MyArray’s dynamically allocated `int` array. Then lines 155–157 iterate through the span’s elements, reading one value at a time from the input stream and placing the value in the corresponding element of the dynamically allocated `int` array.

```cpp
// overloaded input operator for class MyArray.
// inputs values for entire MyArray
std::istream& operator>>(std::istream& in, MyArray& a) {
    std::span<int> items{a.m_ptr.get(), a.m_size};

    for (auto& item : items) {
        in >> item;
    }

    return in; // enables cin >> x >> y;
}
```

### Implementing the Stream Insertion Operator

The overloaded stream insertion function (<<) (lines 163–166) receives an `ostream` reference and a const MyArray reference as arguments and returns an `ostream` reference. The function calls MyArray’s toString member function, then outputs the resulting string. The function returns the `ostream` reference argument to enable cascaded **output statements**, like

```cpp
std::cout << ints1 << ints2;
```

When the compiler sees an expression like `std::cout << ints1`, it invokes **non-member function operator<<** with the call

```cpp
operator<<(std::cout, ints1)
```

```cpp
// overloaded output operator for class MyArray
std::ostream& operator<<(std::ostream& out, const MyArray& a) {
    out << a.toString();
    return out; // enables std::cout << x << y;
}
```

### Why operator>> and operator<< Must Be Non-member Functions

The operator>> and operator<< functions are defined as non-member functions, so we can specify their operands’ order in each function’s parameter list. In a binary overloaded operator implemented as a non-member function, the first parameter is the left operand, and the second is the right operand.

For the operators >> and <<, the MyArray object should be each operator’s right operand, so you can use them the way C++ programmers expect, as in the statements

```cpp
std::cin >> ints4;
std::cout << ints4;
```

If we defined these functions as MyArray member functions, programmers would have to write the following awkward statements to input or output MyArray objects:

```cpp
ints4 >> std::cin;
ints4 << std::cout;
```

Such statements would be confusing and, in some cases, would lead to compilation errors. Programmers are familiar with cin and cout always appearing to the left of these operators.

Overloaded binary operators may be member functions only for the class of the operator’s left operand. For operator>> and operator<< to be member functions, we’d have to modify the standard library classes istream and ostream, which is not allowed.

### Choosing Member vs. Non-Member Functions

Overloaded operator functions, and functions in general, can be

- member functions with direct access to the class’s internal implementation details,
- friend functions with direct access to the class’s internal implementation details, or
- non-member, non-friend functions—often called free functions—that interact with objects of the class through its public interface.

The C++ Core Guidelines say a function should be a member only if it needs direct access to the class’s internal implementation details, such as its private data.<sup>33</sup>

Another reason to use non-member functions is to define commutative operators. Consider a class HugeInt for arbitrary-sized integers. With a HugeInt named bigInt, we might write expressions like

```cpp
bigInt + 7
7 + bigInt
```

33. C++ Core Guidelines, “C4: Make a Function a Member Only If It Needs Direct Access to the Representation of a Class.” Accessed April 18, 2023. https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rc-member.
