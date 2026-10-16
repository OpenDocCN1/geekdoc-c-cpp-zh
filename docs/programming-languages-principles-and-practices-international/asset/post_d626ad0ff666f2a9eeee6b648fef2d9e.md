
### 8.19

Given the declarations

```
int x[10];
int y[5];
```

are x and y type equivalent in C?

### 8.20

Given the following C declaration:

```
const PI = 3.14159;
```

if we then use the constant PI in a geometry formula (like `A = PI*r*r`), we get the wrong answer. Why?

### 8.21

Given the following Java declaration:

```
short i = 2;
```

the Java compiler generates an error for the statement:

```
i = i + i;
```

Why?

### 8.22

Here are some type and variable declarations in C syntax:

```
typedef struct{
    int x;
    char y;
} Rec1;
typedef Rec1 Rec2;
typedef struct{
    int x;
    char y;
} Rec3;
Rec1 a, b;
Rec2 c;
Rec3 d;
```

State which variables are type equivalent under (a) structural equivalence, (b) name equivalence, and (c) the actual C equivalence algorithm. Be sure to identify those cases that are ambiguous from the information at hand.

### 8.23

In C++ the equality test `==` can be applied to arrays, but it tests the wrong thing. Also, the assignment operator `=` cannot be applied to arrays at all. Explain.

### 8.24

Can equality and assignment be applied to Ada arrays? Do they test the right thing?

### 8.25

By the type rules stated in the text, the array constructor in C does not construct a new type; that is, structural equivalence is applied to arrays. How could you write code to test this? (Hint: Can we use an equality test? Are there any other ways to test compatibility?)

### 8.26

Can a union in C be used to convert ints to doubles and vice versa? To convert longs to floats? Why or why not?

### 8.27

In a language in which “/” can mean either integer or real division and that allows coercions between integers and reals, the expression `I + J / K` can be interpreted in two different ways. Describe how this can happen.

### 8.28

Show how Hindley-Milner type checking determines that the following function (in ML syntax) takes an integer parameter and returns an integer result (i.e., is of type `int -> int` in ML terminology):

```
fun fac n = if n = 0 then 1 else n * fac (n-1);
```

### 8.29

Here is a function in ML syntax:

```
fun f (g,x) = g (g(x));
```

- (a) What polymorphic type does this function have?
- (b) Show how Hindley-Milner type checking infers the type of this function.
- (c) Rewrite this function as a C++ template function.

### 8.30

Write a polymorphic swap function that swaps the values of two variables of the same type in:

- (a) C++
- (b) ML

### 8.31

Write a polymorphic max function in C++ that takes an array of values of any type and returns the maximum value in the array, assuming the existence of a “>” operation.

### 8.32

Repeat the previous exercise, but add a parameter for a `gt` function that takes the place of the “>” operation.

### 8.33

Can both functions of the previous two exercises exist (and be used) simultaneously in a C++ program? Explain.

### 8.34

Explicit parametric polymorphism need not be restricted to a single type parameter. For example, in C++ one can write:

```
template <typename First, typename Second>
struct Pair{
    First first;
    Second second;
};
```

Write a C++ template function `makePair` that takes two parameters of different types and returns a `Pair` containing its two values.

### 8.35

Write the `Pair` data structure of the previous exercise as an Ada generic package, and write a similar `makePair` function in Ada.

### 8.36

Is C++ parametric polymorphism let-bound? (Hint: See the functions `makePair` and `makePair2` near the end of Section 8.8.)

### 8.37

Does the occur-check problem occur in C++? Explain.

### 8.38

A problem related to let-bound polymorphism in ML is that of polymorphic recursion, where a function calls itself recursively, but on different types at different points in the code. For example, consider the following function (in ML syntax):

```
fun f x = if x = x then true else (f false);
```

What type does this function have in ML? Is this the most general type it could have? Show how ML arrived at its answer.

### 8.39

Does the polymorphic recursion problem of the previous exercise exist in C++? Explain.

### 8.40

Data types can be kept as part of the syntax tree of a program and checked for structural equivalence by a simple recursive algorithm. For example, the type

```
struct{
    double x;
    int y[10];
};
```

