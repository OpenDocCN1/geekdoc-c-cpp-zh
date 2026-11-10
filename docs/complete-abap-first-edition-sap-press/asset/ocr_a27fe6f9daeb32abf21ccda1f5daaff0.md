Also can be written as

```
DATA : v_name(20) TYPE c,
       v_age TYPE i.
```

End the last statement in the chain with a period. Chained statements are not limited to keywords; you can put any identical first part of a chain of statements before the colon and write the remaining parts of the individual statements separated by comma—for example,

```
v_total = v_total + 1.
v_total = v_total + 2.
v_total = v_total + 3.
v_total = v_total + 4.
```

can be chained as

```
v_total = v_total + : 1, 2, 3, 4.
```

> **Note**
> 
> ABAP code is not case-sensitive, so you can use either uppercase or lowercase to write ABAP statements. We recommend writing keywords and their additions in uppercase and using lowercase for other words in the statement to make the code more legible.

# 4.2.3 Comment Lines

To make your source code easy to understand for other programmers, you can add comments to it (see Listing 4.2). *Comment lines* are ignored by the system when the program is generated, and they're useful in many ways.

```
DATA f1 TYPE c LENGTH 2 VALUE '13'.
DATA f2 TYPE n LENGTH 2.
*This is a comment line
f2 = f1.
WRITE f2. "This is also a comment line
```

**Listing 4.2** Comment lines

There are two ways to add comment lines in source code:

+   - You can enter an asterisk (*) at the beginning of a line to make the entire line a comment.
+   - You can enter a double quotation mark (") midline to make the part of the line after the quotation mark a comment; this is called an *in-line comment*.