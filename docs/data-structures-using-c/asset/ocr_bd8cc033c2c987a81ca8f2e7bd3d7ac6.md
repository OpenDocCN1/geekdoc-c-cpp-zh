```
begin
    t2 = pop() and t1 = pop()
    push(strcat(ch, t1, t2)
end
ch = get_next_token(E)
end while
3. if ch = '#', while(!emptystack()) pop and display
4. stop
```

Example 3.5 illustrates the conversion of a postfix expression to its prefix form.

# EXAMPLE 3.5

Convert the following postfix expression to its prefix form:

```
AB ^ C x C - DA/EE+/+
```

Solution The conversion of the given postfix expression to its infix form is given in Table 3.12.

# Table 3.12 Postfix to prefix conversion of the expression AB ^ C x C - DA/EE+/+

| Character scanned | Stack contents |
|---|---|
| A | A |
| B | AB |
| ^ | ^AB |
| C | ^ABC |
| x | x^ABC |
| C | x^ABC, C |
| - | --x^ABCC |
| D | --x^ABCC, D |
| A | --x^ABCC, D, A |
| / | --x^ABCC, /DA |
| E | --x^ABCC, /DA, E |
| E | --x^ABCC, /DA, E, E |
| + | --x^ABCC, /DA+ EE |
| / | --x^ABCC, //DA+ EE |
| + | +--x^ABCC//DA+ EE |

# Prefix to Infix Conversion

Algorithm 3.6 illustrates the prefix to infix conversion.

# ALGORITHM 3.6

+   1. Scan expression E from right to left character by character
+      ch = get_next_token(E)
+   2. while(ch != '#') do