```
```cpp
template<typename T, typename R2>
Array<T, A_Mult<T,A_Scalar<T>,R2>>
operator* (T const& s, Array<T,R2> const& b) {
  return Array<T,A_Mult<T,A_Scalar<T>,R2>>
    (A_Mult<T,A_Scalar<T>,R2>(A_Scalar<T>(s), b.rep()));
}

// multiplication of Array and scalar, addition of scalar and Array
// addition of Array and scalar:
...
```
```

The declaration of these operators is somewhat cumbersome (as can be seen from these examples), but the functions really don’t do much. For example, the plus operator for two arrays first creates an A_Add<> object that represents the operator and the operands

```
```cpp
A_Add<T,R1,R2>(a.rep(),b.rep())
```
```

and wraps this object in an Array object so that we can use the result as any other object that represents data of an array:

```
```cpp
return Array<T,A_Add<T,R1,R2>> (...);
```
```

For scalar multiplication, we use the A_Scalar template to create the A_Mult object

```
```cpp
A_Mult<T,A_Scalar<T>,R2>(A_Scalar<T>(s), b.rep())
```
```

and wrap again:

```
```cpp
return Array<T,A_Mult<T,A_Scalar<T>,R2>> (...);
```
```

Other nonmember binary operators are so similar that macros can be used to cover most operators with relatively little source code. Another (smaller) macro could be used for nonmember unary operators.

# 27.2.4 Review

On first discovery of the expression template idea, the interaction of the various declarations and definitions can be daunting. Hence, a top-down review of what happens with our example code may help crystallize understanding. The code we will analyze is the following (you can find it as part of `meta/exprmain.cpp`):

```
```cpp
int main()
{
Array<double> x(1000), y(1000);
...
```
```