> **ERIC LIPPERT** I generally agree with the annotation above but would make one additional point: var works well when the writer of the code is attempting to communicate "the storage type of this variable is unimportant; what is important is the meaning of the variable, not its implementation details." For example, I'll often write code like `var attributes = ParseMethodAttributes();`—I am saying here that it doesn't matter whether what comes back is AttributeSyntax[] or List<AttributeSyntax>. What matters is that the collection of attributes has been parsed.

> **BILL WAGNER** I freely admit to being guilty of using var extensively. In fact, my habit is to use implicitly typed variables for almost everything except simple types. I find that it's much more important to have a semantic understanding of a variable rather than a syntactic understanding of a variable. In Chris's example, GetPerson() would logically return a Person, or an IPerson, or something derived from Person or from implementing IPerson. In all those cases, I'm fine with that bit of ambiguity. I understand the concept of "a variable that represents something person-like" without knowing its exact type.

The scope of a local variable declared in a local-variable-declaration is the block in which the declaration occurs. It is an error to refer to a local variable in a textual position that precedes the local-variable-declarator of the local variable. Within the scope of a local variable, it is a compile-time error to declare another local variable or constant with the same name.

A local variable declaration that declares multiple variables is equivalent to multiple declarations of single variables with the same type. Furthermore, a variable initializer in a local variable declaration corresponds exactly to an assignment statement that is inserted immediately after the declaration.

# The example

```
void f() {
    int x = 1, y, z = x * 2;
}
```

corresponds exactly to

```
void f() {
    int x; x = 1;
    int y;
    int z; z = x * 2;
}
```