might be kept as the tree shown in Figure 8.21.

![](img/062750ade02e28185b1fb8e8cf6dc89e_401_0.png)

Figure 8.21: A syntax tree for the struct definition

Describe a tree node structure that could be used to express the types of C or a similar language as trees. Write out a `TypeEqual` function in pseudocode that would check structural equivalence on these trees.

### 8.41

How could the trees of the previous exercise represent recursive types? Modify your `TypeEqual` function to take recursive types into account.

### 8.42

The language C uses structural type equivalence for arrays and pointers, but declaration equivalence for structs and unions. Why do you think the language designers did this?

### 8.43

Compare the BNFs for type declarations in C (Java, Ada) with the type tree of Figure 8.5 (8.6, 8.7). To what extent is the tree a direct reflection of the syntax?

### 8.44

What new type constructors does C++ add to those of C? Add these to the type tree of Figure 8.5. (Hint: Use the BNFs for C++ as motivation.)

### 8.45

The type tree for Ada (Figure 8.7) is somewhat simplified, with a number of constructors omitted. Add the missing constructors. Are there any missing simple types?

### 8.46

What operations would you consider necessary for a string data type? How well do arrays of characters support these operations?

### 8.52

In C there is no Boolean data type. Instead, comparisons such as `a == b` and `a <= b` return the integer value 0 for false and 1 for true. On the other hand, the `if` statement in C considers any nonzero value of its condition to be equivalent to true. Is there an advantage to doing this? Why not allow the condition `a <= b` to return any nonzero value if it is true?

### 8.53

Complete the entry of type information for the TinyAda parser discussed in Section 8.10. You should modify the type definition methods and the parameter declaration methods. Be sure to add type checking to these methods where relevant. Note that the `SymbolEntry` class and the `TypeDescriptor` class include two methods for setting formal parameter lists and lists of array index types, respectively. Test your parser with example TinyAda programs that exercise all of the modified methods.

### 8.54

Complete the modifications for type analysis to the TinyAda parsing methods that process expressions. Be sure to add type checking to these methods where relevant. Test your parser with example TinyAda programs that exercise all of the modified methods.

### 8.55

Complete the modifications for type analysis to the TinyAda parsing methods that process indexed variable references. Note that the `ArrayDescriptor` class includes the method `getIndexes`, which returns an iterator on the array’s index types.

### 8.56

Complete the modifications for type analysis to the TinyAda parsing methods that process actual parameters of procedure calls. Note that the `SymbolEntry` class includes the method `getParameters`, which returns an iterator on the procedure’s formal parameters.

### 8.57

Complete the modifications for type analysis to the TinyAda parsing methods that process names and assignment or procedure call statements.

## Notes and References

Data type systems in Algol-like languages such as Pascal, C, and Ada seem to suffer from excessive complexity and many special cases. In part, this is because a type system is trying to balance two opposing design goals: expressiveness and security. That is, a type system tries to make it possible to catch as many errors as possible while at the same time allowing the programmer the flexibility to create and use as many types as are necessary for the natural expression of an algorithm. ML (as well as Haskell) escapes from this complexity somewhat by using structural equivalence for predefined structures but name equivalence for user-defined types; however, this does weaken the effectiveness of type names in distinguishing different uses of the same structure. An interesting variant on this same idea is Modula-3, an object-oriented modification of Modula-2 that uses structural equivalence for ordinary data and name equivalence for objects (Cardelli et al. [1989a,b]; Nelson [1991]). Ada has perhaps the most consistent system, albeit containing many different ideas and hence extremely complex.

One frustrating aspect of the study of type systems is that language reference manuals rarely state the underlying type-checking algorithms explicitly. Instead, the algorithms must be inferred from a long list of special rules, a time-consuming investigative task. There are also few references that give detailed overviews of language type systems. Two that do have considerable detail are Cleaveland [1986] and Bishop [1986]. A lucid description of Pascal’s type system can be found in Cooper [1983]. A very detailed description of Ada’s type system can be found in Cohen [1996]. Java’s type system is described in Gosling et al. [2000], C’s type system in Kernighan and Ritchie [1988], C++’s type system
