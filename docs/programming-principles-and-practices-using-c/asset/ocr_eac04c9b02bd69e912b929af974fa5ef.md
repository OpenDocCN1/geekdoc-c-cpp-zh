Basically, writing a loop is simple. Getting it right for real-world problems can be tricky, though. In particular, it can be hard to express the condition correctly and to initialize all variables so that the loop starts correctly.

# TRY THIS

The character **'b'** is **char**('a'+1), **'c'** is **char**('a'+2), etc. Use a loop to write out a table of characters with their corresponding integer values:

```
```
a  97
b  98
...
z 122
```
```

# 4.4.2.2 Blocks

Note how we grouped the two statements that the **while** had to execute:

```
```
while (i<100) {
    cout << i << '\t' << square(i) << "\n";
    ++i ;     // increment i (that is, i becomes i+1)
}
```
```

A sequence of statements delimited by curly braces { and } is called a *block* or a *compound statement*. A block is a kind of statement. The empty block {} is sometimes useful for expressing that nothing is to be done. For example:

```
```
if (a<=b) {    // do nothing
}
else {         // swap a and b
    int t = a;
    a = b;
    b = t;
}
```
```

# 4.4.2.3 for-statements

Iterating over a sequence of numbers is so common that C++, like most other programming languages, has a special syntax for it. A **for**-statement is like a **while**-statement except that the management of the control variable is concentrated