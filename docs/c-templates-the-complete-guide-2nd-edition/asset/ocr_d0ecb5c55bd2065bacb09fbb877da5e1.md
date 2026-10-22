In this function template, the most complicated part of the lambda (by far) is its parameter type. C++14 introduced the notion of “generic” lambdas, where one or more of the parameter types use auto to deduce the type rather than writing it specifically: Click here to view code image

```
template<typename Iter>
Iter findNegative(Iter first, Iter last)
{
return std::find_if(first, last,
[] (auto value) {
return value < 0;
});
}
```

An auto in a parameter of a lambda is handled similarly to an auto in the type of a variable with an initializer: It is replaced by an invented template type parameter T. However, unlike in the variable case, the deduction isn’t performed immediately because the argument isn’t known at the time the lambda is created. Instead, the lambda itself becomes generic (if it wasn’t already), and the invented template type parameter is added to its template parameter list. Thus, the lambda above can be invoked with any argument type, so long as that argument type supports the < 0 operation whose result is convertible to bool. For example, this lambda could be called with either an int or a float value.

To understand what it means for a lambda to be generic, we first consider the implementation model for a nongeneric lambda. Given the lambda [] (int i) { return i < 0; }

the C++ compiler translates this expression into an instance of a newly invented class specific to this lambda. This instance is called a closure or closure object, and the class is called a closure type. The closure type has a function call operator, and hence the closure is a function object.¹⁶ For this lambda, the closure type would look something like the following (we leave out the conversion function to a pointer-to-function value for brevity and simplicity): Click here to view code image

```
class SomeCompilerSpecificNameX
{
public:
SomeCompilerSpecificNameX(); // only callable by the compiler
bool operator() (int i) const
{
return i < 0;
```