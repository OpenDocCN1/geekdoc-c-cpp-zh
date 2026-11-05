
named. In other words, non-trailing named arguments are only allowed when the name and the position result in finding the same corresponding parameter. end note

## 12.6.2.3 Run-time evaluation of argument lists

During the run-time processing of a function member invocation (§12.6.6), the expressions or variable references of an argument list are evaluated in order, from left to right, as follows:

- For a value argument, if the parameter's passing mode is value
  - the argument expression is evaluated and an implicit conversion (§10.2) to the corresponding parameter type is performed. The resulting value becomes the initial value of the value parameter in the function member invocation.
  - otherwise, the parameter's passing mode is input. If the argument is a variable reference and there exists an identity conversion (§10.2.2) between the argument's type and the parameter's type, the resulting storage location becomes the storage location represented by the parameter in the function member invocation. Otherwise, a storage location is created with the same type as that of the corresponding parameter. The argument expression is evaluated and an implicit conversion (§10.2) to the corresponding parameter type is performed. The resulting value is stored within that storage location. That storage location is represented by the input parameter in the function member invocation.

Example: Given the following declarations and method calls:

```
static void M1(in int p1) { ... }
int i = 10;
M1(i);    // i is passed as an input argument
M1(i + 5);    // transformed to a temporary input argument
```

In the M1(i) method call, i itself is passed as an input argument, because it is classified as a variable and has the same type int as the input parameter. In the M1(i + 5) method call, an unnamed int variable is created, initialized with the argument's value, and then passed as an input argument. See §12.6.4.2 and §12.6.4.4.

end example

- For an input, output, or reference argument, the variable reference is evaluated and the resulting storage location becomes the storage location represented by the parameter in the function member invocation. For an input or reference argument, the variable must be definitely assigned at the point of the method call. If the variable reference given as an output, or reference is an array element of a reference_type, a run-time check is performed to ensure that the element type of the array is identical to the type of the parameter. If this check fails, a System.ArrayTypeMismatchException is thrown.

Methods, indexers, and instance constructors may declare their right-most parameter to be a parameter array (§15.6.2.6). Such function members are invoked either in their normal form or in their expanded form depending on which is applicable (§12.6.4.2):

- When a function member with a parameter array is invoked in its normal form, the argument given for the parameter array shall be a single expression that is implicitly convertible (§10.2) to the parameter array type. In this case, the parameter array acts precisely like a value parameter.
- When a function member with a parameter array is invoked in its expanded form, the invocation shall specify zero or more positional arguments for the parameter array, where each argument is an expression that is implicitly convertible (§10.2) to the element type of the parameter array. In this case, the invocation creates an instance of the parameter array type with a length corresponding to the number of arguments, initializes the elements of the array instance with the given argument values, and uses the newly created array instance as the actual argument.

The expressions of an argument list are always evaluated in textual order.

Example: Thus, the example

```
class Test
{
    static void F(int x, int y = -1, int z = -2) =>
        Console.WriteLine($"x = {x}, y = {y}, z = {z}");

    static void Main()
    {
        int i = 0;
        F(i++, i++, i++);
        F(z: i++, x: i++);
    }
}
```

produces the output

x = 0, y = 1, z = 2
x = 4, y = -1, z = 3

end example

The array co-variance rules (§17.6) permit a value of an array type A[] to be a reference to an instance of an array type B[], provided an implicit reference conversion exists from B to A. Because of these rules, when an array element of a reference_type is passed as an output or reference argument, a run-time check is required to ensure that the actual element type of the array is identical to that of the parameter.

Example: In the following code

```
class Test
{
    static void F(ref object x) {...}

    static void Main()
    {
        object[] a = new object[10];
        object[] b = new string[10];
        F(ref a[0]); // Ok
        F(ref b[1]); // ArrayTypeMismatchException
    }
}
```

the second invocation of F causes a System.ArrayTypeMismatchException to be thrown because the actual element type of b is string and not object.

end example

When a function member with a parameter array is invoked in its expanded form with at least one expanded argument, the invocation is processed as if an array creation expression with an array initializer (§12.8.16.5) was inserted around the expanded arguments. An empty array is passed when there are no arguments for the parameter array; it is unspecified whether the reference passed is to a newly allocated or existing empty array.

Example: Given the declaration

```
void F(int x, int y, params object[] args);
```

the following invocations of the expanded form of the method

