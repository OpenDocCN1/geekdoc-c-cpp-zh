# 11.7.8.3 Extension method invocations

In a method invocation (§11.6.6.2) of one of the forms

```
«expr» . «identifier» ( )
«expr» . «identifier» ( «args» )
«expr» . «identifier» < «typeargs» > ( )
«expr» . «identifier» < «typeargs» > ( «args» )
```

if the normal processing of the invocation finds no applicable methods, an attempt is made to process the construct as an extension method invocation. If «expr» or any of the «args» has compile-time type dynamic, extension methods will not apply.

The objective is to find the best type_name C, so that the corresponding static method invocation can take place:

```
C . «identifier» ( «expr» )
C . «identifier» ( «expr» , «args» )
C . «identifier» < «typeargs» > ( «expr» )
C . «identifier» < «typeargs» > ( «expr» , «args» )
```

An extension method C₁ . Mₑ is eligible if:

+   - C₁ is a non-generic, non-nested class
+   - The name of Mₑ is identifier
+   - Mₑ is accessible and applicable when applied to the arguments as a static method as shown above
+   - An implicit identity, reference or boxing conversion exists from expr to the type of the first parameter of Mₑ.

The search for C proceeds as follows:

+   - Starting with the closest enclosing namespace declaration, continuing with each enclosing namespace declaration, and ending with the containing compilation unit, successive attempts are made to find a candidate set of extension methods:
+     - If the given namespace or compilation unit directly contains non-generic type declarations C₁ with eligible extension methods Mₑ, then the set of those extension methods is the candidate set.
+     - If namespaces imported by using namespace directives in the given namespace or compilation unit directly contain non-generic type declarations C₁ with eligible extension methods Mₑ, then the set of those extension methods is the candidate set.
+   - If no candidate set is found in any enclosing namespace declaration or compilation unit, a compile-time error occurs.
+   - Otherwise, overload resolution is applied to the candidate set as described in §11.6.4. If no single best method is found, a compile-time error occurs.
+   - C is the type within which the best method is declared as an extension method.

Using C as a target, the method call is then processed as a static method invocation (§11.6.6).

> Note: Unlike an instance method invocation, no exception is thrown when expr evaluates to a null reference. Instead, this null value is passed to the extension method as it would be via a regular static method invocation. It is up to the extension method implementation to decide how to respond to such a call. end note