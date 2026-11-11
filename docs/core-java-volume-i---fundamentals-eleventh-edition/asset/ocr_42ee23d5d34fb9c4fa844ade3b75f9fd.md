In the third variant, all parameters are passed to the static method: Math::pow is equivalent to (x, y) -> Math.pow(x, y).

Table 6.1 walks you through additional examples.

Note that a lambda expression can only be rewritten as a method reference if the body of the lambda expression calls a single method and doesn't do anything else. Consider the lambda expression

```
s -> s.length() == 0
```

There is a single method call. But there is also a comparison, so you can't use a method reference here.

> > **NOTE:** When there are multiple overloaded methods with the same name, the compiler will try to find from the context which one you mean. For example, there are two versions of the Math.max method, one for integers and one for double values. Which one gets picked depends on the method parameters of the functional interface to which Math::max is converted. Just like lambda expressions, method references don't live in isolation. They are always turned into instances of functional interfaces.

> > **NOTE:** Sometimes, the API contains methods that are specifically intended to be used as method references. For example, the Objects class has a method isNull to test whether an object reference is null. At first glance, this doesn't seem useful because the test obj == null is easier to read than Objects.isNull(obj). But you can pass the method reference to any method with a Predicate parameter. For example, to remove all null references from a list, you can call

```
list.removeIf(Objects::isNull);
    // A bit easier to read than list.removeIf(e -> e == null);
```

> > **NOTE:** There is a tiny difference between a method reference with an object and its equivalent lambda expression. Consider a method reference such as separator::equals. If separator is null, forming separator::equals immediately throws a NullPointerException. The lambda expression x -> separator.equals(x) only throws a NullPointerException if it is invoked.

You can capture the this parameter in a method reference. For example, this::equals is the same as x -> this.equals(x). It is also valid to use super. The method expression

```
super::instanceMethod
```