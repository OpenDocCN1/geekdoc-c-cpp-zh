To support list initialization, you can define a constructor that receives an object of the class template initializer_list. For class Array, you'd include the <initializer_list> header. Then, you'd define a constructor with the first line:

```
```cpp
Array::Array( initializer_list< int > list )
```
```

You can determine the number of elements in the list parameter by calling its size member function. To obtain each initializer and copy it into the Array object's dynamically allocated built-in array, you can use a range-based for as follows:

```
```cpp
size_t i = 0;
for ( int item : list )
    ptr[ i++ ] = item;
```
```

# ## 18.11 Operators as Member vs. Non-Member Functions

Whether an operator function is implemented as a *member function* or as a *non-member function*, the operator is still used the same way in expressions. So which is best?

When an operator function is implemented as a *member function*, the *leftmost* (or only) operand must be an object (or a reference to an object) of the operator's class. If the left operand must be an object of a different class or a fundamental type, this operator function *must* be implemented as a *non-member function* (as we did in Section 18.5 when overloading << and >> as the stream insertion and stream extraction operators, respectively). A *non-member operator function* can be made a friend of a class if that function must access private or protected members of the class directly.

*Operator member functions* of a specific class are called (*implicitly* by the compiler) only when the *left* operand of a binary operator is specifically an object of that class, or when the *single* operand of a unary operator is an object of that class.

# ### Commutative Operators

Another reason why you might choose a non-member function to overload an operator is to enable the operator to be *commutative*. For example, suppose we have a *fundamental type variable*, number, of type long int, and an *object* bigInteger1, of class HugeInt (a class in which integers may be arbitrarily large rather than being limited by the machine word size of the underlying hardware; class HugeInt is developed in the chapter exercises). The addition operator (+) produces a *temporary HugeInt object* as the sum of a HugeInt and a long int (as in the expression bigInteger1 + number), or as the sum of a long int and a HugeInt (as in the expression number + bigInteger1). Thus, we require the addition operator to be *commutative* (exactly as it is with two fundamental-type operands). The problem is that the class object *must appear on the left* of the addition operator if that operator is to be overloaded as a *member function*. So, we also overload the operator as a *non-member function* to allow the HugeInt to appear on the *right* of the addition. The operator+ function that deals with the HugeInt on the *left* can still be a *member function*. The *non-member function* can simply swap its arguments and call the *member function*.

# ## 18.12 Converting Between Types

Most programs process information of many types. Sometimes all the operations "stay within a type." For example, adding an int to an int produces an int. It's often necessary,