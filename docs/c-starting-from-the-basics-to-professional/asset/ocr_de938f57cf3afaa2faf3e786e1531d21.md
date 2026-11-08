The nested try block starts by defining constants that specify the range of index values and the size of the array. The size and start variables are used to create an instance of the Array<> template to store 21 values of type double. The second template argument corresponds to the non-type parameter and specifies the lower limit for the index values of the array. The size of the array is specified by the constructor argument.

The for loop that follows assigns values to the elements of the values object. The loop index, i, runs from the lower limit start, which will be -10, up to and including the upper limit end, which will be +10. Within the loop the values of the array elements are set to run from 1 to 21.

A second for loop then outputs the sums of pairs of successive elements, starting at the last array element and counting down. The lines variable is used to output the sums, five to a line. As in Ex17_01, sloppy control of the index value eventually results in an values[1-i] expression, which throws an out_of_range exception. The handler for the nested try block catches it and displays the message you see in the output.

The statement that creates an array to store Box objects is in the outer try block of main(). The type for boxes is ArrayBox<-numBoxes / 2>, which demonstrates that expressions are acceptable as argument values for non-type parameters in a template instantiation. The type of such an expression must either match the type of the parameter, or at least be convertible to the appropriate type by means of an implicit conversion.

You do need to take care if such an expression includes the > character. Here's an example:

```
```cpp
ArrayBox<numBoxes > 5 ? numBoxes : 5> boxes{42};    // Will not compile!
```
```

The intent of the expression for the second argument that uses the conditional operator is to supply a value of at least 5, but as it stands, this won't compile. The > in the expression is paired with the opening angle bracket and closes the parameter list. Parentheses are necessary to make the statement valid:

```
```cpp
ArrayBox<(numBoxes > 5 ? numBoxes : 5)> boxes{42};    // OK
```
```

Parentheses are also likely to be necessary for expressions for non-type parameters that involve the arrow operator (->) or the shift right operator (>>).

The final for loop throws another exception, this time because the index exceeds the upper limit. The exception is caught by the catch block for the body of main(). The output shows that the exception is identified as type std::out_of_range. This again confirms there is no object slicing when catching the exception by reference to a base class (see Chapter 16).

# **CODE READABILITY**

It's time for another sidebar on code quality. For Ex17_02, we used the following implementation of the operator[]() template for our Array<> class template:

```
```cpp
template <typename T, int startIndex>
const T& Array<T, startIndex>::operator[](int index) const
{
  if (index < startIndex)
    throw std::out_of_range {"Index too small: " + std::to_string(index)};

  if (index > startIndex + static_cast<int>(m_size) - 1)
    throw std::out_of_range {"Index too large: " + std::to_string(index)};

  return m_elements[index - startIndex];
}
```
```