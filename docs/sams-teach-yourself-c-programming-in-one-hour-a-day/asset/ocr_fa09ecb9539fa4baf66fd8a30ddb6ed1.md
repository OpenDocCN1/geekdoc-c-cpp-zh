"How now brown cow"

This literal string is different from the following:

How now brown cow

The difference is a result of the additional spaces. With a literal string, C keeps track of the white space.

Although it's extremely bad form, the following is legal code in C:

```
printf(
  "Hello, world!"
  );
```

This, however, is not legal:

```
printf("Hello,
world!");
```

To break a literal string constant line, you must use the backslash character (\) just before the break. Thus, the following is legal:

```
printf("Hello,\nworld!");
```

# Creating a Null Statement

If you place a semicolon by itself on a line, you create a null statement. A null statement is one that doesn't perform any action. This is perfectly legal in C. Later in this book, you learn how the null statement can be useful.

# Working with Compound Statements

A compound statement, also called a block, is a group of two or more C statements enclosed in braces. Here's an example of a:

```
{
  printf("Hello, *");
  printf("world!");
}
```

In C, a block can be used anywhere a single statement can be used. Many examples of this appear throughout this book. Note that the enclosing braces can be positioned in different ways. The following is equivalent to the preceding example:

```
{printf("Hello, *");
printf("world!");}
```