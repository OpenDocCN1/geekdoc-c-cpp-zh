# Chapter 12: Generics

The containing type's type parameters are accessible in the nested type in the same way that members of the containing type are also accessible from the nested type. The rule is simply that a type parameter is available anywhere within the body of the type that declares it.

> Guidelines
AVOID shadowing a type parameter of an outer type with an identically named type parameter of a nested type.

# Constraints

Generics support the ability to define constraints on type parameters. These constraints ensure that the types provided as arguments conform to various rules. Take, for example, the BinaryTree<T> class shown in Listing 12.19.

Listing 12.19: Declaring a BinaryTree<T> Class with No Constraints

```
public class BinaryTree<T>
{
    public BinaryTree(T item)
    {
        Item = item;
    }

    public T Item { get; set; }
    public Pair<BinaryTree<T>> SubItems { get; set; }
}
```

(An interesting note is that BinaryTree<T> uses Pair<T> internally, which is possible because Pair<T> is simply another type.)

Suppose you want the tree to sort the values within the Pair<T> value as it is assigned to the SubItems property. To achieve the sorting, the SubItems accessor uses the CompareTo() method of the supplied key, as shown in Listing 12.20.

At compile time, the type parameter T is an unconstrained generic. When the code is written as shown in Listing 12.20, the compiler assumes that the only