
The advantage of such variables is that they have the highest degree of flexibility, allowing highly generic code to be written. One disadvantage of implicit heap-dynamic variables is the run-time overhead of maintaining all the dynamic attributes, which could include array subscript types and ranges, among others. Another disadvantage is the loss of some error detection by the compiler, as discussed in Section 5.4.2.2.

## 5.5 Scope

One of the important factors in understanding variables is scope. The scope of a variable is the range of statements in which the variable is visible. A variable is visible in a statement if it can be referenced or assigned in that statement.

The scope rules of a language determine how a particular occurrence of a name is associated with a variable, or in the case of a functional language, how a name is associated with an expression. In particular, scope rules determine how references to variables declared outside the currently executing subprogram or block are associated with their declarations and thus their attributes (blocks are discussed in Section 5.5.2). A clear understanding of these rules for a language is therefore essential to the ability to write or read programs in that language.

A variable is local in a program unit or block if it is declared there. The nonlocal variables of a program unit or block are those that are visible within the program unit or block but are not declared there. Global variables are a special category of nonlocal variables, which are discussed in Section 5.5.4.

Scoping issues of classes, packages, and namespaces are discussed in Chapter 11.

### 5.5.1 Static Scope

ALGOL 60 introduced the method of binding names to nonlocal variables called static scoping, which has been copied by many subsequent imperative languages and many nonimperative languages as well. Static scoping is so named because the scope of a variable can be statically determined—that is, prior to execution. This permits a human program reader (and a compiler) to determine the type of every variable in the program simply by examining its source code.

There are two categories of static-scoped languages: those in which subprograms can be nested, which creates nested static scopes, and those in which subprograms cannot be nested. In the latter category, static scopes are also created by subprograms but nested scopes are created only by nested class definitions and blocks.

Ada, JavaScript, Common Lisp, Scheme, Fortran 2003+, F#, and Python allow nested subprograms, but the C-based languages do not.

Our discussion of static scoping in this section focuses on those languages that allow nested subprograms. Initially, we assume that all scopes are associated with program units and that all referenced nonlocal variables are declared in other program units.⁶ In this chapter, it is assumed that scoping is the only method of accessing nonlocal variables in the languages under discussion. This is not true for all languages. It is not even true for all languages that use static scoping, but the assumption simplifies the discussion here.

When the reader of a program finds a reference to a variable, the attributes of the variable can be determined by finding the statement in which it is declared (either explicitly or implicitly). In static-scoped languages with nested subprograms, this process can be thought of in the following way. Suppose a reference is made to a variable x in subprogram sub1. The correct declaration is found by first searching the declarations of subprogram sub1. If no declaration is found for the variable there, the search continues in the declarations of the subprogram that declared subprogram sub1, which is called its static parent. If a declaration of x is not found there, the search continues to the next-larger enclosing unit (the unit that declared sub1's parent), and so forth, until a declaration for x is found or the largest unit's declarations have been searched without success. In that case, an undeclared variable error is reported. The static parent of subprogram sub1, and its static parent, and so forth up to and including the largest enclosing subprogram, are called the static ancestors of sub1. Actual implementation techniques for static scoping, which are discussed in Chapter 10, are usually much more efficient than the process just described.

Consider the following JavaScript function, big, in which the two functions sub1 and sub2 are nested:

```
function big() {
    function sub1() {
        var x = 7;
        sub2();
    }
    function sub2() {
        var y = x;
    }
    var x = 3;
    sub1();
}
```

Under static scoping, the reference to the variable x in sub2 is to the x declared in the procedure big. This is true because the search for x begins in the procedure in which the reference occurs, sub2, but no declaration for x is found there. The search continues in the static parent of sub2, big, where the declaration of x is found. The x declared in sub1 is ignored, because it is not in the static ancestry of sub2.

In some languages that use static scoping, regardless of whether nested subprograms are allowed, some variable declarations can be hidden from some other code segments. For example, consider again the JavaScript function big. The variable x is declared in both big and in sub1, which is nested inside big. Within sub1, every simple reference to x is to the local x. Therefore, the outer x is hidden from sub1.

### 5.5.2 Blocks

Many languages allow new static scopes to be defined in the midst of executable code. This powerful concept, introduced in ALGOL 60, allows a section of code to have its own local variables whose scope is minimized. Such variables are typically stack dynamic, so their storage is allocated when the section is entered and deallocated when the section is exited. Such a section of code is called a block. Blocks provide the origin of the phrase block-structured language.

The C-based languages allow any compound statement (a statement sequence surrounded by matched braces) to have declarations and thereby define a new scope. Such compound statements are called blocks. For example, if list were an integer array, one could write the following:

```
if (list[i] < list[j]) {
    int temp;
    temp = list[i];
    list[i] = list[j];
    list[j] = temp;
}
```

The scopes created by blocks, which could be nested in larger blocks, are treated exactly like those created by subprograms. References to variables in a block that are not declared there are connected to declarations by searching enclosing scopes (blocks or subprograms) in order of increasing size.

Consider the following skeletal C function:

```
void sub() {
    int count;
    ...
    while (...) {
        int count;
        count++;
        ...
    }
    ...
}
```

The reference to count in the while loop is to that loop's local count. In this case, the count of sub is hidden from the code inside the while loop. In general, a declaration for a variable effectively hides any declaration of a variable with the same name in a larger enclosing scope.⁷ Note that this code is legal in C and C++ but illegal in Java and C#. The designers of Java and C# believed that the reuse of names in nested blocks was too error prone to be allowed.

Although JavaScript uses static scoping for its nested functions, nonfunction blocks cannot be defined in the language.

Most functional programming languages include a construct that is related to the blocks of the imperative languages, usually named let. These constructs have two parts, the first of which is to bind names to values, usually specified as expressions. The second part is an expression that uses the names defined in the first part. Programs in functional languages are comprised of expressions, rather than statements. Therefore, the final part of a let construct is an expression, rather than a statement. In Scheme, a let construct is a call to the function LET with the following form:

```
(LET (
  (name₁ expression₁)
  ...
  (nameₙ expressionₙ))
  expression
)
```

The semantics of the call to LET is as follows: The first n expressions are evaluated and the values are assigned to the associated names. Then, the final expression is evaluated and the return value of LET is that value. This differs from a block in an imperative language in that the names are of values; they are not variables in the imperative sense. Once set, they cannot be changed. However, they are like local variables in a block in an imperative language in that their scope is local to the call to LET. Consider the following call to LET:

```
(LET (
  (top (+ a b))
  (bottom (- c d)))
  (/ top bottom)
)
```

This call computes and returns the value of the expression (a + b) / (c - d).

In ML, the form of a let construct is as follows:

```
let
  val name₁ = expression₁
  ...
  val nameₙ = expressionₙ
in
  expression
end;
```
