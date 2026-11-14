
TPara is substituted by the unqualified argument type—here int and unique_ptr<int>—and the type of p is the corresponding rvalue reference.

When we call f4 with an lvalue like i or j, the compiler accepts these arguments as template rvalue-reference parameters. The type parameter TPara is substituted by int& and this is also the type of p. How is this possible? The explanation is found in Table 3-1, which shows how references of references are collapsed.

The résumé of Table 3-1 is that references are collapsed to an lvalue reference when at least one of them is an lvalue reference (loosely said, very loosely, we can take the minimal number of ampersands). This explains the handling of lvalues in f4. TPara is substituted by int& and an rvalue reference thereof is int&&, too.

The lack of type substitution is the reason why the non-template rvalue references do not accept lvalues. The only reason why the function parameter can be an lvalue is that an lvalue reference is introduced by the substitution. Without this substitution, no lvalue reference is involved and references are not collapsed.

A more detailed and more dramatic telling of the whole type deduction story is found in [32, pages 9-35 and 157-214].

### 3.1.2.4 Perfect Forwarding

We have already seen that lvalues can be turned into rvalues with move (§2.3.5.4). This time we want to cast them conditionally. A forward reference parameter accepts both rvalue and lvalue arguments that are held by rvalue and lvalue references respectively. When we pass such a reference parameter to another function, we want the lvalue reference to be passed as an lvalue and the rvalue reference to be passed as an lvalue and the rvalue reference as an rvalue. However, the references themselves are lvalues in both cases (since they have names). We could cast a reference to an rvalue with move but this would also apply to an lvalue reference.

Here, we need a conditional cast. This is achieved by std::forward. It casts an rvalue reference into an rvalue and leaves an lvalue as it is. forward must be instantiated with the (unqualified) type parameter, e.g.:

```cpp
template <typename TPara>
void f5(TPara&& p)
{
    f4(forward<TPara>(p));
}
```

The argument of f5 is passed with the same value category to f4. Whatever was passed as an lvalue to f5 is passed as an lvalue to f4; likewise for every rvalue. Like move, forward is a pure cast and does not generate a single machine operation. People have phrased this as: move does not move and forward does not forward. They rather cast their arguments to be moved or forwarded.

| | & | && |
|---|---|---|
| T& | T& | T& |
| T&& | T& | T&& |

### 3.1.3 Dealing with Errors in Templates

Back to our max example that works for all numeric types. But what happens with types that provide no operator<, for instance, std::complex<>? Let us try to compile the following snippet:

```cpp
std::complex<float> z(3, 2), c(4, 8);
std::cout << "The maximum of c and z is " << ::max(c, z) << '\n';
```

Our compilation attempt will end in an error like this:

> Error: no match for >operator<< in >>a >> b<

What happens when our template function calls another template function which in turn calls another one when ... and so on? Likewise, these functions are only parsed and the complete check is delayed until instantiation. Let us look at the following program:

```cpp
int main ()
{
    vector<complex<float> > v;
    sort(v.begin(), v.end());
}
```

Without going into detail, the problem is the same as before: we cannot compare complex numbers and thus we are unable to sort arrays of them. This time the missing comparison is discovered in an indirectly called function, and the compiler provides us the entire call and include stack so that we can trace back the error. Please try to compile this example on different compilers and see if you can make any sense out of the error messages.

If you run into such a lengthy error message, don't panic! First, look at the error itself and take out what is useful for you: e.g., missing operator>, or something not assignable, or something that is const that should not be. Then find in the call stack the innermost code that is the part of your program, i.e., the location where you call a template function from the standard or a third-party library. Stare for a while at this code and its preceding lines because this is the most likely place where the error occurred (in our experience). Then ask yourself: Does a type of the function's template arguments miss an operator or a function according to the error message?

Do not get scared to the point that you decide not to use templates for the rest of your life. In most cases, the problem is much simpler than the never-ending error message makes us believe. In our experience, most errors in template functions can be found faster than run-time errors—with some training.

### 3.1.4 Mixing Types

