

```cpp
template<typename T>
using Iterator_category = typename std::iterator_traits<T>::iterator_category;
```
The example cleans up nicely:
```
```cpp
template<typename Iter>
Iter search(Iter p, iter q, Value_type<Iter> val)
{
  Difference_type<Iter> m = q-p;
  // ...
}
```
```

I suspect that traits are currently overused. Consider how to write the previous example without any mention of traits or other type functions:
```
```cpp
template<typename Iter, typename Val>
Iter search(Iter p, iter q, Val val)
{
  auto x = *p; // if we don’t need to name *p’s type
  auto m = q-p; // if we don’t need to name q-p’s type
  using value_type = decltype(*p); // if we want to name *p’s type
  using difference_type = decltype(q-p); // if we want to name q-p’s type
  // ...
}
```
```

Of course, **decltype()** is a type function, so all I did was to eliminate user-defined and standard library type functions. Also, **auto** and **decltype** are new in C++11, so older code could not have been written this way.

We need a trait (or equivalent, such as **decltype()**) to associate a type with another type, such as a **value_type** with a **T***. For that, a trait (or an equivalent) is indispensable for non-intrusively adding type names needed for generic programming or metaprogramming. When a trait is used simply to provide a name for something that already has a perfectly good name, such as **pointer** for **value_type*** and **reference** for **value_type&**, the utility is less clear and the potential for confusion greater. Don’t blindly define traits for everything “just in case.”

## 28.3 Control Structures

To do general computation at compile time, we need selection and recursion.

### 28.3.1 Selection

In addition to what is trivially done using ordinary constant expressions (§10.4), I use:
- **Conditional**: a way of choosing between two types (an alias for **std::conditional**)
- **Select**: a way of choosing among several types (defined in §28.3.1.3)

These type functions return types. If you want to choose among values, ?: is sufficient; **Conditional** and **Select** are for selecting types. They are not simply compile-time equivalents to **if** and **switch** even though they can appear to be when they are used to choose among function objects (§3.4.3, §19.2.2).

### 28.3.1.1 Selecting between Two Types

It is surprisingly simple to implement **Conditional**, as used in §28.2. The **conditional** template is part of the standard library (in **<type_traits>**), so we don’t have to implement it, but it illustrates an important technique:
```
template<bool C, typename T, typename F> // general template
struct conditional {
using type = T;
};

template<typename T, typename F> // specialization for false
struct conditional<false,T,F> {
using type = F;
};
```

The primary template (§25.3.1.1) simply defines its **type** to be **T** (the first template parameter after the condition). If the condition is not **true**, the specialization for **false** is chosen and **type** is defined to be **F**. For example:
```
typename conditional<(std::is_polymorphic<T>::value),X,Y>::type z;
```

Obviously, the syntax leaves a bit to be desired (§28.2.2), but the underlying logic is beautiful.

Specialization is used to separate the general case from one or more specialized ones (§25.3). In this example, the primary template takes care of exactly half of the functionality, but that fraction can vary from nothing (every nonerroneous case is handled by a specialization; §25.3.1.1) to all but a single terminating case (§28.5). This form of selection is completely compile-time and doesn’t cost a byte or a cycle at run time. To improve the syntax, I introduce a type alias:
```
template<bool B, typename T, typename F>
using Conditional = typename std::conditional<B,T,F>::type;
```

Given that, we can write:
```
Conditional<(Is_polymorphic<T>()),X,Y> z;
```

I consider that a significant improvement.

### 28.3.1.2 Compile Time vs. Run Time

Looking at something like
```
Conditional<std::is_polymorphic<T>::value,X,Y> z;
```
for the first time, it is not uncommon for people to think, “Why don’t we just write a normal **if**?” Consider having to choose between two alternatives, **Square** and **Cube**:
```
struct Square {
constexpr int operator()(int i) { return i*i; }
};
```
```
struct Cube {
constexpr int operator()(int i) { return i*i*i; }
};
```

We might try the familiar **if**-statement:
```
if (My_cond<T>())
    using Type = Square;
else

// error: declaration as if-statement branch
using Type = Cube; // error: declaration as if-statement branch
Type x; // error: Type is not in scope
```

