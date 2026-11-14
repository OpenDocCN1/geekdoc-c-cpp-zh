These complex numbers of course provide the common operations like addition and multiplication. For unknown reasons, these operations are only provided between the type itself and the underlying real type. Thus, when we write:

```
z2= 2 * z; // Error: no int * complex<float>
z2= 2.0 * z; // Error: no double * complex<float>
```

we will get an error message that the multiplication is not available. More specifically, the compiler will tell us that there is no operator*() for int and std::complex<float> respectively for double and std::complex<float>.1 To get the simple expression above compiled, we must make sure that our value 2 has the type float:

z2= 2.0f * z;

Ambiguity: At some point in this book, we introduced function overloading: a function with different implementations for different argument types (§1.5.4). The compiler selects that function overload which fits best. Sometimes the best fit is not clear, for instance, if function f accepts an unsigned or a pointer and we call:

```
f(0);
```

The literal 0 is considered an int and can be implicitly converted into unsigned or any pointer type. None of the conversions is prioritized. As before, we can address the issue by a literal of the desired type:

```
f(0u);
```

Accuracy: The accuracy issue comes up when we work with long double. On the author's computer, the format can handle at least 19 digits. Let us define 1/3 with 20 digits and print out 19 of them:

```
long double third= 0.33333333333333333333;
cout.precision(19);
cout << "One third is " << third << ".\n";
```

The result is

One third is 0.33333333333333333333148.

The program behavior is more satisfying if we append an l to the number:

```
long double third= 0.33333333333333333333l;
```

yielding the printout that we hoped for:

One third is 0.33333333333333333333.

1. Since the multiplication is implemented as a template function, the compiler does not convert the int and double to float.