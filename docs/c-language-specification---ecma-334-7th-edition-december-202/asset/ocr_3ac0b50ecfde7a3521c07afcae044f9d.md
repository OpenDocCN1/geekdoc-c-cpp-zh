```
struct_modifier
  : 'new'
  | 'public'
  | 'protected'
  | 'internal'
  | 'private'
  | 'readonly'
  | unsafe_modifier  // unsafe code support
  ;
```

unsafe_modifier (§23.2) is only available in unsafe code (§23).

It is a compile-time error for the same modifier to appear multiple times in a struct declaration.

Except for readonly, the modifiers of a struct declaration have the same meaning as those of a class declaration (§15.2.2).

The readonly modifier indicates that the struct_declaration declares a type whose instances are immutable.

A readonly struct has the following constraints:

+   - Each of its instance fields shall also be declared readonly.
+   - None of its instance properties shall have a set_accessor_declaration (§15.7.3).
+   - It shall not declare any field-like events (§15.8.2).

When an instance of a readonly struct is passed to a method, its this is treated like an in argument/parameter, which disallows write access to any instance fields (except by constructors).

# 16.2.3 Ref modifier

The ref modifier indicates that the struct_declaration declares a type whose instances are allocated on the execution stack. These types are called ref struct types. The ref modifier declares that instances may contain ref-like fields, and may not be copied out of its safe-context (§16.4.12). The rules for determining the safe context of a ref struct are described in §16.4.12.

It is a compile-time error if a ref struct type is used in any of the following contexts:

+   - As the element type of an array.
+   - As the declared type of a field of a class or a struct that does not have the ref modifier.
+   - Being boxed to System.ValueType or System.Object.
+   - As a type argument.
+   - As the type of a tuple element.
+   - An async method.
+   - An iterator.
+   - There is no conversion from a ref struct type to the type object or the type System.ValueType.
+   - A ref struct type shall not be declared to implement any interface.
+   - An instance method declared in object or in System.ValueType but not overridden in a ref struct type shall not be called with a receiver of that ref struct type.