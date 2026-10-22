must be the last template parameter. Function templates have a weaker restriction: Multiple template parameter packs are permitted, as long as each template parameter subsequent to a template parameter pack either has a default value (see the next section) or can be deduced (see Chapter 15): Click here to view code image

```
template<typename... Types, typename Last>
class LastType; // ERROR: template parameter pack is not the last template parameter

template<typename... TestTypes, typename T>
void runTests(T value); // OK: template parameter pack is followed
// by a deducible template parameter
template<unsigned...> struct Tensor;
template<unsigned... Dims1, unsigned... Dims2>
auto compose(Tensor<Dims1...>, Tensor<Dims2...>);
// OK: the tensor dimensions can be deduced
```

The last example is the declaration of a function with a deduced return type—a C++14 feature. See also Section 15.10.1 on page 296.

Declarations of partial specializations of class and variable templates (see Chapter 16) can have multiple parameter packs, unlike their primary template counterparts. That is because partial specialization are selected through a deduction process that is nearly identical to that used for function templates.

Click here to view code image

```
template<typename...> Typelist;
template<typename X, typename Y> struct Zip;
template<typename... Xs, typename... Ys>
struct Zip<Typelist<Xs...>, Typelist<Ys...>>;
// OK: partial specialization uses deduction to determine
// the Xs and Ys substitutions
```

Perhaps not surprisingly, a type parameter pack cannot be expanded in its own parameter clause. For example: Click here to view code image

```
template<typename... Ts, Ts... vals> struct StaticValues {};
// ERROR: Ts cannot be expanded in its own parameter list
```

However, nested templates can create similar valid situations: Click here to view code image

```
template<typename... Ts> struct ArgList {
template<Ts... vals> struct Vals {};
};
ArgList<int, char, char>::Vals<3, 'x', 'y'> tada; A template that contains a template parameter pack is called a variadic template because it accepts a variable number of template arguments. Chapter 4 and Section 12.4 on page 200 describe the use of variadic templates.
```