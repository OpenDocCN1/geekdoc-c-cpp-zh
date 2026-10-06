# ISO/IEC 14882:2017(E)

```
// The inner closure type must be a literal type regardless of how reference captures are represented.
static_assert((int n) { return &k; return ++n; }); {3} == 4;
```

-- end example. A bit-field or member of anonymous union shall not be captured by reference.

13 A *lambda-expression* captures an entity and that entity is captured by immediately enclosing lambda-expression m1, then m2's is transformed as follows:

+   (13.1) if m1 captures the entity by, m2 captures the corresponding-static data member of m1's closure type:

+   (13.2) if m2 captures the entity by reference, m2 captures the entity captured by m1.

```
[Example: The nested lambda expressions and invocations below will output 122334.
int a = 1, b = 1, c = 2;
auto m1 = [a, &b, &c]() mutable {
  std::cout << a << b << c;
  a = 4; b = 4; c = 4;
};
a = 3; b = 3; c = 3;
m1();
a = 2; b = 2; c = 2;
m1();
std::cout << a << b << c;
```

-- end example

14 Every occurrence of *decltype*( is treated as if x were transformed into an access to a corresponding data member of the closure type that would have been declared if x were an udr of the denoted entity). [Example:

```
void f0() {
  float x, *r = x;
  {
    decltype(x) y1; // y1 has type float
    decltype(x) y2 = y1; // y2 has type const float because this lambda is not mutable and x is lvalue
    decltype(x) r1 = y1; // r1 has type float (transformation considered)
    decltype(x) r2 = y2; // r2 has type float const
  }
}
```

-- end example

15 When the lambda-expression is initialized, the entities that are captured are used to de-initialize each non-static data member of the resulting closure object, and the non-static data members corresponding to the init-captures are initialized by the corresponding *initializer* (which may be copies or de-initialization). These initializations are performed in the (specified) order in which the non-static data members are declared. [Note: This ensures that the destructors occur in the reverse order of the constructions. -- end note

16 [Note: If a non-reference entity is implicitly or explicitly captured by reference, invoking the function call of the corresponding *lambda-expression* after the lifetime of the entity is likely to result in undefined behavior.-- end note]