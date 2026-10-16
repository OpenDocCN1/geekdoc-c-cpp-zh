
/*
factor = primary [ "**" primary ] | "not" primary
*/
private TypeDescriptor factor(){
    TypeDescriptor t1;
    if (token.code == Token.NOT){
        token = scanner.nextToken();
        t1 = primary();
        matchTypes(t1, BOOL_TYPE, "Boolean expression expected");
    }
    else{
        t1 = primary();
        if (token.code == Token.EXPO){
            matchTypes(t1, INT_TYPE, "integer expression expected");
            token = scanner.nextToken();
            TypeDescriptor t2 = primary();
            matchTypes(t2, INT_TYPE, "integer expression expected");
        }
    }
    return t1;
}

This method has the following three options for returning a type descriptor:

+   1. There is no operator in the factor, so the type descriptor t1 obtained from the first call of primary is returned directly to the caller.
+   2. The operator is a leading not. Then the type descriptor t1 is returned, after matching it to BOOL_TYPE.
+   3. The operator is a binary **. Then the type descriptor t1 is returned, after matching it and the type descriptor t2, obtained from the second call to primary, to INT_TYPE.

As you can see, the type of every operand must be checked, and great care must be taken to ensure that the right type descriptor is returned. The modification of the remaining methods for parsing expressions is left as an exercise for the reader.

## 8.10.5 Processing Names: Indexed Component References and Procedure Calls

The syntax of TinyAda indexed component references and procedure calls is the same if the procedure expects at least one parameter. As shown in the previous code segment, the method name now must distinguish these two types of phrases, based on the role of the leading identifier. The code for processing the trailing phrase, which consists of a parenthesized list of expressions, can now be split into two distinct parsing methods, actualParameterPart and indexedComponent.

The method actualParameterPart receives the procedure name’s symbol entry as a parameter. The entry contains the information for the procedure’s formal parameters, which was entered earlier when the procedure was declared. As it loops through the list of expressions, this method should match the type of each expression to the type of the formal parameter in that position. Also, the number of expressions and formal parameters must be the same.

The method indexedComponent receives the array identifier’s entry as a parameter. This entry’s type descriptor contains the information for the array’s index types and element type, which was entered earlier when that array type was defined. This method uses the same strategy to match expressions to declared index types as we saw for matching the types of formal and actual parameters in the method actualParameterPart. However, indexedComponent must also return a new symbol entry that contains the array’s element type, as well as the role of the array identifier. This will be the information returned by the name method for role and type analysis farther up the call tree. The completion of these two methods, as well as the rest of the code for type analysis in the TinyAda parser, is left as an exercise for the reader.

## 8.10.6 Completing Static Semantic Analysis

Two other types of semantic restrictions can be imposed during parsing. One restriction involves the checking of parameter modes. TinyAda has three parameter modes: input only (signified by the keyword in), output only (signified by the keyword out), and input/output (signified by the keywords in out). These modes are used to control the flow of information to and from procedures. For example, only a variable or a parameter with the same mode can be passed as an actual parameter where the formal parameter has been declared as out or in out. Within a procedure’s code, an out parameter cannot appear in an expression, and an in parameter cannot be the target of an assignment statement.

The other restriction recognizes a distinction between static expressions and other expressions. A static expression is one whose value can be computed at compile time. Only static expressions can be used in number declarations and range type definitions. We will discuss the enforcement of these two types of restrictions in later chapters.

## Exercises

+   8.1 Compare the flexibility of the dynamic typing of Lisp with the reliability of the static typing of Ada, ML, C++, or Java. Think of as many arguments as you can both for and against static typing as an aid to program design.

+   8.2 Look up the implementation details on the representation of data by your C/C++ compiler (or other non-Java compiler) that you are using and compare them to the sketches of typical implementations given in the text. Where do they differ? Where are they the same?

+   8.3 (a) The Boolean data type may or may not have an order relation, and it may or may not be convertible to integral types, depending on the language. Compare the treatment of the Boolean type in at least two of the following languages with regard to these two issues: Java, C++, Ada, ML.
+   (b) Is it useful for Booleans to be ordered? Convertible to integers?

## 8.4

**(a)** Given the C declarations

