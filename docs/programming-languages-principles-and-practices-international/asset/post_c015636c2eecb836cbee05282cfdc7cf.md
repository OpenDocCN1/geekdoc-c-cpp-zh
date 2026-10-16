
functional languages (Chapter 3), expressions in programs share an important property with mathematical expressions. We call this shared property the **substitution rule** (or sometimes **referential transparency**). According to this rule, any two expressions in a program that have the same value may be substituted for each other anywhere in the program. In other words, their values always remain equal, regardless of the context in which they are evaluated. For example, if x and y have the same value at one point in a referentially transparent program, then they *always* have the same value⁵ and may be freely substituted for each other anywhere. (Note that this prohibits x and y from being variables in the programming language sense. Instead, they must be constants.)

Referential transparency allows for a very strong form of delayed evaluation to be used that has important theoretical and practical consequences. It is called **normal order evaluation**. A precise mathematical definition can be given in the context of the lambda calculus, as was explained briefly in Chapter 3. For our purposes in this section, normal order evaluation of an expression means that each operation (or function) begins its evaluation *before* its operands are evaluated, and each operand is evaluated only if it is needed for the calculation of the value of the operation.

As an example of normal order evaluation, consider the following functions (in C syntax):

```
```c
int double(int x){
    return x + x;
}

int square(int x){
    return x * x;
}
```
```

Now consider the expression **square(double(2))**. Using normal order evaluation, the call to square is replaced by double(2)*double(2) without evaluating double(2), and then double(2) is replaced by 2 + 2, so that the following sequence of replacements occurs:

square(double(2)) ⇒ double(2)*double(2) ⇒ (2 + 2)*(2 + 2)

Only after these replacements occur is the expression evaluated, typically in left-to-right order:

(2 + 2)*(2 + 2) ⇒ 4 * (2 + 2) ⇒ 4 * 4 ⇒ 16

Note how this differs from applicative order evaluation, which evaluates the call to double before the call to square, and would result in the following sequence of replacements (with evaluation intermingled):

square(double(2)) ⇒ square(2 + 2) ⇒ square(4) ⇒ 4 * 4 ⇒ 16

Normal order evaluation implements a kind of code inlining, in which the bodies of functions are substituted at their call sites *before* evaluation occurs; see footnote 2.

⁵As long as we are in the scope of a particular declaration of these variables. Obviously, different declarations may cause different values to be associated with these names.

In the absence of side effects, normal order evaluation does not change the semantics of a program. While it might seem inefficient (e.g., 2+2 gets evaluated twice instead of once in the previous example), it can be made efficient, and it has a number of good properties that make it useful, particularly for functional languages. As a simple example, if C used normal order evaluation, the C if-expression e1 ? e2 : e3 can be written (for each data type) as an ordinary C function, instead of needing special syntax in the language:

```
int if_exp(int x, int y, int z){
    if (x) return y; else return z;
}
```

Here y and z are only evaluated if they are needed in the code of if_exp, which is the behavior that we want.

On the other hand, the presence of side effects can mean that normal order evaluation substantially changes the semantics of a program. Consider, for example, the C function:

```
int get_int(){
    int x;
    /* read an integer value into x from standard input */
    scanf("%d",&x);
    return x;
}
```

This function has a side effect (input).

Now consider what would happen to the expression square(get_int()) using normal order evaluation: It would be expanded into get_int()*get_int(), and two integer values, rather than just one, would be read from standard input—a very different outcome from what we would expect.

Normal order evaluation appears as so-called lazy evaluation in the functional language Haskell, as was studied in detail in Chapter 3. Normal order evaluation appears also as a parameter passing technique for functions in Algol60, where it is known as pass by name; this will be studied briefly in the next chapter.

## 9.2 Conditional Statements and Guards

The most typical form of structured control is execution of a group of statements only under certain conditions. This involves making a Boolean, or logical, test before entering a sequence of statements. The well-known if-statement is the most common form of this construct. The various ways such a conditional can be introduced will be discussed shortly.

First, however, we want to describe a general form of conditional statement that encompasses all the various conditional constructs. This general form, known as the guarded if statement, was introduced by E. W. Dijkstra, and looks like this:

