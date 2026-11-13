# FIGURE 7.13 Example Computation for the Algorithm of Figure 7.12

# Example

```
Convert the infix expression:
3 * X + ( Y - 12 ) - Z
```

(a) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand 3 is printed.
Output so far:
3

(b) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The * is pushed.
Output so far:
3

(c) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand X is printed.
Output so far:
3 X

(d) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Pop and print the * since it has higher precedence than the +; then push the +.
Output so far:
3 X *

(e) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Push the parenthesis.
Output so far:
3 X *

(f) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand Y is printed.
Output so far:
3 X * Y

(g) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The - is pushed.
Output so far:
3 X * Y

(h) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand 12 is printed.
Output so far:
3 X * Y 12

(i) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Pop until left parenthesis.
Output so far:
3 X * Y 12 -

(j) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Pop and print the + since it has precedence equal to the -; then push the -.
Output so far:
3 X * Y 12 - +

(k) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
The operand Z is printed.
Output so far:
3 X * Y 12 - + Z

(l) Input so far (shaded):
3 * X + ( Y - 12 ) - Z
Pop any remaining operations.
Output so far:
3 X * Y 12 - + Z -