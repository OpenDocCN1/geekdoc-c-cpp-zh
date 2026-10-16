```
public class B: A
{
    public unsafe override void F(char* p) {...}
}
```

Because the signature for F has a pointer type in it, we can only write it in the unsafe context. We can do this in two ways – as we did with A, we can make the whole class into an unsafe context, or, as we did with B, we can add the unsafe modifier into the method declaration.

# Pointer Types

In the unsafe context, a type can be a value_type, a reference_type, or a pointer_type. However, you can also use a pointer_type in expressions external to unsafe contexts because this type of use is not considered to be unsafe:

```
type_unsafe
  : pointer_type
  ;
```

We write pointer_types as unmanaged_types or we use the void keyword and a * token:

```
pointer_type
  : unmanaged_type '*'
  | 'void' '*'
  ;
```

```
unmanaged_type
  : type
  ;
```