# 12.17.6 Named Arguments in Method Calls (C# 4.0)

The parameter name corresponding to an argument expression in the actual-list of a method call (page 74) may be explicitly specified using a named argument, which must have one of these three forms:

+   - parametername: expression
- parametername: out expression
- parametername: ref expression

This means that the argument expressions may be given in any order, not just the order in which they appear in the method's formal parameter list. Also, named arguments considerably improve code clarity when multiple arguments have the same type and there is no (universagreed) natural order of the arguments (example 99).

The argument expressions are evaluated from left to right. Named arguments must appear after all unnamed arguments.

In an instance method call o.M(actual-list), argument named in the actual-list are resolved against the parameter names given in the compile-time type of o. That is, the parameter names in overriding methods M in the compile-time type of o are ignored.

# 12.17.7 Calling a Method with Optional Parameters (C# 4.0)

A call may leave out argument expressions for optional parameters (see section 10.10 and example 60). In overloading, a method with the correct number of parameters is considered better than one with optional parameters.

# 12.17.8 Dynamic Resolution of Method Calls (C# 4.0)

When the o of an instance method call o.M(...) has type dynamic (section 18), the implementation of M is resolved at run-time instead of compile-time, and the call expression has type dynamic regardless of the declared types of possible target M.

Likewise, when an argument e of a method call M(...) has type dynamic, method overloading is resolved at run-time instead of compile-time, and the call expression has type dynamic regardless of the declared types of possible target M.

For purposes of overloading resolution and finding the best method signature (section 12.17.1), the types dynamic and Object are indistinguishable.

A dynamically resolved method call ignores extension methods and cannot take an anonymous method expression (section 12.22) or lambda expression (section 12.23) as argument. See also sections 6.4 and 18 and their examples.