```
(Ast.Expr.FunApply (v, arg, rest)) | Some
| ->
  (Ast.Expr.Var v, rest) | Some
|LPAREN (Expression (e, RPAREN rest)) ->
  (e, rest) | Some
| ->
  None
```

```
and (|Term|_|) = function
| Factor (el, rest) ->
  match rest with
    MUL (Term (e1, e2), rest) ->
      (Ast.Expr.Prod (e1, e2), rest) | Some
    DIV (Term (e2, rest)) ->
      (Ast.Expr.Ratio (e1, e2), rest) | Some
    -> =
      (el, rest) | Some
| ->
  None
```

```
and (|Sum|_|) = function
| Term (el, rest) ->
  match rest with
    PLUS (Sum (e2, rest)) ->
      (Ast.Expr.Sum (el, e2), rest) | Some
    MINUS (Sum (e2, rest)) ->
      (Ast.Expr.Diff (el, e2), rest) | Some
    -> =
      (el, rest) | Some
| ->
  None
```

```
and (|Expression|_|) = (|Sum|_)
let (Eof|_|) = s =
  if String.IsNullOrEmpty s then
    () | Some
  else
    match s with
      WHITESPACE (_, rest) when rest Is String.isNullOrEmpty ->
        () | Some
      | =
        None
```

# # The Evaluator Module

This module implements your evaluator — a function that takes AST terms and evaluates them with respect to an environment. You will model the environment as a list of string-float pairs that map a float value to a given variable.