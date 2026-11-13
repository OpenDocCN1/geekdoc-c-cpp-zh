```
ch = pop() from operator Stack and push 'ch' in
display Stack
end while
ch = get_next_token(E)
end while
3. if (ch == '*') then
while(!emptystack(operator))
ch = pop(operator)
push ch on display stack
end while
4. while(!emptystack(display))
ch = pop(operator)
display ch
end while
5. stop
```

Example 3.3 illustrates the conversion of an infix expression to its prefix form.

# EXAMPLE 3.3 Convert the following infix expression to its corresponding prefix form:

```
A ^ B x C - C + D / A(E + F)
```

Solution The conversion to prefix notation is as given in Table 3.10

# Table 3.10 Infix to prefix conversion of the expression A ^ B x C - C + D / A(E + F)

| Character scanned | Stack | Prefix expression |
|---|---|---|
| ) | ) | F |
| F | ) | F |
| + | )+ | F |
| E | )+ | EF |
| ( | Empty | +EF |
| / | / | +EF |
| A | / | A+EF |
| I | // | A + EF |
| D | // | DA + EF |
| + | + | //DA + EF |
| C | + | //DA + EF |
| - | +- | C//DA + EF |
| C | +- | CC//DA + EF |
| x | +-x | CCI//DA + EF |
| B | +-x | BCCI//DA + EF |
| ^ | +-x^ | BCCI//DA + EF |
| A | +-x^ | ABCCI//DA + EF |
| | Empty | +-x^ABCCI//DA + EF |