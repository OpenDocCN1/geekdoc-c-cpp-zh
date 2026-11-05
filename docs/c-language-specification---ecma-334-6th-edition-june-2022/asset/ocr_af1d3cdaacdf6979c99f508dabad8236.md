```
Rectangle r = new Rectangle
{
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```

which has the same effect as

```
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

end example

# 11.7.15.4 Collection initializers

A collection initializer specifies the elements of a collection.

```
collection_initializer
: '{' element_initializer_list '}'
| '{' element_initializer_list ';' '}'
;

element_initializer_list
: element_initializer (',' element_initializer)*
;

element_initializer
: non_assignment_expression
| '{' expression_list '}'
;

expression_list
: expression
| expression_list ',' expression
;
```

A collection initializer consists of a sequence of element initializers, enclosed by { and } tokens and separated by commas. Each element initializer specifies an element to be added to the collection object being initialized, and consists of a list of expressions enclosed by { and } tokens and separated by commas. A single-expression element initializer can be written without braces, but cannot then be an assignment expression, to avoid ambiguity with member initializers. The non_assignment_expression production is defined in §11.19.

Example: The following is an example of an object creation expression that includes a collection initializer:

```
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

end example

The collection object to which a collection initializer is applied shall be of a type that implements System.Collections.IEnumerable or a compile-time error occurs. For each specified element in order, normal member lookup is applied to find a member named Add. If the result of the member lookup is not a method group, a compile-time error occurs. Otherwise, overload resolution is applied with the expression