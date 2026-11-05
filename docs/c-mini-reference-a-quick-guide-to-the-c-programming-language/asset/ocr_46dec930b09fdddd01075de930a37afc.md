# 12.2.5. The delegate constraints

```
```csharp
class C1<T> where T : System.Delegate { }
class C2<T> where T : System.MulticastDelegate { }
```
```

The generic type argument T must be a System.Delegate or System.MulticastDelegate type. The delegate constraint enables you to write code that works with delegates in a type-safe manner.