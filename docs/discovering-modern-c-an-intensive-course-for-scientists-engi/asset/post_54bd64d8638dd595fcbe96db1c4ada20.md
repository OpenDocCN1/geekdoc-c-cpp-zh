

else
    return b;
}

This function template replaces the non-template overloads and we keep the name max. It can be used in the same fashion as the overloaded functions:

```
std::cout << "The maximum of 3 and 5 is " << max(3, 5) << '\n';
std::cout << "The maximum of 3l and 5l is " << max(3l, 5l) << '\n';
std::cout << "The maximum of 3.0 and 5.0 is " << max(3.0, 5.0) << '\n';
```

In the first case, 3 and 5 are literals of type int and the max function is Instantiated to

```
int max (int, int);
```

Likewise the second and third calls of max instantiate:

```
long max (long, long);
double max (double, double);
```

since the literals are interpreted as long and double. In the same way, the template function can be called with variables and expressions:

```
unsigned u1 = 2, u2 = 8;
std::cout << "The maximum of u1 and u2 is " << max(u1, u2) << '\n';
std::cout << "The maximum of u1+u2 and u1+u2 is "
<< max(u1*u2, u1+u2) << '\n';
```

Here the function is instantiated for unsigned.

Instead of typename, one can also write class in this context, but we do not recommend this because typename expresses the intention of generic functions better.

## 3.1.1 Instantiation

What does Instantiation mean? For a non-generic function, the compiler reads its definition, checks for errors, and generates executable code. When the compiler processes a generic function's definition, it can only detect errors that are independent of the template parameters like parsing errors. For instance:

```
template <typename T>
inline T max (T a, T b)
{
    if a > b      // Error !
        return a;
    else
        return b;
}
```

would not compile because the if-statement without the parentheses is not a legal expression of the C++ grammar.

However, most errors we encounter depend on the substituted types. For instance, the following implementation would compile:

```
template <typename T>
inline T max(T x, T y)
{
    return x < y ? y.value : x.value;
}
```

We could not call it with any intrinsic type like int or double, but the function template might not be intended for intrinsic types and may work with the actual argument types.

The compilation of the function template itself does not generate any code in the binary. This only happens when we call it. In this case, we instantiate this function template. Only then the compiler performs a complete check of whether the generic function is correct for the given argument type(s). In our previous examples, we saw that max can be instantiated with int and double.

So far, we have seen the most implicit form: the template is instantiated when a call exists and the type parameter is deduced from the arguments. To be more explicit, we can declare the type that substitutes the template parameter, e.g.:

```
std::cout << max<float>(8.1, 9.3) << '\n';
```

Here, the template is explicitly instantiated with a given type. In the most explicit form, we force an instantiation without a function call:

```
template short max<short>(short, short);
```

This can be useful when we generate object files (§7.2.1.3) and must guarantee that certain instances are present, regardless of the function calls in the compile unit.

> Definition 3-1. For conciseness, we call an instantiation with type deduction Implicit Instantiation and an instantiation with an explicit type declaration Explicit Instantiation.

In our experience, implicit instantiation works in most cases as expected. The explicit nomination of the instantiation type is mostly needed for disambiguation and special usages like std::forward (§3.1.2.4). For a deeper understanding of templates, it is very helpful to know how the compiler substitutes the types.

## 3.1.2 Parameter Type Deduction

```
=> c++11/template_type_deduction.cpp
```

In this section, we will have a closer look at how template parameters are substituted depending on whether the arguments are passed by value, value, or rvalue reference. This knowledge is even more important when variables are declared with an automatic type via auto as shown in Section 3.4.1. However, the substitution rules are more intuitive with function parameters than with auto variables and we therefore discuss them here.

### 3.1.2.1 Value Parameters

In the previous example, we used the type parameter T directly as a function parameter in max:

```
template <typename T>
T max (T a, T b);
```

Like any other function parameter, those of function templates can be const- and reference-qualified as well:

```
template <typename T>
T max (const T& a, const T& b);
```

Let us denote this (without loss of generalization) for a unary void function f:

```
template <typename TPara>
void f(TPara p);
```

where FPara contains TPara. When we call f(arg), the compiler has to Deduce the type TPara such that parameter p can be initialized with arg. This is the whole story in a nutshell. But let us look at some cases to get a feeling for it. The easiest syntactical case is the equality of TPara and FPara:

```
template <typename TPara>
void f1(TPara p);
```

This means the function parameter is a local copy of the argument. We call f1 with an int literal, an int variable, and a mutable and constant int reference:

```
template <typename TPara>
void f1(TPara p) {}
```

```
int main ()
{
    int i = 0;
    int& j = i;
    const int& k = i;

    f1(3);
    f1(i);
    f1(j);
    f1(k);
    ...
}
```

In all four instantiations, TPara is substituted with int so that the type of the function parameter p is int as well. If TPara was substituted with int& or const int&, the arguments could be passed in as well. But then we would have no value semantics since a modification of p would affect the function argument (e.g., j). Thus, when the function parameter is a type parameter without qualification, TPara becomes the argument type where all qualifiers are removed. This template function accepts all arguments as long as their types are copyable.

For instance, unique_ptr has a deleted copy constructor and can only be passed to this function as an rvalue:

```
unique_ptr<int> up;
// f1(up); // Error: no copy constructor
f1(move(up)); // Okay: use move constructor
```

### 3.1.2.2 Lvalue-Reference Parameters

To really accept every argument, we can use a constant reference as a parameter:

```
template <typename TPara>
void f2(const TPara& p) {}
```

TPara is again the argument type with all qualifiers stripped off. Thus, p is a constant reference of the unqualified argument type so we cannot modify p.

A more interesting case is the mutable reference as a parameter:

```
template <typename TPara>
void f3(TPara& p) {}
```

This function rejects all literals and temporaries as they are not referable.1 We can phrase this also in terms of type substitution: the temporaries are refused because there exists no type for TPara such that TPara&& becomes int&& (we will come back to this when we talk about reference collapsing in Section 3.1.2.3).

When we pass in an ordinary int variable like i, TPara is substituted by int so p has the type int&& and refers to i. The same substitution can be observed when a mutable reference variable like j is passed. What happens when we pass a const int or const int& like k? Can this be matched with TPara&&? Yes, it can, when TPara is substituted with const int. Accordingly, the type of p is const int&&. Thus, the type pattern TPara&& does not limit the arguments to mutable references. The pattern can match constant references. However, if the function modifies p, the instantiation would fail later.

### 3.1.2.3 Forward References

In Section 2.3.5.1, we introduced rvalue references that only accept rvalues as arguments. Rvalue references with a type parameter of the form T&& accept lvalues as well. For this reason, Scott Meyers coined the term Universal Reference for them. Here we stick with the standard term Forward Reference. We will show why they can accept both rvalues and lvalues. To this end, we look at the type substitution of the following unary function:

```
template <typename TPara>
void f4(TPara&& p) {}
```

When we pass an rvalue to this function, e.g.:

```
f4(3);
f4(move(i));
f4(move(up));
```
