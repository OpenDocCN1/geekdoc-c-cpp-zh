The most annoying aspect of this is that the compiler obviously already knows the *iterator* type for the *list* and the *size_type* for the *vector*. Why should we have to tell the compiler what it already knows? Doing so just annoys the poor typists among us and opens opportunities for mistakes. Fortunately, we don't have to: we can declare a variable *auto*, meaning use the type of the *iterator* as the type of the variable:

```
template<typename T>       // requires Element<T>()
void user(vector<T>& v, list<T>& lst)
{

    for (auto p = v.begin(); p!=v.end(); ++p) cout << *p << "\n";

    auto q = find(lst.begin(), lst.end(),T{42});
}
```

Here, **p** is a *vector<T>::iterator* and **q** is a *list<T>::iterator*. We can use *auto* in just about every definition that includes an initializer. For example:

```
auto x = 123;     // x is an int
auto c = 'y';     // c is a char
auto& r = x;      // r is an int&
auto y = r;       // y is an int (references are implicitly dereferenced)
```

Note that a string literal has the type *const char\**, so using *auto* for string literals might lead to an unpleasant surprise:

```
auto s1 = "San Antonio";       // s1 is a const char* (Surprise!?)
string s2 = "Fredricksburg";   // s2 is a string
```

When we know exactly which type we want, we can often say so as easily as we can use *auto*.

One common use of *auto* is to specify the loop variable in a range-**for**-loop. Consider:

```
template<typename C>       // requires Container<T>
void print3(const C& cont)
{

    for (const auto& x : cont)
        cout << x << "\n";
}
```