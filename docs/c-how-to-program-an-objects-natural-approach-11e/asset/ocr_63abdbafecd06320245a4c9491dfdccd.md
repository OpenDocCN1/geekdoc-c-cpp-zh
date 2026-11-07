# MyArray Member Functions That Return Iterators

Lines 163–182 define the MyArray member functions that return MyArray’s various kinds of iterators and reverse iterators. The key functions are begin and end in lines 163–168:

+   - **begin** (line 163) returns an iterator pointing to the MyArray’s first element.
+   - **end** (line 164) returns an iterator pointing to one past the MyArray’s last element.
+   - **begin** (line 165) is a const-qualified overload that returns a const_iterator pointing to the MyArray’s first element.
+   - **end** (line 166–168) is a const-qualified overload that returns a const_iterator pointing to one past the MyArray’s last element.

The other member functions that return iterators call these begin and end functions:

+   - **cbegin** and **cend** (lines 169–170) call the versions of **begin** and **end** that return const iterators.
+   - **rbegin** and **rend** (lines 173–174) produce reverse_iterators based on the iterators returned by the **non-const** versions of **begin** and **end**.
+   - **rbegin** and **rend** (lines 175–180) are overloads that produce const_reverse_iterators based on the const_iterators returned by the **const versions of begin and end**.
+   - **crbegin** and **crend** (lines 181–182) return the const_reverse_iterators from calling the const versions of rbegin and rend.

# MyArray Overloaded Operators

Lines 185, 189–196 and 200–207 define MyArray’s overloaded operators. Though we won’t use it in this example, the compiler-generated three-way comparison operator (line 185) enables you to compare entire MyArray objects of the same element type and size. The overloaded operator[] member functions are identical to those in Chapter 11’s MyArray class, but we now call the size member function (lines 191 and 202) when determining whether an index is outside a MyArray’s bounds.

# 15.9.4 MyArray Deduction Guide for Braced Initialization

As you’ve seen, you can initialize a `std::array` using class template argument deduction (CTAD). For example, when the compiler sees the statement:

```
std::array<ints{1, 2, 3, 4, 5};
```

it infers that the array’s element type is int because all the initializers are ints, and it counts the initializers to determine the array’s size. MyArray does not define a constructor that can receive any number of arguments. However, we can define a deduction guide<sup>82</sup> (lines 214–215) that shows the compiler how to deduce a MyArray’s type from a braced initializer, then the compiler can use aggregate initialization (e.g., line 15 in Fig. 15.12) to place the initializers into our MyArray aggregate type’s built-in array data member.

> 82. “Class Template Argument Deduction.” Accessed April 18, 2023. https://en.cppreference.com/w/cpp/language/class_template_argument_deduction.