# 12.2.6. The struct constraint

```
class <T> where T : struct { }
```

The type argument T must be a non-nullable value type. Because all value types have an accessible parameterless constructor, the struct constraint implies the new() constraint, and they cannot be combined.