```
F(10, 20, 30, 40);
F(10, 20, 1, "hello", 3.0);
```

correspond exactly to

```
F(10, 20, new object[] { 30, 40 });
F(10, 20, new object[] { 1, "hello", 3.0 });
```

*end example*

When arguments are omitted from a function member with corresponding optional parameters, the default arguments of the function member declaration are implicitly passed. (This can involve the creation of a storage location, as described above.)

*Note:* Because these are always constant, their evaluation will not impact the evaluation of the remaining arguments. *end note*

## 12.6.3 Type inference

### 12.6.3.1 General

When a generic method is called without specifying type arguments, a *type inference* process attempts to infer type arguments for the call. The presence of type inference allows a more convenient syntax to be used for calling a generic method, and allows the programmer to avoid specifying redundant type information.

*Example:*

```
class Chooser
{
    static Random rand = new Random();

    public static T Choose<T>(T first, T second) =>
        rand.Next(2) == 0 ? first : second;
}

class A
{
    static void M()
    {
        int i = Chooser.Choose(5, 213); // Calls Choose<int>
        string s = Chooser.Choose("apple", "banana"); // Calls Choose<string>
    }
}
```

Through type inference, the type arguments int and string are determined from the arguments to the method.

*end example*

Type inference occurs as part of the binding-time processing of a method invocation (§12.8.9.2) and takes place before the overload resolution step of the invocation. When a particular method group is specified in a method invocation, and no type arguments are specified as part of the method invocation, type inference is applied to each generic method in the method group. If type inference succeeds, then the inferred type arguments are used to determine the types of arguments for subsequent overload resolution. If overload resolution chooses a generic method as the one to invoke, then the inferred type arguments are used as the type arguments for the invocation. If type inference for a particular method fails, that method does not participate in overload resolution. The failure of type inference, in and of itself, does not cause a binding-time error. However, it often leads to a binding-time error when overload resolution then fails to find any applicable methods.

If each supplied argument does not correspond to exactly one parameter in the method (§12.6.2.2), or there is a non-optional parameter with no corresponding argument, then inference immediately fails. Otherwise, assume that the generic method has the following signature:

T₀ M<X₁...Xₙ>(T₁ p₁ ... Tₙ pₙ)

With a method call of the form M(E₁ ... Eₙ) the task of type inference is to find unique type arguments S₁...Sₙ for each of the type parameters X₁...Xₙ, so that the call M<S₁...Sₙ>(E₁...Eₙ) becomes valid.

The process of type inference is described below as an algorithm. A conformant compiler may be implemented using an alternative approach, provided it reaches the same result in all cases.

During the process of inference each type parameter Xᵢ is either fixed to a particular type Sᵢ or unfixed with an associated set of bounds. Each of the bounds is some type T. Initially each type variable Xᵢ is unfixed with an empty set of bounds.

Type inference takes place in phases. Each phase will try to infer type arguments for more type variables based on the findings of the previous phase. The first phase makes some initial inferences of bounds, whereas the second phase fixes type variables to specific types and infers further bounds. The second phase may have to be repeated a number of times.

> Note: Type inference is also used in other contexts including for conversion of method groups (§12.6.3.14) and finding the best common type of a set of expressions (§12.6.3.15). end note

### 12.6.3.2 The first phase

For each of the method arguments Eᵢ:

- If Eᵢ is an anonymous function, an explicit parameter type inference (§12.6.3.8) is made from Eᵢ to Tᵢ
- Otherwise, if Eᵢ has a type U and Xᵢ is a value parameter (§15.6.2.2) then a lower-bound inference (§12.6.3.10) is made from U to Tᵢ.
- Otherwise, if Eᵢ has a type U and Xᵢ is a reference parameter (§15.6.2.4), or output parameter (§15.6.2.5) then an exact inference (§12.6.3.9) is made from U to Tᵢ.
- Otherwise, if Eᵢ has a type U and Xᵢ is an input parameter (§15.6.2.3) and Eᵢ is an input argument, then an exact inference (§12.6.3.9) is made from U to Tᵢ.
- Otherwise, if Eᵢ has a type U and Xᵢ is an input parameter (§15.6.2.3) then a lower bound inference (§12.6.3.10) is made from U to Tᵢ.
- Otherwise, no inference is made for this argument.

### 12.6.3.3 The second phase

The second phase proceeds as follows:
