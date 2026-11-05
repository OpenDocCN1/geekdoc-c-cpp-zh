
```
public class A
{
    protected int x;
    static void F(A a, B b) {
        a.x = 1;    // Ok
        b.x = 1;    // Ok
    }
}
public class B: A
{
    static void F(A a, B b) {
        a.x = 1;    // Error, must access through instance of B
        b.x = 1;    // Ok
    }
}
```

within A, it is possible to access x through instances of both A and B, since in either case the access takes place through an instance of A or a class derived from A. However, within B, it is not possible to access x through an instance of A, since A does not derive from B. end example]

[Example:

```
class C<T>
{
    protected T x;
}
class D<T>: C<T>
{
    static void F() {
        D<T> dt = new D<T>();
        D<int> di = new D<int>();
        D<string> ds = new D<string>();
        dt.x = default(T);
        di.x = 123;
        ds.x = "test";
    }
}
```

Here, the three assignments to x are permitted because they all take place through instances of class types constructed from the generic type. end example]

[Note: The accessibility domain (§8.5.3) of a protected member declared in a generic class includes the program text of all class declarations derived from any type constructed from that generic class. In the example:

```
class C<T>
{
    protected static T x;
}
class D: C<string>
{
    static void Main() {
        C<int>.x = 5;
    }
}
```

the reference to protected member C<int>.x in D is valid even though the class D derives from C<string>. end note]

## 8.5.5 Accessibility constraints

Several constructs in the C# language require a type to be at least as accessible as a member or another type. A type T is said to be at least as accessible as a member or type M if the accessibility domain of T is a superset of the accessibility domain of M. In other words, T is at least as accessible as M if T is accessible in all contexts in which M is accessible.

The following accessibility constraints exist:

- The direct base class of a class type shall be at least as accessible as the class type itself.
- The explicit base interfaces of an interface type shall be at least as accessible as the interface type itself.
- The return type and parameter types of a delegate type shall be at least as accessible as the delegate type itself.
- The type of a constant shall be at least as accessible as the constant itself.
- The type of a field shall be at least as accessible as the field itself.
- The return type and parameter types of a method shall be at least as accessible as the method itself.
- The type of a property shall be at least as accessible as the property itself.
- The type of an event shall be at least as accessible as the event itself.
- The type and parameter types of an indexer shall be at least as accessible as the indexer itself.
- The return type and parameter types of an operator shall be at least as accessible as the operator itself.
- The parameter types of an instance constructor shall be at least as accessible as the instance constructor itself.

[Example: In the following code
```
class A {...}
public class B: A {...}
```
the B class results in a compile-time error because A is not at least as accessible as B. end example]

[Example: Likewise, in the following code
```
class A {...}
public class B
{
    A F() {...}
    internal A G() {...}
    public A H() {...}
}
```
the H method in B results in a compile-time error because the return type A is not at least as accessible as the method. end example]

## 8.6 Signatures and overloading

Methods, instance constructors, indexers, and operators are characterized by their signatures:

- The signature of a method consists of the name of the method, the number of type parameters, and the type and parameter-passing mode (value, reference, or output) of each of its formal parameters, considered in the order left to right. For these purposes, any type parameter of the method that occurs in the type of a formal parameter is identified not by its name, but by its ordinal position in the type parameter list of the method. The signature of a method specifically does not include the return type, parameter names, type parameter names, type parameter constraints, the params or this parameter modifiers, nor whether parameters are required or optional.
- The signature of an instance constructor consists of the type and parameter-passing mode (value, reference, or output) of each of its formal parameters, considered in the order left to right. The

```
void F<S,T>(S s);        // F<'0','1>('0)
void F<T,S>(S s);        // F<'0','1>('1)  ok
}
```

Note that any ref and out parameter modifiers (§15.6.2) are part of a signature. Thus, F(int), F(ref int), and F(out int) are all unique signatures. However, F(ref int) and F(out int) cannot be declared within the same interface because their signatures differ solely by ref and out. Also, note that the return type and the params modifier are not part of a signature, so it is not possible to overload solely based on return type or on the inclusion or exclusion of the params modifier. As such, the declarations of the methods F(int) and F(params string[]) identified above, result in a compile-time error. end example

## 8.7 Scopes

### 8.7.1 General

The scope of a name is the region of program text within which it is possible to refer to the entity declared by the name without qualification of the name. Scopes can be nested, and an inner scope may redeclare the meaning of a name from an outer scope. (This does not, however, remove the restriction imposed by §8.3 that within a nested block it is not possible to declare a local variable or local constant with the same name as a local variable or local constant in an enclosing block.) The name from the outer scope is then said to be hidden in the region of program text covered by the inner scope, and access to the outer name is only possible by qualifying the name.

- The scope of a namespace member declared by a namespace-member-declaration (§14.6) with no enclosing namespace-declaration is the entire program text.
- The scope of a namespace member declared by a namespace-member-declaration within a namespace-declaration whose fully qualified name is N, is the namespace-body of every namespace-declaration whose fully qualified name is N or starts with N, followed by a period.
- The scope of a name defined by an extern-alias-directive (§14.4) extends over the using-directives, global-attributes and namespace-member-declarations of its immediately containing compilation-unit or namespace-body. An extern-alias-directive does not contribute any new members to the underlying declaration space. In other words, an extern-alias-directive is not transitive, but, rather, affects only the compilation-unit or namespace-body in which it occurs.
- The scope of a name defined or imported by a using-directive (§14.5) extends over the global-attributes and namespace-member-declarations of the compilation-unit or namespace-body in which the using-directive occurs. A using-directive may make zero or more namespace or type names available within a particular compilation-unit or namespace-body, but does not contribute any new members to the underlying declaration space. In other words, a using-directive is not transitive but rather affects only the compilation-unit or namespace-body in which it occurs.
- The scope of a type parameter declared by a type-parameter-list on a class-declaration (§15.2) is the class-base, type-parameter-constraints-clauses, and class-body of that class-declaration. [Note: Unlike members of a class, this scope does not extend to derived classes. end note]
- The scope of a type parameter declared by a type-parameter-list on a struct-declaration (§16.2) is the struct-interfaces, type-parameter-constraints-clauses, and struct-body of that struct-declaration.
- The scope of a type parameter declared by a type-parameter-list on an interface-declaration (§18.2) is the interface-base, type-parameter-constraints-clauses, and interface-body of that interface-declaration.
- The scope of a type parameter declared by a type-parameter-list on a delegate-declaration (§20.2) is the return-type, formal-parameter-list, and type-parameter-constraints-clauses of that delegate-declaration.
- The scope of a type parameter declared by a type-parameter-list on a method-declaration (§15.6.1) is the method-declaration.