```
if B1 -> S1
| B2 -> S2
| B3 -> S3
...
| Bn -> Sn
fi
```

The semantics of this statement are as follows: each Bi is a Boolean expression, called a guard, and each Si is a statement sequence. If one Bi evaluates to true, then the corresponding statement sequence Si is executed. If more than one Bi is true, then the one and only corresponding Si is selected for execution. If no Bi is true, then an error occurs.

There are several interesting features in this description. First, it does not say that the first Bi that evaluates to true is the one chosen. Thus, the guarded if introduces nondeterminism into programming, a feature that becomes very useful in concurrent programming (Chapter 13). Second, it leaves unspecified whether all the guards are evaluated. Thus, if the evaluation of a Bi has a side effect, the result of the execution of the guarded if may be unknown. Of course, the usual deterministic implementation of such a statement would sequentially evaluate the Bi s until a true one is found, whence the corresponding Si is executed and control is transferred to the point following the guarded statement.

The two major ways that programming languages implement conditional statements like the guarded if are as if-statements and case-statements.

### 9.2.1 If-Statements

The basic form of the if-statement is as given in the extended Backus-Naur form (EBNF) rule for the if statement in C, with an optional “else” part:

```
if-statement → if ( expression ) statement [else statement]
```

where statement can be either a single statement or a sequence of statements surrounded by braces:

```
if (x > 0) y = 1/x;
else{
    x = 2;
    y = 1/z;
}
```

This form of the if (which also exists in Java and Pascal) is problematic, however, because it is ambiguous in the syntactic sense described in Chapter 6. Indeed, the statement

```
if (e1) if (e2) S1 else S2
```

has two different parse trees according to the BNF. These parse trees are shown in Figure 9.4.

![](img/062750ade02e28185b1fb8e8cf6dc89e_416_0.png)

# Figure 9.4 Two parse trees for the statement if (e1) if (e2) S1 else S2

This ambiguity is called the dangling-else problem. The syntax does not tell us whether an else after two if-statements should be associated with the first or second if. C and Pascal solve this problem by enforcing a disambiguating rule, which works as follows: The else is associated with the closest preceding if that does not already have an else part. This rule is also referred to as the most closely nested rule for if-statements. It states that the second parse tree is the correct one.

The fact that the dangling-else problem arises at all indicates an essential language design problem. This is true for two reasons. First, it makes us state a new rule to describe what is essentially a syntactic feature. Second, it makes the interpretation of the if-statement by the reader more difficult; that is, it

violates the readability design criterion. As an illustration, if we want actually to associate the else with the first if in the preceding statement, we would have to write either:

```
if ( e1 ) { if ( e2 ) S1 } else S2
```

or:

```
if ( e1 ) if ( e2 ) S1 else ; else S2
```

There are other ways to solve the dangling else than by using a disambiguating rule. In fact, it is possible to write out BNF rules that specify the association precisely, but these rules make the grammar somewhat more complex. (Java does this—see Exercises 9.28 and 9.29.) A better way is to use a bracketing keyword for the if-statement, such as the Ada rule:

```
if-statement    if condition then sequence-of-statements
                [else sequence-of-statements] end if ;
```

The two bracketing keywords end if (together with the semicolon) close the if-statement and remove the ambiguity, since we must now write either:

```
if e1 then if e2 then S1 end if ; else S2 end if;
```

or:

```
if e1 then if e2 then S1 else S2 end if ; end if ;
```

to decide which if is associated with the else part. This also removes the necessity of using brackets (or a begin - end pair) to open a new sequence of statements. The if-statement can open its own sequence of statements and, thus, becomes fully structured:

```
if x > 0.0 then
    y := 1.0/x;
    done := true;
else
    x := 1.0;
    y := 1.0/z;
    done := false;
end if;
```

A similar approach was taken in the historical (but influential) language Algol68, which suggestively uses keywords spelled backward as bracketing keywords:

```
if e1 then S1 else S2 fi
```

Thus, the bracketing keyword for if-statements is fi. (One still sees this convention in theoretical language design publications—witness the guarded if of Dijkstra, described above.)

An extension of the if-statement simplifies things when there are many alternatives. Multiple else’s statements would have to be written in Ada as:
