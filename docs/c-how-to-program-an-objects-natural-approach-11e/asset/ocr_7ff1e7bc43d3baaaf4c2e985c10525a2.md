# Using the Overloaded Inequality Operator (!=)

Line 36 tests MyArray’s overloaded inequality operator (!=) by evaluating the condition

`ints1 != ints2`

The program output shows that the MyArray objects are not equal. Two MyArray objects will be equal if they have the same number of elements and their corresponding element values are identical. As you’ll see, we define only MyArray’s overloaded == operator. In C++20, the compiler autogenerates != if you provide an == operator for your type. Operator != simply returns the opposite of ==.

```
```cpp
// use overloaded inequality (!=) operator
std::cout << "\n\nEvaluating: ints1 != ints2\n";

if (ints1 != ints2) {
    std::cout << "ints1 and ints2 are not equal\n\n";
}
```
```

```
```text
Evaluating: ints1 != ints2
ints1 and ints2 are not equal
```
```

# Initializing a New MyArray with a Copy of an Existing MyArray

Line 41 instantiates the MyArray object ints3 and initializes it with a copy of ints1’s data. This invokes the MyArray copy constructor to copy ints1’s elements into ints3. A copy constructor is invoked whenever a copy of an object is needed, such as

+   - passing an object by value to a function,
+   - returning an object by value from a function or
+   - initializing an object with a copy of another object of the same class.

Lines 44–45 display ints3’s size and contents to confirm that ints3’s elements were set correctly by the copy constructor.

```
```cpp
// create MyArray ints3 by copying ints1
MyArray ints3{ints1}; // invokes copy constructor

// print ints3 size and contents
std::cout << std::format("\nints3 size: {}\ncontents: ", ints3.size())
          << ints3;
```
```

```
```text
MyArray copy constructor

ints3 size: 7
contents: {1, 2, 3, 4, 5, 6, 7}
```
```

When a class such as MyArray contains both a copy constructor and a move constructor, the compiler chooses the correct one to use based on the context. In line 41, the compiler chose MyArray’s copy constructor because variable names, like ints1, are lvalues. As