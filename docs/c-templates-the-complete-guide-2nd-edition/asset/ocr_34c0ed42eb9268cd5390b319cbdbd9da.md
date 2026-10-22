```
void f();
template<typename> void f();
namespace N {
class C {
friend int f(); // OK
friend int f<>(); // ERROR: return type conflict
};
}
```

When a plain identifier is used to name a friend function, that function is only looked up within the nearest enclosing scope, and if it is not found there, a new entity is declared in that scope (but it remains “invisible” except when looked up via argument-dependent lookup (ADL); see Section 13.2.2 on page 220). That is what happens with our first friend declaration above: No f is declared within namespace N, and so a new N::f() is “invisibly” declared.

However, when the identifier naming the friend is followed by a template argument list, a template must be visible through normal lookup at that point, and normal lookup will go up any number of scopes that may be required. So, our second declaration above will find the global function template f(), but the compiler will then issue an error because the return types do not match (since no ADL is performed here, the declaration created by the preceding friend function declaration is ignored).

Explicitly specified template arguments are substituted using SFINAE principles: If the substitution leads to an error in the immediate context of that substitution, the function template is discarded, but other templates may still succeed. For example: Click here to view code image

```
template<typename T> typename T::EType f();// #1
template<typename T> T f();// #2

int main() {
auto x = f<int*>();
}
```

Here, substituting int* for T in candidate #1 causes substitution to fail, but in candidate #2 it succeeds, and therefore that is the candidate selected. In fact, if after substitution exactly one candidate remains, then the name of the function template with the explicit template arguments behaves pretty much like an ordinary function name, including decaying to a pointer-to-function type in many contexts. That is, replacing main() above by Click here to view code image

```
int main() {
auto x = f<int*>; // OK: x is a pointer to function
}
```