# Working with Discinated Unions

If the record can be viewed as a tuple with labels, the discriminated union (DU) can be viewed as a union of different types. Listing 6-30 shows how to define a shape union that contains a circle, triangle, and rectangle. The possible value in the union is called a union case. The shape union has three union cases, and each case has a different type. For example, the triangle case has three double tuples.

**LISTING 6-30** Defining a discriminated union

```
DU with type
type Shape =
| Circle of double
| Triangle of double * * double
| Rectangle of double * double

DU without type
type Number = OddNumber | EvenNumber
```

> Note If the union case is on the same line, the first pipe () is not mandatory.

The DU can be recursive. Just like other recursive types, you can define one in a DU with the **and** keyword. A typical application of the DU recursive feature is to define a tree structure. See Listing 6-31.

**LISTING 6-31** Defining a tree structure using DU

```
Defining a tree using DU
type Tree =
| Tip of int
| Node of int * Tree * Tree

Defining a tree with a recursive type
type Tree =
| Tip of NodeType
| Node of int * Tree * Tree
and NodeType =
| NodeContent of int
```