Another question that we have not answered so far: What happens with our function max when we use two different types as arguments?

```cpp
unsigned ui = 2;
int i = 3;
std::cout << "The maximum of ui and i is " << max(ui, i) << '\n';
```

The compiler tells us—this time surprisingly briefly—something like

> Error: no match for function call 'max(unsigned int&, int)'

Indeed, we assumed that both types are equal. But wait, does not C++ convert arguments implicitly when no exact match exists? Yes, it does, but not for template arguments. The template mechanism is supposed to provide enough flexibility on the type level. In addition, combining template instantiation with implicit conversion has such a high potential for ambiguities.

So far so bad. Can we write a function template with two template parameters? Of course we can. But this creates a new problem: What should be the return type of this template? There are different options. First, we could add a non-templated function overload like

```cpp
int inline max (int a, int b) { return a > b ? a : b; }
```

This can be called with mixed types and the unsigned argument would be implicitly converted into an int. But what would happen if we also added another function overload for unsigned?

```cpp
int max(unsigned a, unsigned b) { return a > b ? a : b; }
```

Will the int be converted into an unsigned or vice versa? The compiler does not know and will complain about this ambiguity.

At any rate, adding non-templated overloads to the template implementation is far from being elegant or productive. So, we remove all non-template overloads and look first at what we can do in the function call. We can explicitly convert one argument to the type of the other argument:

```cpp
unsigned ui = 2;
int i = 3;
std::cout << "max of ui and i is " << max(int(ui), i) << '\n';
```

Now, max is called with two ints. Yet another option is specifying the template type explicitly in the function call:

```cpp
std::cout << "max of ui and i is " << max<int>(ui, i) << '\n';
```

Then both parameters are int and the function template's instance can be called when both arguments are either int or implicitly convertible to int.

After these less pleasant details on templates, some really good news: template functions perform as efficiently as their non-template counterparts! The reason is that C++ generates new code for every type or type combination that the function is called with. Java in contrast compiles templates only once and executes them for different types by casting them to the corresponding types. This results in faster compilation and shorter executables but takes more runtime.

Another price we have to pay for the fast templates is that we have longer executables because of the multiple instantiations for each type (combination). In extreme (and rare) cases, larger binaries can lead to slower execution when the faster memory[^4] is filled with assembly instructions and the data must be loaded from and stored to slower memory instead. However, in practice the number of a function's instances will not be that large, and it only matters for large functions not inlined. For inlined functions, the binary code is at any rate inserted directly in the executable at the location of the function call so the impact on the executable length is the same for template and non-template functions.

### 3.1.5 Uniform Initialization

Uniform initialization (from §2.3.4) works with templates as well. However, in extremely rare cases, the brace elimination can cause some astonishing behavior. If you are curious or have already experienced some surprises, please read Appendix A, Section A.6.1.

### 3.1.6 Automatic return Type

C++11 introduced lambdas with automatic return types whereas the return type of functions is still mandatory. In C++14, we can let the compiler deduce the return type:

```cpp
template <typename T, typename U>
inline auto max (T a, U b)
{
    return a > b ? a : b;
}
```

The return type is deduced from the expression in the return statement in the same fashion as parameters of function templates are deduced from the arguments. If the function contains multiple return statements, their deduced types must all be equal. In template libraries, sometimes simple functions have rather lengthy return type declarations—possibly even longer than the function body—and it is then a great relief for the programmer not to have to spell them out.

## 3.2 Namespaces and Function Lookup

Namespaces are not a sub-topic of generic programming (in fact they are orthogonal to it).
However, they become more important in the presence of function templates, so this is a good place in the book to talk about them.

### 3.2.1 Namespaces

The motivation for namespaces is that common names like min, max, or abs can be defined in different contexts so the names are ambiguous. Even names that are unique when the function or class is implemented can collide later when more libraries are included or an included library evolves. For instance, there is typically a class named window in a GUI implementation, and there might be one in a statistics library. We can distinguish them by namespaces:

[^4]: L2 and L3 caches are usually shared between data and instructions.
