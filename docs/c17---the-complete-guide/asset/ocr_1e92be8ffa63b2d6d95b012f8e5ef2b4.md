```
((1 + 2) + 3)
```

This also means that the following example compiles:

```
std::cout << foldSumL(std::string("hello"), "world", "!") << '\n'; // OK
```

Remember that operator + is defined for standard strings provided at least one operand is a std::string. Because the left fold is used, the call first evaluates

```
std::string("hello") + "world"
```

which returns a std::string, so that adding the string literal "!" is then also valid.

However, a call such as

```
std::cout << foldSumL("hello", "world", std::string("!")) << '\n'; // ERROR
```

will not compile because it evaluates to

```
("hello" + "world") + std::string("!")
```

and adding two string literals is not allowed.

However, if we change the implementation to:

```
template<typename... T>
auto foldSumR(T... args){
    return (args + ...);  // (arg1 + (arg2 + arg3))...
}
```

the call

```
foldSumR(1, 2, 3)
```

evaluates to:

```
(1 + (2 + 3))
```

which means that the following example no longer compiles:

```
std::cout << foldSumR(std::string("hello"), "world", "!") << '\n';  // ERROR
```

while the following call does now compile:

```
std::cout << foldSumR("hello", "world", std::string("!")) << '\n';  // OK
```

In almost all cases, evaluation from left to right is the intention. Therefore, the left fold syntax with the parameter pack at the end should usually be preferred:

```
(... + args);  // preferred syntax for fold expressions
```

# 11.2.1 Dealing with Empty Parameter Packs

If a fold expression is used with an empty parameter pack, the following rules apply:

+   - If operator && is used, the value is true.
+   - If operator || is used, the value is false.
+   - If the comma operator is used, the value is void().
+   - For all other operators, the call is ill-formed.

For all other cases (and in general), you can add an initial value: given a parameter pack args, an initial value value, and an operator op, C++17 also allows us to write