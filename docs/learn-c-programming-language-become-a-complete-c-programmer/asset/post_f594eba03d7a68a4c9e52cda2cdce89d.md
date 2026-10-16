
```cpp
sqrt(2); // sqrt<int>(int)
sqrt(2.0); // sqrt(double)
sqrt(z); // sqrt<double>(complex<double>)
}
```

In the same way that a function template is a generalization of the notion of a function, the rules for resolution in the presence of function templates are generalizations of the function overload resolution rules. Basically, for each template we find the specialization that is best for the set of function arguments. Then, we apply the usual function overload resolution rules to these specializations and all ordinary functions (§iso.14.8.3):

- [1] Find the set of function template specializations (§23.2.2) that will take part in overload resolution. Do this by considering each function template and deciding which template arguments, if any, would be used if no other function templates or functions of the same name were in scope. For the call `sqrt(z)`, this makes `sqrt<double>(complex<double>)` and `sqrt<complex<double>>(complex<double>)` candidates. See also §23.5.3.2.

- [2] If two function templates can be called and one is more specialized than the other (§25.3.3), consider only the most specialized template function in the following steps. For the call `sqrt(z)`, this means that `sqrt<double>(complex<double>)` is preferred over `sqrt<complex<double>>(complex<double>)`: any call that matches `sqrt<T>(complex<T>)` also matches `sqrt<T>(T)`.

- [3] Do overload resolution for this set of functions, plus any ordinary functions, as for ordinary functions (§12.3). If a function template’s argument has been determined by template argument deduction (§23.5.2), that argument cannot also have promotions, standard conversions, or user-defined conversions applied. For `sqrt(2)`, `sqrt<int>(int)` is an exact match, so it is preferred over `sqrt(double)`.

- [4] If a function and a specialization are equally good matches, the function is preferred. Consequently, `sqrt(double)` is preferred over `sqrt<double>(double)` for `sqrt(2.0)`.

- [5] If no match is found, the call is an error. If we end up with two or more equally good matches, the call is ambiguous and is an error.

For example:

```cpp
template<typename T>
T max(T,T);
const int s = 7;

void k() {
    max(1,2); // max<int>(1,2)
    max('a','b'); // max<char>('a','b')
    max(2.7,4.9); // max<double>(2.7,4.9)
    max(s,7); // max<int>(int{s},7) (trivial conversion used)

    max('a',1); // error: ambiguous: max<char,char>() or max<int,int>()?
    max(2.7,4); // error: ambiguous: max<double,double>() or max<int,int>()?
}
```

The problem with the last two calls is that we don’t apply promotions and standard conversions until after template parameters have been uniquely determined. There is no rule telling the compiler to prefer one resolution over the other. In most cases, it is probably good that the language rules leave subtle decisions in the hands of the programmer. The alternative to surprising ambiguity errors is surprising results from unexpected resolutions. People’s “intuitions” about overload resolution differ dramatically, so it is impossible to design a perfectly intuitive set of overload resolution rules.

## 23.5.3.1 Ambiguity Resolution

We could resolve the two ambiguities by explicit qualification:

```cpp
void f()
{
    max<int>('a',1); // max<int>(int('a'),1)
    max<double>(2.7,4); // max<double>(2.7,double(4))
}
```

Alternatively, we could add suitable declarations:

```cpp
inline int max(int i, int j) { return max<int>(i,j); }
inline double max(int i, double d) { return max<double>(i,d); }
inline double max(double d, int i) { return max<double>(d,i); }
inline double max(double d1, double d2) { return max<double>(d1,d2); }
```

```cpp
void g() {
    max('a',1); // max(int('a'),1)
    max(2.7,4); // max(2.7,4)
}
```

For ordinary functions, ordinary overloading rules (§12.3) apply, and the use of `inline` ensures that no extra overhead is imposed.

The definition of `max()` is trivial, so we could have implemented the comparison directly rather than calling a specialization of `max()`. However, using an explicit specialization of the template is an easy way of defining such resolution functions and can help maintenance by avoiding almost identical code in several functions.

## 23.5.3.2 Argument Substitution Failure

When looking for a best match for a set of arguments for a function template, the compiler considers whether the argument can be used in the way required by the complete function template declaration (including the return type). For example:

```cpp
template<typename Iter>
typename Iter::value_type mean(Iter first, Iter last);
```

