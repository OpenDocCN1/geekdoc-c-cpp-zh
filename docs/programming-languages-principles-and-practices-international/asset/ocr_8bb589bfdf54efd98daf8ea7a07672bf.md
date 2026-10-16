# ## 8.3 Type Constructors

Since data types are sets, set operations can be used to construct new types out of existing ones. Such operations include Cartesian product, union, powerset, function set, and subset.

When applied to types, these set operations are called **type constructors**. In a programming language, all types are constructed out of the predefined types using type constructors. In the previous section, we have already seen a limited form of one of these constructors—the subset construction—in subrange types. There are also type constructors that do not correspond to mathematical set constructions, with the principal example being pointer types, which involve a notion of storage not present in mathematical sets. There are also some set operations that do not correspond to type constructors, such as intersection (for reasons to be explained). In this section, we will catalog and give examples of the common type constructors.

# ### 8.3.1 Cartesian Product

Given two sets *U* and *V*, we can form the Cartesian or cross product consisting of all ordered pairs of elements from *U* and *V*:

\[ U \times V = \{(u,v) \mid u \text{ is in } U \text{ and } v \text{ is in } V\} \]

Cartesian products come with projection functions \(p_1: U \times V \to U\) and \(p_2: U \times V \to V\), where \(p_1((u,v)) = u\) and \(p_2((u,v)) = v\). This construction extends to more than two sets. Thus \(U \times V \times W = \{(u,v,w) \mid u \text{ in } U, v \text{ in } V, w \text{ in } W\}\). There are as many projection functions as there are components.

In many languages the Cartesian product type constructor is available as the **record** or **structure construction**. For example, in C the declaration

```
```c
struct IntCharReal{
    int i;
    char c;
    double r;
};
```
```

constructs the Cartesian product type **int × char × double**.

In Ada this same declaration appears as:

```
```ada
type IntCharReal is record
    i: integer;
    c: character;
    r: float;
end record;
```
```

However, there is a difference between a Cartesian product and a record structure: In a record structure, the components have names, whereas in a product they are referred to by position. The projections in a record structure are given by the **component selector operation** (or **structure member operation**): If *x* is a variable of type **IntCharReal**, then *x.i* is the projection of *x* to the integers. Some authors, therefore,