The template function use_f() has a static member count, and we can use its address to see how many instantiations are made. There are five distinct addresses, so there must have been five distinct instantiations of the use_f() template.

To see what is happening, consider how the compiler determines the type for the F template parameter. First, look at this call:

```
```
use_f(y, dub);
```
```

Here dub is the name of a function that takes a double argument and returns a double value. The name of a function is a pointer, hence the parameter F becomes type double (*) (double), a pointer to a function with a double argument and a double return value.

The next call is this:

```
```
use_f(y, square);
```
```

Again, the second argument is type double (*) (double), so this call uses the same instantiation of use_f() as the first call.

The next two calls to use_f() have objects as second arguments, so F becomes type Fp and Fq respectively, so we get two new instantiations for these values of F. Finally, the last two calls set F to whatever types the compiler uses for lambda expressions.

# ## Fixing the Problem

The function wrapper lets you rewrite the program so that it uses just one instantiation of use_f() instead of five. Note that the function pointers, function objects, and lambda expressions in Listing 18.7 share a common behavior—each takes one type double argument and each returns a type double value. We can say that each has the same call signature, which is described by the return type followed by a comma-separated list of parameter types enclosed in a pair of parentheses. Thus, these six examples all have double(double) as the call signature.

The function template, declared in the functional header file, specifies an object in terms of a call signature, and it can be used to wrap a function pointer, function object, or lambda expression having the same call signature. For example, the following declaration creates a function object fdci that takes a char and an int argument and returns type double:

```
```
std::function<double(char, int)> fdci;
```
```

You can then assign to fdci any function pointer, function object, or lambda expression that takes type char and int arguments and returns type double.

The various callable arguments in Listing 18.7 all have the same call signature—double(double). So to fix Listing 18.7 and reduce the number of instantiations, we can use function<double(double)> to create six wrappers for the six functions, functors, and lambdas. Then all six calls to use_f() can be made with the same type (function<double(double)>) for F, resulting in just one instantiation. Listing 18.8 shows the result.