```c
struct{
    int i;
    double j;
} x, y;
struct{
    int i;
    double j;
} z;
```

the assignment `x = z` generates a compilation error, but the assignment `x = y` does not. Why?

**(b)** Give two different ways to fix the code in part (a) so that `x = z` works. Which way is better and why?

## 8.5

Suppose that we have two C arrays:

```c
int x[10];
int y[10];
```

Why won’t the assignment `x = y` compile in C? Can the declarations be fixed so the assignment will work?

## 8.6

Given the following variable declarations in C/C++:

```c
enum { one } x;
enum { two } y;
```

the assignment `x = y` is fine in C, but generates a compiler error in C++. Explain.

## 8.7

Given the following function variable declarations in C/C++:

```c
int (*f)(int);
int (*g)(int);
int (*h)(char);
```

the assignment `f = g` is fine in C and C++, but the assignment `h = g` generates a compiler warning in C and a compiler error in C++. Explain.

## 8.8

Show that the set:

{emptylist} ∪ char ∪ (char × char) ∪ (char × char × char) ∪ …

is the smallest solution to the set equation:

CharList = {emptylist} ∪ char × CharList

(See Section 8.3.5 and Exercise 6.53.)

## 8.9 Consider the set equation

ℵ × char = ℵ

+   (a) Show that any set X satisfying this equation must be infinite.
+   (b) Show that any element of a set satisfying this equation must contain an infinite number of characters.
+   (c) Is there a smallest solution to this equation?

## 8.10 Consider the following declaration in C syntax:

```c
struct CharTree{
    char data;
    struct CharTree left, right;
};
```

+   (a) Rewrite CharTree as a union, similar to the union CharList declaration of Section 8.3.5.
+   (b) Write a recursive set equation for your declaration in part (a).
+   (c) Describe a set that is the smallest solution to your equation of part (b).
+   (d) Prove that your set in part (c) is the smallest solution.
+   (e) Rewrite this as a valid C declaration.

## 8.11 Here are some type declarations in C:

```c
typedef struct Rec1 * Ptr1;
typedef struct Rec2 * Ptr2;
struct Rec1{
    int data;
    Ptr2 next;
};
struct Rec2{
    double data;
    Ptr2 next;
};
```

Should these be allowed? Are they allowed? Why or why not?

## 8.12

+   (a) What is the difference between a subtype and a derived type in Ada?
+   (b) What C type declaration is the following Ada declaration equivalent to?
+       subtype New_Int is integer;
+   (c) What C type declaration is the following Ada declaration equivalent to?
+       type New_Int is new integer;

8.13 In Ada the equality test (x = y in Ada syntax) is legal for all types, as long as x and y have the same type. In C, however, the equality test (x == y in C syntax) is only permitted for variables of a few types; however, the types of x and y need not always be the same.
(a) Describe the types of x and y for which the C comparison x == y is legal.
(b) Why does the C language not allow equality tests for variables of certain types?
(c) Why does the C language allow comparisons between certain values of different types?

8.14 Describe the type correctness and inference rules in C for the conditional expression:
	e1 ? e2 : e3
Must e2 and e3 have the same type? If they have the same type, can it be any type?

8.15 Suppose we used the following C++ code that attempts to avoid the use of a static_cast to print out the internal value of true (see the code at the end of Section 8.7):

```c
union{
    int i;
    bool b;
} x;
...
x.b = true;
cout << x.i << endl;
```

Why is this wrong? (Hint: Try the assignment x.i=20000 before x.b=true.)

8.16 Programmers often forget that numeric data types such as int are only approximations of mathematical number systems. For example, try the following two divisions in C or C++ or Java on your system, and explain the result: -2147483648 / -1; -2147483647 / -1.

8.17 The chapter makes no mention of the initialization problem for variables. Describe the rules for variable initialization in C, Ada, ML, or other similar language. In particular, are variables of all types initialized when a program starts running? If so, how is the initial value constructed?

8.18 Here are some type and variable declarations in C syntax:

```c
typedef char* Table1;
typedef char* Table2;

Table1 x,y;
Table2 z;
Table2 w;
```

State which variables are type equivalent under (a) structural equivalence, (b) name equivalence, and (c) the actual C equivalence algorithm. Be sure to identify those cases that are ambiguous from the information at hand.
