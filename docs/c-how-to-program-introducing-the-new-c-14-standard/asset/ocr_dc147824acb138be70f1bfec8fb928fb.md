# Section 16.3.4 Lambda Return Types

+   - The compiler can infer a lambda’s return type if the body contains a statement of the form

```
return expression;
```

Otherwise, the lambda’s return type is `void`, unless you explicitly specify a return type using C++11’s trailing return type syntax (`-> type`), as in

```
[](parameterList) -> type {lambdaBody}
```