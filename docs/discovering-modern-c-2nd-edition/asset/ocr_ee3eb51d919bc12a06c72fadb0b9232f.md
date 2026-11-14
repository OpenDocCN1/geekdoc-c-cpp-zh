(including variadic implementations, §3.11) is the application operator: `operator()`.

Another freedom that the language provides us is the choice of the arguments’ types. We can, for instance, implement a subscription operator for an `unsigned` (returning a single element), for a range (returning a sub-vector), and for a set (returning a set of vector elements). This is indeed realized in MTL4. Compared to MATLAB, C++ offers fewer operators, but we have the unlimited opportunity of overloading them infinitely to create every amount of functionality we like.

# 2.7.2 Respect the Priority

When we implement operators ourselves, we need to make sure that the priorities in C++ match those of the application domain. For instance, we might have the idea of using the Lᴬᵀᴱᵀ notation for exponentiation of matrices:

```
A = B^2;
```

A is B squared. So far so good. That the original meaning of ^ is a bitwise exclusive OR does not worry us as we never planned to implement bitwise operations on matrices. Now we add C to B^2:

```
A = B^2 + C;
```

Looks nice. But it does not work (or does something weird). Why? Because + has a higher priority than ^ in C++. Thus, the compiler understands our expression as:

```
A = B ^ (2 + C);
```

Oops. Although the operator notation gives a concise and intuitive interface, some expressions don’t meet our expectations. Therefore:

> **Respect Priorities**
> Pay attention that the semantic/intended priority of your overloaded operators matches the priorities of C++ operators.

# 2.7.3 Member or Free Function