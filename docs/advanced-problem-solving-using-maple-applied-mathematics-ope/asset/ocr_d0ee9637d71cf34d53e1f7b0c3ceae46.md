# diff or Diff – *differentiation or partial differentiation*

Calling Sequence
`diff(f, x1, ..., xj)`

\[
\frac{d^j}{dx_1\cdots dx_j}f
\]

`diff(f, [x1$])`

\[
\frac{d^n}{dx_1^n}f
\]

**Remark:** these calling sequences are also valid with the inert *Diff* command

**Parameters**

- `f` — algebraic expression or an equation
- `x1, x2, ..., xj` — names representing differentiation variables
- `n` — algebraic expression entering differentiation constructs like x$n, representing nth order derivative, assumed to be integer order differentiation

# solve – *solve one or more equations*

Calling Sequence
`solve(equations, variables)`

**Parameters**

- `equations` — equation or inequality, or set or list of equations or inequalities
- `variables` — (optional) name or set or list of names; unknown(s) for which to solve

# fsolve – *solve one or more equations using floating-point arithmetic*

Calling Sequence
`fsolve(equations, variables, complex)`

**Parameters**

- `equations` — equation, set(equation), expression, set(expression), list(equation)
- `variables` — (optional) name or set or list of names; unknown(s) for which to solve
- `complex` — (optional) literal; search for complex solutions

> Note: For simple functions *f(x)*, Maple can use *f′(x)*, *f″(x)*, etc., for derivatives.