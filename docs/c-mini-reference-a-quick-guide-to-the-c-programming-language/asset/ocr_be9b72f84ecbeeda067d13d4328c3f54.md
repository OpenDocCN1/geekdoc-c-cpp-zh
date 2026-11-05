# 12.2.1. The notnull constraint

```
class <T> where T : notnull { }
```

The type argument T must be a non-nullable type. You can use the notnull constraint to specify that the type argument must be a non-nullable value type or non-nullable reference type. Unlike most other constraints, if a type argument violates the notnull constraint, the compiler generates a warning instead of an error.