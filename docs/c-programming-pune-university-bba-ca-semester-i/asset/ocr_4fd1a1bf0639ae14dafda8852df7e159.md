# # Error Handling in C Language

**We distinguish between the following types of errors:**

+   1. **Syntax errors**: errors due to the fact that the syntax of the language is not respected.
+   2. **Semantic errors**: errors due to an improper use of program statements.
+   3. **Logical errors**: errors due to the fact that the specification is not respected.
+      [From programming point of view of when]

+   1. **Compile time errors**: syntax errors and static semantic errors indicated by the compiler.
+   2. **Runtime errors**: dynamic semantic errors, and logical errors, that cannot be detected by the compiler (debugging).

# ## Syntax errors

Let us see some examples of syntax errors.

**Example 1: Missing semicolon:**

```
    int a = 5 // semicolon is missing
    Compiler message:
    Example. ‘;’ expected
    int a = 5
```

**Example 2: Errors in expressions:**

```
    x = ( 3 + 5; // missing closing parenthesis ‘)’
    y = 3 + * 5; // missing argument between ‘+’ and ‘*’
```

# ## Semantic errors

Let us see some examples of semantic errors.

**Example 1: Use of a non-initialized variable:**

```
    int i;
    i++; // the variable i is not initialized
```

**Example 2: Type incompatibility:**

```
    int a = "hello"; // the types String and int are not compatible
```