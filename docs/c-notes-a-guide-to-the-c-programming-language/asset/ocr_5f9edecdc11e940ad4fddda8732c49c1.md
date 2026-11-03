for the two parts of a **COMPLEX** structure. See [1.7] for the definition of the type named **COMPLEX**.

Any initializer occurring in an external declaration must be a constant expression, but this may include pointer expressions like

```
```c
&c[2].real
```
```

where c has been declared to be a static array of **COMPLEX**. The & operator delivers the location of the variable c[2].real, which can be computed at compile-time. This expression is of type pointer to float and might appear in the declaration

```
```c
static float *fptr = &c[2].real;
```
```

Initializers in local declarations (see Chapter 4) must involve only expressions that can be calculated at entry to the compound statement housing the declarations. Externals may not be initialized in local declarations.

The constants in an initializer are effectively assigned to the corresponding variables, although not all coercions are performed that would be permitted in an assignment (see [3.1]). For example, in the above initializer for vector, the variables vector[0].real and vector[0].imag are initialized by the floating equivalents 0.0 and 1.0 for the integer constants 0 and 1, which are specified. Initializing an integer with a floating literal, on the other hand, is not generally supported.

An external name must not be initialized more than once, although multiple declarations are permitted and even necessary among program files in order to provide inter-program file communication.

Some implementations require that each external declaration be initialized exactly once, to fix the defining instance of the object; others require at least the use of the extern keyword with one declaration, while still others generally will accept the absence of any initializers. The safest practice appears to be to pick one instance of a multiply declared variable as the defining instance; give it the extern attribute explicitly, and give it an initializer, even if it is just 0.