A declaration cannot be the only statement of a branch of an **if**-statement (§6.3.4, §9.4.1), so this will not work even though **My_cond<T>()** is computed at compile time. Thus, an ordinary **if**-statement is useful for ordinary expressions, but not for type selection.

Let us try an example that doesn’t involve defining a variable:
```
Conditional<My_cond<T>(),Square,Cube>{}(99); // invoke Square{}(99) or Cube{}(99)
```

That is, select a type, construct a default object of that type, and call it. That works. Using “conventional control structures,” this would become:
```
((My_cond<T>())?Square:Cube{})(99);
```

This example doesn’t work because **Square{}(99)** and **Cube{}(99)** do not yield types, rather than values of types that are compatible in a conditional expression (§11.1.3). We could try
```
(My_cond<T>()?Square{}:Cube{})(99); // error: incompatible arguments for ?:
```

Unfortunately, this version still suffers from the problem that **Square{}** and **Cube{}** are not of compatible types acceptable as alternatives in a **?:** expression. The restriction to compatible types is often unacceptable in metaprogramming because we need to choose between types that are not explicitly related.

Finally, this works:
```
My_cond<T>()?Square{}(99):Cube{}(99);
```

Furthermore, it is not significantly more readable than
```
Conditional<My_cond<T>(),Square,Cube>{}(99);
```

### 28.3.1.3 Selecting among Several Types

Selecting among N alternatives is very similar to choosing between two. Here is a type function returning its Nth argument type:
```
class Nil {};
template<int I, typename T1 = Nil, typename T2 = Nil, typename T3 = Nil, typename T4 = Nil> struct select;
template<int I, typename T1 = Nil, typename T2 = Nil, typename T3 = Nil, typename T4 = Nil> using Select = typename select<I,T1,T2,T3,T4>::type;
// Specializations for 0-3:
template<typename T1, typename T2, typename T3, typename T4> struct select<0,T1,T2,T3,T4> { using type = T1; }; // specialize for N == 0
template<typename T1, typename T2, typename T3, typename T4> struct select<1,T1,T2,T3,T4> { using type = T2; }; // specialize for N == 1
template<typename T1, typename T2, typename T3, typename T4> struct
select<2,T1,T2,T3,T4> { using type = T3; }; // specialize for N==2
template<typename T1, typename T2, typename T3, typename T4>
struct select<3,T1,T2,T3,T4> { using type = T4; }; // specialize for N==3
```

The general version of select should never be used, so I didn’t define it. I chose zero-based numbering to match the rest of C++. This technique is perfectly general: such specializations can present any aspect of the template arguments. We don’t really want to pick a maximum number of alternatives (here, four), but that problem can be addressed using variadic templates (§28.6). The result of picking a nonexisting alternative is to use the primary (general) template. For example:
```
Select<5,int,double,char> x;
```

In this case, that would lead to an immediate compile-time error as the general Select isn’t defined.

A realistic use would be to select the type for a function returning the Nth element of a tuple:
```
template<int N, typename T1, typename T2, typename T3, typename T4>
Select<N,T1,T2,T3,T4> get(Tuple<T1,T2,T3,T4> & t); // see §28.5.2
```
```
auto x = get<2>(t); // assume that t is a Tuple
```

Here, the type of x will be whatever T3 is for the Tuple called t. Indexing into tuples is zero-based.

Using variadic templates (§28.6), we can provide a far simpler and more general select:
```
template<unsigned N, typename... Cases> // general case; never instantiated
struct select;
```
```
template<unsigned N, typename T, typename ... Cases> struct select<N,T,Cases...>
:select<N-1,Cases...> {};
```
```
template<typename T, typename ... Cases> // final case: N==0 struct
select<0,T,Cases...> {
using type = T;
};
```
```
template<unsigned N, typename... Cases> using Select = typename select<N,Cases...>::type;
```

## 28.3.2 Iteration and Recursion

The basic techniques for calculating a value at compile time can be illustrated by a factorial function template:
```
template<int N>
constexpr int fac()
{
return N*fac<N-1>(); }
```
```
template<>
```
