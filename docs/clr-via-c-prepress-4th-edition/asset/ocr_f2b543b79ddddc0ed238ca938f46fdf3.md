It is also possible to use **dynamic** when specifying generic type arguments to a generic class (reference type), a structure (value type), an interface, a delegate, or a method. When you do this, the compiler converts a dynamic to Object and applies DynamicAttribute to the various pieces of metadata where it makes sense. Note that the generic code that you are using has already been compiled and will silently setup the type to be Object; no dynamic dispatch will be performed because the compiler did not produce any payload code in the generic code.

Any expression can implicitly be cast to dynamic since all expressions result in a type that is derived from Object⁵. Normally, the compiler does not allow you to write code that implicitly casts an expression from Object to another type; you must use explicit cast syntax. However, the compiler does allow you to cast an expression from dynamic to another type using implicit cast syntax.

```
object o1 = 123;       // OK: Implicit cast from Int32 to Object (boxing)
Int32 n1 = o;           // Error: No implicit cast from Object to Int32
Int32 n2 = (Int32) o;   // OK: Explicit cast from Object to Int32 (unboxing)

dynamic d1 = 123;       // OK: Implicit cast from Int32 to dynamic (boxing)
Int32 n3 = d1;          // OK: Implicit cast from dynamic to Int32 (unboxing)
```

While the compiler allows you to omit the explicit cast when casting from dynamic to some other type, the CLR will validate the cast at runtime to ensure that type safety is maintained. If the object’s type is not compatible with the cast, the CLR will throw an InvalidCastException exception.

Note that the result of evaluating a dynamic expression is a dynamic expression. Examine this code:

```
dynamic d = 123;
var result = M(d);  // Note! 'var result' is the same as 'dynamic result'
```

Here, the compiler allows you to compile because it doesn’t know at compile time which M method it will call. Therefore, it also does not know what type of result M will return. And so, the compiler assumes that the result variable is of type dynamic itself. You can verify this by placing your mouse over var in the Visual Studio editor; the IntelliSense window will indicate 'dynamic: Represents an object whose operations will be resolved at runtime.' If the M method invoked at runtime has a return type of void, a Microsoft.CSharp.RuntimeBinder.RuntimeBinderException exception is thrown.

**Important** Do not confuse dynamic and var. Declaring a local variable using var is just a syntactical shortcut that the compiler infers the specific data type from an expression. The var keyword can be used only for declaring local variables inside a method while the dynamic keyword can be used for local variables, fields, and arguments. You cannot cast an expression to var but you can cast an expression to dynamic. You must explicitly initialize a variable declared using var while you do not have to initialize a variable declared with dynamic. For more information about C#’s var, see the “Implicitly Typed Local Variables” section in Chapter 9, “Parameters.”

⁵ And, as always, value types will be boxed.