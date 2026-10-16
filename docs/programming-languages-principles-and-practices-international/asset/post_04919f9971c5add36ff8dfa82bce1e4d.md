
defining block via references to nonlocal variables. It has no way of directly accessing the variables in its calling environment. In the sample C code, procedure B cannot directly access the local variable x of procedure A. Nevertheless, it may need the value of x in A to perform its computations.

The method of communication of a procedure with its calling environment is through parameters. A parameter list is declared along with the definition of the procedure, as in the max procedure of the previous section:

```
int max (int x, int y){
  return x > y ? x : y;
}
```

Here, x and y are parameters to the max function. They do not take on any value until max is called, when they are replaced by the arguments from the calling environment, as in:

```
z = max(a+b,10);
```

In this call to max, the parameter x is replaced by the argument a + b, and the parameter y is replaced by the argument 10. To emphasize the fact that parameters have no value until they are replaced by arguments, parameters are sometimes called formal parameters, while arguments are called actual parameters.

A strong case can be made that procedures should communicate with the rest of the program using only the parameters—that is, a procedure or function should never use or change a nonlocal variable. After all, such use or change represents a dependency (in the case of a use) or a side effect (in the case of a change) that is invisible from a reading of the procedure specification—it can only be determined from examining the body of the procedure (which could be very long, or even missing in the case of a library procedure). While this rule is generally a good one with regard to variables (e.g., a global variable should still be a parameter if it is changed), it is too much to expect with regard to functions and constants. In general, the body of a procedure will need to call other procedures in the program and library procedures, and may also need to use constants (such as PI). These are all nonlocal references, but we would not want to clutter up the parameter list with all such references (particularly since they are all essentially constants). Thus, nonlocal uses cannot be avoided.

Nevertheless, some procedures may depend only on parameters and fixed language features. These are said to be in closed form, since they contain no nonlocal dependencies. An example is the max function above, which has no dependencies on nonlocal definitions—it depends entirely on fixed language features and its parameters.

On the other hand, a polymorphic definition of the same function in C++ (using templates):

```
template <typename T>
T max (T x, T y)
{ return x > y ? x : y ; }
```

is not in closed form, since the “>” operator can be overloaded for non-built-in types. Thus, to write this function in closed form, we would have to include the “>” operation in the parameter list:

```
template <typename T>
T max (T x, T y, bool (*gt)(T,T))
{ return gt(x,y) ? x : y ; }
```

(These examples were discussed in detail in Section 8.9.)

This form of pass by value is usually the only parameter-passing mechanism in functional languages. Pass by value is also the default mechanism in C++ and Pascal, and is essentially the only parameter-passing mechanism in C and Java. However, in these languages a slightly different interpretation of pass by value is used: The parameters are viewed as local variables of the procedure, with initial values given by the values of the arguments in the call. Thus, in C, Java, and Pascal, value parameters may be assigned, just as with local variables (but cause no changes outside the procedure), while Ada in parameters may not be the targets of assignment statements (see the discussion of Ada parameters in Section 10.3.5).

Note that pass by value does not imply that changes cannot occur outside the procedure through the use of parameters. If the parameter has a pointer or reference type, then the value is an address and can be used to change memory outside the procedure. For example, the following C function definitely changes the value of the integer pointed to by the parameter p:

```
void init_p (int* p)
{ *p = 0; }
```

On the other hand, directly assigning to p does not change the argument outside the procedure:

```
void init_ptr (int* p)
{ p = (int*) malloc(sizeof(int)); /* error - has no effect! */
}
```

In addition, in some languages certain values are implicitly pointers or references. For example, in C, arrays are implicitly pointers (to the first location of the array); this means an array value parameter can always be used to change the values stored in the array:

```
void init_p_0 (int p[])
{ p[0] = 0; }
```

In Java, too, objects are implicitly pointers, so any object parameter can be used to change its data:

```
void append_1 (Vector v)
// adds an element to Vector v
{ v.addElement( new Integer(1)); }
```

However, as in C, direct assignments to parameters do not work either:

```
void make_new (Vector v)
{ v = new Vector(); /* error - has no effect! */ }
```

### 10.3.2 Pass by Reference

In pass by reference, an argument must be something like a variable with an allocated address. Instead of passing the value of the variable, pass by reference passes the location of the variable, so that the parameter becomes an alias for the argument, and any changes made to the parameter occur to the argument as well. In FORTRAN, pass by reference is the only parameter-passing mechanism. In C++ and Pascal, pass by reference (instead of the default pass by value) can be specified by using an ampersand (&) after the data type in C++, and a var keyword before the variable name in Pascal:

```
void inc(int& x) // C++
{ x++ ; }

procedure inc(var x: integer); (* Pascal *)
begin
    x :=  x + 1;
end;
```

After a call to inc(a) the value of a has increased by 1, so that a side effect has occurred. Multiple aliasing is also possible, such as in the following example:

```
int a;

void yuck (int& x, int& y)
{ x = 2;
    y = 3;
    a = 4;
}

yuck (a, a);
```

Inside procedure yuck after the call, the identifiers x, y, and a all refer to the same variable, namely, the variable a.

As noted previously, C can achieve pass by reference by passing a reference or location explicitly as a pointer. C uses the operator & to indicate the location of a variable and the operator * to dereference a pointer. For example:

```
void inc (int* x) /*C imitation of pass by reference */
{ (*x)++; /* adds 1 to *x */ }

int a;

inc(&a); /* pass the address of a to the inc function */
```

This code has the same effect as the previous C++ or Pascal code for the inc procedure. Of course, there is the annoying necessity here of explicitly taking the address of the variable a, and then explicitly dereferencing it again in the body of inc.

A similar effect can be achieved in ML by using reference types to imitate pass by reference. (In ML, as in C, only pass by value is available.) For example:

```
fun inc (x: int ref) = x := !x + 1;
```

One additional issue that must be resolved in a language with pass by reference is the response of the language to reference arguments that are not variables and, thus, do not have known addresses within the runtime environment. For example, given the C++ code

```
void inc(int& x)
{ x++; }
...
inc(2); // ??
```

how should the compiler respond to the call inc(2)? In FORTRAN, in which pass by reference is the only available parameter mechanism, this is syntactically correct code. The response of the compiler is to create a temporary integer location, initialize it with the value 2, and then apply the inc function. This actually mimics pass by value, since the change to the temporary location does not affect the rest of the program. In C++ and Pascal, however, this is an error. In these languages, reference arguments must be l-values—that is, they must have known addresses.

### 10.3.3 Pass by Value-Result

Pass by value-result achieves a similar result to pass by reference, except that no actual alias is established. Instead, in pass by value-result, the value of the argument is copied and used in the procedure, and then the final value of the parameter is copied back out to the location of the argument when the procedure exits. Thus, this method is sometimes known as copy-in, copy-out, or copy-restore.

Pass by value-result is only distinguishable from pass by reference in the presence of aliasing. Thus, in the following code (written for convenience in C syntax):

```
void p(int x, int y)
{ x++;
  y++;
}

main()
{ int a = 1;
  p(a,a);
  ...
}
```

a has value 3 after p is called if pass by reference is used, while a has the value 2 if pass by value-result is used.

Issues left unspecified by this mechanism, and possibly differing in different languages or implementations, are the order in which results are copied back to the arguments and whether the locations of the arguments are calculated only on entry and stored or whether they are recalculated on exit.

A further option is that a language can offer a pass by result mechanism as well, in which there is no incoming value, but only an outgoing one.
