
## C++11: *Move Constructor and Move Assignment Operator*

C++11 adds the notions of a *move constructor* and a *move assignment operator*. We defer a discussion of these new functions until Chapter 24, C++11 and C++14 Additional Features. This discussion will affect the two preceding tips.

## C++11: Deleting Unwanted Member Functions from Your Class

Prior to C++11, you could prevent class objects from being *copied* or *assigned* by declaring as `private` the class’s copy constructor and overloaded assignment operator. As of C++11, you can simply *delete* these functions from your class. To do so in class `Array`, replace the prototypes in lines 14 and 18 of **Fig. 10.10** with

```cpp
Array(const Array&) = delete;
const Array& operator=(const Array&) = delete;
```

Though you can delete *any* member function, it’s most commonly used with member functions that the compiler can *auto-generate*—the default constructor, copy constructor, assignment operator, and in C++11, the move constructor and move assignment operator.

## *Overloaded Equality and Inequality Operators*

Line 19 of **Fig. 10.10** declares the overloaded equality operator (`==`) for the class. When the compiler sees the expression `integers1 == integers2` in line 51 of **Fig. 10.9**, the compiler invokes member function `operator==` with the call

```cpp
integers1.operator==(integers2);
```

Member function `operator==` (defined in **Fig. 10.11**, lines 57–69) immediately returns `false` if the `size` members of the `Array`s are not equal. Otherwise, `operator==` compares each pair of elements. If they’re all equal, the function returns `true`. The first pair of elements to differ causes the function to return `false` immediately.

Lines 22–24 of **Fig. 10.10** define the overloaded inequality operator (`!=`). Member function `operator!=` uses the overloaded `operator==` function to determine whether one `Array` is *equal* to another, then returns the *opposite* of that result. Writing `operator!=` in this manner enables you to *reuse* `operator==`, which reduces the amount of code that must be written in the class. Also, the full function definition for `operator!=` is in the `Array` header. This allows the compiler to *inline* the definition of `operator!=`.

## Overloaded Subscript Operators

Lines 27 and 30 of **Fig. 10.10** declare two overloaded subscript operators (defined in **Fig. 10.11** in lines 73–80 and 84–91, respectively). When the compiler sees the expression `integers1[5]` (**Fig. 10.9**, line 56), it invokes the appropriate overloaded `operator[]` member function by generating the call

```cpp
integers1.operator[](5)
```

The compiler creates a call to the `const` version of `operator[]` (**Fig. 10.11**, lines 84–91) when the subscript operator is used on a `const` `Array` object. For example, if you pass an `Array` to a function that receives the `Array` as a `const Array&` named `z`, then the `const` version of `operator[]` is required to execute a statement such as

```cpp
cout << z[3] << endl;
```

Remember, a program can invoke only the `const` member functions of a `const` object.

Each definition of `operator[]` determines whether the subscript it receives as an argument is *in range*—and if not, each throws an `out_of_range` exception. If the subscript is in range, the non-`const` version of `operator[]` returns the appropriate `Array` element as a reference so that it may be used as a modifiable *lvalue* (e.g., on the *left* side of an assignment statement). If the subscript is in range, the `const` version of `operator[]` returns a copy of the appropriate element of the `Array`.

## *C++11: Managing Dynamically Allocated Memory with `unique_ptr`*

In this case study, class `Array`’s destructor used `delete[]` to return the dynamically allocated built-in array to the free store. C++11 enables you to use `unique_ptr` to ensure that this dynamically allocated memory is deleted automatically when the `Array` object goes out of scope. In **Chapter 17**, we introduce `unique_ptr` and show how to use it to manage dynamically allocated objects or dynamically allocated built-in arrays.

## C++11: Passing a List Initializer to a Constructor

In **Fig. 7.4**, we showed how to initialize an `array` object with a comma-separated list of initializers in braces, as in

```cpp
array<int, 5> n{32, 27, 64, 18, 95};
```

You can also use list initializers when you declare objects of your own classes. For example, you can provide an `Array` constructor that would enable the following declarations:

```cpp
Array integers{1, 2, 3, 4, 5};
```

or

```cpp
Array integers = {1, 2, 3, 4, 5};
```

each of which creates an `Array` object with five elements containing the integers from 1 to 5.

To support list initialization, you can define a constructor that receives an *object* of the class template `initializer_list`. For class `Array`, you’d include the `<initializer_list>` header. Then, you’d define a constructor with the first line:

```cpp
Array::Array(initializer_list<int> list)
```

You can determine the number of elements in the `list` parameter by calling its `size` member function. To obtain each initializer and copy it into the `Array` object’s dynamically allocated built-in array, you can use a range-based `for` as follows:

```cpp
size_t i{0};
for (int item : list) {
    ptr[i++] = item;
}
```

## 10.11 Operators as Member vs. Non-Member Functions

Whether an operator function is implemented as a *member function* or as a *non-member function*, the operator is still used the same way in expressions. So which is best?

When an operator function is implemented as a *member function*, the *leftmost* (or only) operand must be an object (or a reference to an object) of the operator’s class. If the left operand *must* be an object of a different class or a fundamental type, this operator function *must* be implemented as a *non-member function* (as we did in **Section 10.5** when overloading `<<` and `>>` as the stream insertion and stream extraction operators, respectively). A *non-member operator function* can be made a `friend` of a class if that function must access `private` or `protected` members of that class directly.

Operator member functions of a specific class are called (implicitly by the compiler) only when the *left* operand of a *binary operator* is specifically an object of that class, or when the *single operand* of a *unary operator* is an object of that class.

### *Commutative Operators*

Another reason why you might choose a non-member function to overload an operator is to enable the operator to be *commutative*. For example, suppose we have

- a fundamental type variable, `number`, of type `long int` and
- an object `bigInteger`, of class `HugeInteger`—a class in which integers may be arbitrarily large rather than being limited by the machine word size of the underlying hardware (class `HugeInteger` is developed in the chapter exercises).

Both the expressions `bigInteger + number` (the sum of a `HugeInteger` and a `long int`) and `number + bigInteger` (the sum of a `long int` and a `HugeInteger`) can produce a temporary `HugeInteger` containing the sum of the values. Thus, we require the addition operator to be *commutative* (exactly as it is with two fundamental-type operands).

The problem is that the class object must appear on the left of the addition operator if that operator is to be overloaded as a *member function*. So, we also overload the operator as a non-member function to allow the `HugeInteger` to appear on the right of the addition. The `operator+` function that deals with the `HugeInteger` on the left can still be a member function. The non-member function can simply swap its arguments and call the member function. You also could define both overloads as non-member functions.
