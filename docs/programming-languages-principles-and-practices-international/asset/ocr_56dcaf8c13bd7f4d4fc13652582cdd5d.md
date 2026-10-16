The same notation is used for type parameters as in the types for implicitly polymorphic functions: 'a, 'b, 'c can be used in data structure declarations to indicate arbitrary types. Here is a Stack declaration in ML that imitates the above C declaration, but with an explicit type parameter:

```
datatype 'a Stack = EmptyStack
| Stack of 'a * ('a Stack);
```

First, note that this is unusual syntax, in that the type parameter 'a is written before the type name (Stack) rather than after it (presumably in imitation of what one does without the parameter, which is to define various stacks such as IntStack, CharStack, StringStack, etc.). Second, this declaration incorporates the effect of the pointer in C by expressing a stack as a union of the empty stack with a stack containing a pair of components—the first the data (of type 'a), and the second another stack (the tail or rest of the original stack). We can now write values of type Stack as follows:

```
val empty = EmptyStack; (* empty has type 'a Stack *)
val x = Stack(3, EmptyStack); (*x has type int Stack *)
```

Note that EmptyStack has no values, so is still of polymorphic type, while x, which contains the single value 3, is specialized by this value to int Stack.

Explicit parametric polymorphism creates no special new problems for Hindley-Milner type checking. It can operate in the same way on explicitly parameterized data as it did on implicitly parameterized functions. Indeed, polymorphic functions can be declared using an explicitly parameterized type, as for instance:

```
fun top (Stack p) = #1(p);
```

which (partially) defines top as a function 'a Stack -> 'a by using the projection function #1 on the pair p to extract its first component, which is the data. Thus, for the x previously defined, top x = 3.

Explicitly parameterized polymorphic data types fit nicely into languages with Hindley-Milner polymorphic type checking, but in fact they are nothing more than a mechanism for creating user-defined type constructors.

Recall that a type constructor, like array or struct, is a function from types to types, in that types are supplied as parameter values (these are the component types), and a new type is returned. For example, the array constructor in C, denoted by the brackets [ ], takes a component type (int, say) as a parameter and constructs a new type (array of int). This construction can be expressed directly in C as a typedef, where the syntactic ordering of the type parameter and return type is different from that of a function but entirely analogous. See Figure 8.19.

![](bbox=[0.3, 0.72, 0.72, 0.82])

# Figure 8.19 The components of a type definition in C