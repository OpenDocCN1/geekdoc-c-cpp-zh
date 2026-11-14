A SemiGroup with an identity is a Monoid:

Click here to view code image

```
template <typename Op, typename Value>
concept Monoid =
    SemiGroup<Op, Value> &&
    requires (Op op, Value x)
    {
        {identity(op, x)} -> std::same_as<Value>;
        requires monoid_map<Op, Value>;
    };
```

The compiler can check the existence of a function `identity` and that its return type is `Value`. Whether this identity element actually behaves like an identity element must be declared by the user in `monoid_map`.

The concept `Commutative` refines `Magma` in another sense: the interchangeability of arguments. This is a semantic property that must be explicitly declared:

Click here to view code image

```
template <typename Op, typename Value>
concept Commutative =
    Magma<Op, Value> &&
    commutative_map<Op, Value>;
```

The concept `CommutativeMonoid` that we already saw in the previous section is now just a refinement from `Commutative` and `Monoid`:

Click here to view code image

```
template <typename Op, typename Value>
concept CommutativeMonoid =
    Monoid<Op, Value> && Commutative<Op, Value>;
```

However, now we have a detailed hierarchy of semantic concepts and can constrain our functions very precisely.

There are many more algebraic structures that can be expressed by concepts and the author did this in his academic work. This is summarized in the paper “Integrating Semantics and Compilation: Using C++ Concepts to Develop Robust and Efficient Reusable Libraries” [22] and more extensively discussed in the technical report “The Fundamental Algebraic Concepts in Concept-Enabled C++” [18].