};

// NOW it's complete.

So what seems enough. But if we're doing a linked list? Each linked list node needs to have a reference to another node. But how we can create a reference to another node if we haven't finished declaring the node yet?

C's allowance for incomplete types makes it possible. We can't declare a node, but we can declare a pointer to one, even if it's incomplete!

```
struct node {
  int val;
  struct node *next; // struct node is incomplete, but that's OK!
};
```

Even though the node is incomplete on line 3, we can still declare a pointer to one.

We can do the same thing if we have two different structs that refer to each other:

```
struct a {
  struct b *x; // Refs to `struct b`
};
```

```
struct b {
  struct a *x; // Refs to `struct a`
};
```

We'd never able to make that pair of structures without the relaxed rules for incomplete types.

# 35.2 Incomplete Type Error Messages

Are you getting errors like this?
invalid application of 'sizeof' to incomplete type

invalid use of undefined type

dereferencing pointer to incomplete type
Most likely culprit: you probably forgot to #include the header file that declares the type.

# 35.3 Other Incomplete Types

Declaring a struct or union with no body makes an incomplete type, e.g. struct foo;
enums are incomplete until the closing brace.

void is an incomplete type.

Arrays declared extern with no size are incomplete, e.g.
extern int a[];

If it's a non-extern array with no size followed by an initializer, it's incomplete until the closing brace of the initializer.

> ¹This works because in C, pointers are the same size regardless of the type of data they point to. So the compiler doesn't need to know the size of the struct node at this point; it just needs to know the size of the pointer.