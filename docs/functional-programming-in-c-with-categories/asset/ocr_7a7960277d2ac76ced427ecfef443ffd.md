```
var list = new Cons<int>(value: 2,
    rest: new Cons<int>(value: 5,
        rest: new Empty<int>()));
```

This definition is the base definition of a List. Furthermore, because of its significance, we will often use this simple algebraic form of the List to display many functional ideas.

In practical terms giving recursive definitions means that we can progressively compose more complex entities out of simpler objects by applying some operations between them. The following three ways to combine structures are the most pervasive in programming.

+   1. **Product** [object-oriented equivalent: **composition**]: In our definition of the list the object literal that has two properties is a product
+   `Cons(T value, ListBase<T> rest)`
+   2. **Coproduct** [object-oriented equivalent: **inheritance**]: In our definition of the list, `Cons<T> : ListBase<T>`, and `Empty<T> : ListBase<T>` form a co-product, commonly called a union type. In object-oriented terms, simple inheritance is a union type.
+   3. **Recursive Type** [object-oriented equivalent: **a type that contains objects of the same Type or inheriting type**]: The fact that in
+   `Cons<T> : ListBase<T> {public ListBase<T> Rest { get; set; }}`
+   the Rest is a ListBase<T>Type means that we have a recursive definition.

The fact that a data type can be formed by applying some operations between them gives them the name **algebraic**. An **algebraic data type** is a kind of composite type.

Now, if we define those three operations in any language or programming paradigm, we can define a list by following the algebraic definition “A list is **either** an **empty list** or a **concatenation** of an **element** and a **list.**”. If someone tells us how to form a product a coproduct and a recursive type in Java or python or Elm we can instantly write a definition of a list without the need to be experts of the language.