
## 6.5 Type Checking

In this section, we consider type checking of expressions. The rules for checking statements are similar to those for expressions. For example, we treat the conditional statement “if (E) S;” as if it were the application of a function *f* to *E* and *S*. Let the special type *void* denote the absence of a value. Then function *f* is expected to be applied to a *boolean* and a *void*; the result of the application is a *void*.

### 6.5.2 Type Conversions

Consider expressions like *x + i*, where *x* is of type *float* and *i* is of type *integer*. Since the representation of integers and floating-point numbers is different within a computer and different machine instructions are used for operations on integers and floats, the compiler may need to convert one of the operands of + to ensure that both operands are of the same type when the addition occurs.

Suppose that integers are converted to floats when necessary, using a unary operator *(float)*. For example, the integer 2 is converted to a float in the code for the expression 2 * 3.14:

```
t₁ = (float) 2
t₂ = t₁ * 3.14
```

We can extend such examples to consider integer and float versions of the operators; for example, *int* for integer operands and *float* for floats.

Type synthesis will be illustrated by extending the scheme in Section 6.4.2 for translating expressions. We introduce another attribute *E.type*, whose value is either *integer* or *float*. The rule associated with E → E₁ + E₂ builds on the pseudocode

```
if (E₁.type = integer and E₂.type = integer)  E.type = integer;
else if (E₁.type = float and E₂.type = integer)  ⋯
⋯
```

As the number of types subject to conversion increases, the number of cases increases rapidly. Therefore with large numbers of types, careful organization of the semantic actions becomes important.

Type conversion rules vary from language to language. The rules for Java in Fig. 6.25 distinguish between *widening* conversions, which are intended to preserve information, and *narrowing* conversions, which can lose information. The widening rules are given by the hierarchy in Fig. 6.25(a): any type lower in the hierarchy can be widened to a higher type. Thus, a *char* can be widened to an *int* or a *float*, but a *char* cannot be widened to a *short*. The narrowing rules are illustrated by the graph in Fig. 6.25(b): a type *s* can be narrowed to a type *t* if there is a path from *s* to *t*. Note that *char*, *short*, and *byte* are pairwise convertible to each other.

![](img/2a44b9071782fade81f3050c3b718341_393_0.png)

Figure 6.25: Conversions between primitive types in Java

Conversion from one type to another is said to be *implicit* if it is done automatically by the compiler. Implicit type conversions, also called *coercions*, are limited in many languages to widening conversions. Conversion is said to be *explicit* if the programmer must write something to cause the conversion. Explicit conversions are also called *casts*.

The semantic action for checking E → E₁ + E₂ uses two functions:

- 1. \(max(t_1,t_2)\) takes two types \(t_1\) and \(t_2\) and returns the maximum (or least upper bound) of the two types in the widening hierarchy. It declares an error if either \(t_1\) or \(t_2\) is not in the hierarchy; e.g., if either type is an array or a pointer type.
- 2. \(widen(a,t,w)\) generates type conversions if needed to widen the contents of an address \(a\) of type \(t\) into a value of type \(w\). It returns \(a\) itself if \(t\) and \(w\) are the same type. Otherwise, it generates an instruction to do the conversion and place the result in a temporary, which is returned as the result. Pseudocode for \(widen\), assuming that the only types are \(integer\) and \(float\), appears in Fig. 6.26.

```
    Addr widen(Addr a, Type t, Type w) {
        if ( t = w ) return a;
        else if ( t = integer and w = float ) {
            temp = new Temp();
            gen(temp '=' '(float)' a);
            return temp;
        }
        else error;
    }
```

Figure 6.26: Pseudocode for function *widen*

The semantic action for E → E₁ + E₂ in Fig. 6.27 illustrates how type conversions can be added to the scheme in Fig. 6.20 for translating expressions. In the semantic action, temporary variable a₁ is either E₁.addr, if the type of E₁ does not need to be converted to the type of E, or a new temporary variable returned by *widen* if this conversion is necessary. Similarly, a₂ is either E₂.addr or a new temporary holding the type-converted value of E₂. Neither conversion is needed if both types are *integer* or both are *float*. In general, however, we could find that the only way to add values of two different types is to convert them both to a third type.

```
E → E₁ + E₂  { E.type = max(E₁.type,E₂.type);
              a₁ = widen(E₁.addr,E₁.type,E.type);
              a₂ = widen(E₂.addr,E₂.type,E.type);
              E.addr = new Temp();
              gen(E.addr '=' a₁ '+' a₂); }
```

Figure 6.27: Introducing type conversions into expression evaluation

### 6.5.3 Overloading of Functions and Operators

An *overloaded* symbol has different meanings depending on its context. Overloading is *resolved* when a unique meaning is determined for each occurrence of a name. In this section, we restrict attention to overloading that can be resolved by looking only at the arguments of a function, as in Java.

**Example 6.13:** The + operator in Java denotes either string concatenation or addition, depending on the types of its operands. User-defined functions can be overloaded as well, as in

```
void err() { ... }
void err(String s) { ... }
```

Note that we can choose between these two versions of a function `err` by looking at their arguments. □

The following is a type-synthesis rule for overloaded functions:

```
if f can have type s_i → t_i, for 1 ≤ i ≤ n, where s_i ≠ s_j for i ≠ j
and x has type s_k, for some 1 ≤ k ≤ n
then expression f(x) has type t_k                    (6.10)
```

The value-number method of Section 6.1.2 can be applied to type expressions to resolve overloading based on argument types, efficiently. In a DAG representing a type expression, we assign an integer index, called a value number, to each node. Using Algorithm 6.3, we construct a signature for a node,

Using the symbol ∀ (read as “for any type”) and the type constructor list, the type of *length* can be written as

$$\forall \alpha.\ \mathrm{list}(\alpha) \to \mathrm{integer} \tag{6.12}$$

The ∀ symbol is the *universal quantifier*, and the type variable to which it is applied is said to be *bound* by it. Bound variables can be renamed at will, provided all occurrences of the variable are renamed. Thus, the type expression

$$\forall \beta.\ \mathrm{list}(\beta) \to \mathrm{integer}$$

is equivalent to (6.12). A type expression with a ∀ symbol in it will be referred to informally as a “polymorphic type.”

Each time a polymorphic function is applied, its bound type variables can denote a different type. During type checking, at each use of a polymorphic type we replace the bound variables by fresh variables and remove the universal quantifiers.

The next example informally infers a type for *length*, implicitly using type inference rules like (6.9), which is repeated here:

**if** \(f(x)\) is an expression,  
**then** for some \(\alpha\) and \(\beta\), \(f\) has type \(\alpha \to \beta\) and \(x\) has type \(\alpha\)

**Example 6.15.** The abstract syntax tree in Fig. 6.29 represents the definition of *length* in Fig. 6.28. The root of the tree, labeled *fun*, represents the function definition. The remaining nonleaf nodes can be viewed as function applications. The node labeled + represents the application of the operator + to a pair of children. Similarly, the node labeled *if* represents the application of an operator *if* to a triple formed by its children (for type checking, it does not matter that either the **then** or the **else** part will be evaluated, but not both).

![](img/2a44b9071782fade81f3050c3b718341_396_0.png)

Figure 6.29: Abstract syntax tree for the function definition in Fig. 6.28

From the body of function *length*, we can infer its type. Consider the children of the node labeled *if*, from left to right. Since *null* expects to be applied to lists, \(x\) must be a list. Let us use variable \(\alpha\) as a placeholder for the type of the list elements; that is, \(x\) has type “list of \(\alpha\).”