```cpp
void f(vector<int>& v, int * p, int n) {
    auto x = mean(v.begin(),v.end()); // OK
    auto y = mean(p,p+n); // error
}
```

Here, the initialization of `x` succeeds because the arguments match and `vector<int>::iterator` has a member called `value_type`. The initialization of `y` fails because even though the arguments match, `int*` does not have a member called `value_type`, so we cannot say:

```cpp
int*::value_type mean(int*, int*); // int* does not have a member called value_type
```

However, what if there were another definition of `mean()`?

```cpp
template<typename Iter>
typename Iter::value_type mean(Iter first, Iter last); // #1

template<typename T>
T mean(T*,T*); // #2
```

```cpp
void f(vector<int>& v, int * p, int n) {
    auto x = mean(v.begin(),v.end()); // OK: call #1
    auto y = mean(p,p+n); // OK: call #2
}
```

This works: both initializations succeed. But why didn’t we get an error when trying to match `mean(p,p+n)` with the first template definition? The arguments match perfectly, but by substituting in the actual template argument (`int*`), we get the function declaration:

```cpp
int*::value_type mean(int*, int*); // int* does not have a member called value_type
```

That is garbage, of course: a pointer does not have a member `value_type`. Fortunately, considering this possible declaration is not by itself an error. There is a language rule (§iso.14.8.2) that says that such a substitution failure is not an error. It simply causes the template to be ignored; that is, the template does not contribute a specialization to the overload set. That done, `mean(p,p+n)` matches declaration #2, which is called.

Without the “substitution error is not a failure” rule, we would get compile-time errors even when error-free alternatives (such as #2) are available. More, this rule gives us a general tool for selecting among templates. Techniques based on this rule are described in §28.4. In particular, the standard library provides `enable_if` to simplify conditional definition of templates (§35.4.2).

The rule is known under the unpronounceable acronym SFINAE (Substitution Failure Is Not An Error). SFINAE is often used as a verb with the “F” pronounced as a “v”: “I SFINAE'd away that constructor.” That sounds quite impressive, but I tend to avoid this jargon. “The constructor was eliminated by a substitution failure” is clearer for most people and does less violence to the English language.

So, if – in the process of generating a candidate function to resolve a function call – the compiler finds itself generating a template specialization that would be nonsensical, that candidate is not entered into the overload set. A template specialization is considered nonsensical if it would lead to a type error. In this, we consider only a declaration; template function definitions and the definition of class members are not considered (or generated) unless they are actually used. For example:

```cpp
template<typename Iter>
Iter mean(Iter first, Iter last) // #1
{
    typename Iter::value_type v = *first; // ...
}

template<typename T>
T* mean(T*,T*); // #2
```

```cpp
void f(vector<int>& v, int * p, int n) {
    auto x = mean(v.begin(),v.end()); // OK: call #1
    auto y = mean(p,p+n); // error: ambiguous
}
```

The declaration of `mean()` #1 is fine for `mean(p,p+n)`. The compiler does not start to instantiate the body of that `mean()` and eliminate it because of the type error.

Here, the result is an ambiguity error. Had `mean()` #2 not been present, declaration #1 would have been chosen and we would have suffered an instantiation-time error. Thus, a function may be chosen as the best match yet still fail to compile.

## 23.5.3.3 Overloading and Derivation

The overload resolution rules ensure that function templates interact properly with inheritance:

```cpp
template<typename T>
class B {/*...*/};
template<typename T>
class D : public B<T> {/*...*/};
template<typename T> void f(B<T>*);
void g(B<int>* pb, D<int>* pd) {
    f(pb); // f<int>(pb) of course
    f(pd); // f<int>(static_cast<B<int>*>(pd));
           // standard conversion D<int>* to B<int>* used
}
```

In this example, the function template `f()` accepts a `B<T>*` for any type `T`. We have an argument of type `D<int>*`, so the compiler easily deduces that by choosing `T` to be `int`, the call can be uniquely resolved to a call of `f(B<int>*)`.

## 23.5.3.4 Overloading and Non-Deduced Parameters

A function argument that is not involved in the deduction of a template parameter is treated exactly as an argument of a non-template function. In particular, the usual conversion rules hold. Consider:

```cpp
template<typename T, typename C>
T get_nth(C& p, int n); // get the nth element
```
