
The assignment to d3 shows how no conversion exists if the method is not applicable. The assignment to d4 shows how the method must be applicable in its normal form. The assignment to d5 shows how parameter and return types of the delegate and method are allowed to differ only for reference types.

*end example*

As with all other implicit and explicit conversions, the cast operator can be used to explicitly perform a particular conversion.

Example: Thus, the example

```
object obj = new EventHandler(myDialog.OkClick);
```

could instead be written

```
object obj = (EventHandler)myDialog.OkClick;
```

*end example*

A method group conversion can refer to a generic method, either by explicitly specifying type arguments within E, or via type inference (§11.6.3). If type inference is used, the parameter types of the delegate are used as argument types in the inference process. The return type of the delegate is not used for inference. Whether the type arguments are specified or inferred, they are part of the method group conversion process; these are the type arguments used to invoke the target method when the resulting delegate is invoked.

Example:

```
delegate int D(string s, int i);
delegate int E();

class X
{
    public static T F<T>(string s, T t) {...}
    public static T G<T>() {...}

    static void Main()
    {
        D d1 = F<int>;      // Ok, type argument given explicitly
        D d2 = F;           // Ok, int inferred as type argument
        E e1 = G<int>;      // Ok, type argument given explicitly
        E e2 = G;           // Error, cannot infer from return type
    }
}
```

*end example*

Method groups may influence overload resolution, and participate in type inference. See §11.6 for further details.

The run-time evaluation of a method group conversion proceeds as follows:

- If the method selected at compile-time is an instance method, or it is an extension method which is accessed as an instance method, the target object of the delegate is determined from the instance expression associated with E:
  - The instance expression is evaluated. If this evaluation causes an exception, no further steps are executed.
  - If the instance expression is of a *reference_type*, the value computed by the instance expression becomes the target object. If the selected method is an instance method and the target object is null, a `System.NullReferenceException` is thrown and no further steps are executed.
  - If the instance expression is of a *value_type*, a boxing operation (§10.2.9) is performed to convert the value to an object, and this object becomes the target object.
- Otherwise, the selected method is part of a static method call, and the target object of the delegate is null.
- A delegate instance of delegate type D is obtained with a reference to the method that was determined at compile-time and a reference to the target object computed above, as follows:
  - The conversion is permitted (but not required) to use an existing delegate instance that already contains these references.
  - If an existing instance was not reused, a new one is created (§19.5). If there is not enough memory available to allocate the new instance, a `System.OutOfMemoryException` is thrown. Otherwise the instance is initialized with the given references.

## 11. Expressions

### 11.1 General

An expression is a sequence of operators and operands. This clause defines the syntax, order of evaluation of operands and operators, and meaning of expressions.

### 11.2 Expression classifications

#### 11.2.1 General

The result of an expression is classified as one of the following:

- A value. Every value has an associated type.
- A variable. Every variable has an associated type, namely the declared type of the variable.
- A null literal. An expression with this classification can be implicitly converted to a reference type or nullable value type.
- An anonymous function. An expression with this classification can be implicitly converted to a compatible delegate type or expression tree type.
- A property access. Every property access has an associated type, namely the type of the property. Furthermore, a property access may have an associated instance expression. When an accessor of an instance property access is invoked, the result of evaluating the instance expression becomes the instance represented by `this` (§11.7.12).
- An indexer access. Every indexer access has an associated type, namely the element type of the indexer. Furthermore, an indexer access has an associated instance expression and an associated argument list. When an accessor of an indexer access is invoked, the result of evaluating the instance expression becomes the instance represented by `this` (§11.7.12), and the result of evaluating the argument list becomes the parameter list of the invocation.
- Nothing. This occurs when the expression is an invocation of a method with a return type of `void`. An expression classified as nothing is only valid in the context of a `statement_expression` (§12.7) or as the body of a `lambda_expression` (§11.16).

For expressions which occur as subexpressions of larger expressions, with the noted restrictions, the result can also be classified as one of the following:

- A namespace. An expression with this classification can only appear as the left-hand side of a `member_access` (§11.7.6). In any other context, an expression classified as a namespace causes a compile-time error.
- A type. An expression with this classification can only appear as the left-hand side of a `member_access` (§11.7.6). In any other context, an expression classified as a type causes a compile-time error.
- A method group, which is a set of overloaded methods resulting from a member lookup (§11.5). A method group may have an associated instance expression and an associated type argument list. When an instance method is invoked, the result of evaluating the instance expression becomes the instance represented by *this* (§11.7.12). A method group is permitted in an *invocation_expression* (§11.7.8) or a *delegate_creation_expression* (§11.7.15.6), and can be implicitly converted to a compatible delegate type (§10.8). In any other context, an expression classified as a method group causes a compile-time error.
- An event access. Every event access has an associated type, namely the type of the event. Furthermore, an event access may have an associated instance expression. An event access may appear as the left-hand operand of the += and -= operators (§11.18.4). In any other context, an expression classified as an event access causes a compile-time error. When an accessor of an instance event access is invoked, the result of evaluating the instance expression becomes the instance represented by *this* (§11.7.12).

A property access or indexer access is always reclassified as a value by performing an invocation of the *get_accessor* or the *set_accessor*. The particular accessor is determined by the context of the property or indexer access: If the access is the target of an assignment, the *set_accessor* is invoked to assign a new value (§11.18.2). Otherwise, the *get_accessor* is invoked to obtain the current value (§11.2.2).

An *instance accessor* is a property access on an instance, an event access on an instance, or an indexer access.

#### 11.2.2 Values of expressions

Most of the constructs that involve an expression ultimately require the expression to denote a *value*. In such cases, if the actual expression denotes a namespace, a type, a method group, or nothing, a compile-time error occurs. However, if the expression denotes a property access, an indexer access, or a variable, the value of the property, indexer, or variable is implicitly substituted:

- The value of a variable is simply the value currently stored in the storage location identified by the variable. A variable shall be considered definitely assigned (§9.4) before its value can be obtained, or otherwise a compile-time error occurs.
- The value of a property access expression is obtained by invoking the *get_accessor* of the property. If the property has no *get_accessor*, a compile-time error occurs. Otherwise, a function member invocation (§11.6.6) is performed, and the result of the invocation becomes the value of the property access expression.
- The value of an indexer access expression is obtained by invoking the *get_accessor* of the indexer. If the indexer has no *get_accessor*, a compile-time error occurs. Otherwise, a function member invocation (§11.6.6) is performed with the argument list associated with the indexer access expression, and the result of the invocation becomes the value of the indexer access expression.

### 11.3 Static and Dynamic Binding

#### 11.3.1 General

*Binding* is the process of determining what an operation refers to, based on the type or value of expressions (arguments, operands, receivers). For instance, the binding of a method call is determined based on the type of the receiver and arguments. The binding of an operator is determined based on the type of its operands.

In C# the binding of an operation is usually determined at compile-time, based on the compile-time type of its subexpressions. Likewise, if an expression contains an error, the error is detected and reported by the compiler. This approach is known as *static binding*.
