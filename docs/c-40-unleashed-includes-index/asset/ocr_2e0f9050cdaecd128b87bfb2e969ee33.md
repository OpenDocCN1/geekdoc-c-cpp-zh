![](bbox=[0.11, 0.11, 0.78, 0.6])

FIGURE 21.18 Some binary and unary expression tree node types.

In addition to BinaryExpression and UnaryExpression, some related node types have been included in the figure. TypeBinaryExpression is used for type-related operations such as the TypeIs (is in C#) and TypeAs (as in C#) node types. Conversions are represented as regular unary expression with a Convert or ConvertCheck node type, which correspond to operations like casts in C#. Finally, the ConditionalExpression is the equivalent to C#'s conditional operator, which really is a ternary operator.

# Instantating Objects

Another operation that can be captured in expressions is the creation of objects. C# and other languages have various ways to do this, ranging from plain constructor calls to the use of initializer expressions, including the ones targeting collections. Figure 21.19 illustrates all the expression tree nodes that fall into the category of object instantiation.

The initializer forms are slightly more complicated than other expressions because they capture additional reflection information about the members being initialized. For example, if you write the following:

```
new Foo { Bar = x }
```

In this case, you're calling the default constructor on Foo (but you could be calling another one, too), followed by an assignment to the Bar property or field, using another expression x. This MemberInitExpression decomposes into a NewExpression that captures information about the constructor call, as well as a series of bindings that each contain what expression is bound to what property. For anonymous types, things are slightly different, where the NewExpression's Members property is used to refer to the properties that got initialized.