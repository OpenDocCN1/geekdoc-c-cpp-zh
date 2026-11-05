```
shift-expression:
  additive-expression
  shift-expression << additive-expression
  shift-expression right-shift additive-expression

relational-expression:
  shift-expression
  relational-expression < shift-expression
  relational-expression > shift-expression
  relational-expression <= shift-expression
  relational-expression >= shift-expression
  relational-expression is type
  relational-expression as type

equality-expression:
  relational-expression
  equality-expression == relational-expression
  equality-expression != relational-expression

and-expression:
  equality-expression
  and-expression & equality-expression

exclusive-or-expression:
  and-expression
  exclusive-or-expression ^ and-expression

inclusive-or-expression:
  exclusive-or-expression
  inclusive-or-expression | exclusive-or-expression

conditional-and-expression:
  inclusive-or-expression
  conditional-and-expression && inclusive-or-expression

conditional-or-expression:
  conditional-and-expression
  conditional-or-expression || conditional-and-expression

null-coalescing-expression:
  conditional-or-expression
  conditional-or-expression ?? null-coalescing-expression

conditional-expression:
  null-coalescing-expression
  null-coalescing-expression ? expression : expression

lambda-expression:
  async_opt anonymous-function-signature => anonymous-function-body

anonymous-method-expression:
  async_opt delegate explicit-anonymous-function-signature_opt block

anonymous-function-signature:
  explicit-anonymous-function-signature
  implicit-anonymous-function-signature

explicit-anonymous-function-signature:
  ( explicit-anonymous-function-parameter-list_opt )

explicit-anonymous-function-parameter-list:
  explicit-anonymous-function-parameter
  explicit-anonymous-function-parameter-list , explicit-anonymous-function-parameter
```