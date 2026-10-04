# CHAPTER 2 DEPENDENCE GRAPHS AND SLICING FOR
OBJECT-ORIENTED LANGUAGES

```
class C {
  C f;
  public static void main(String[] args) {
    C c = new C();
    C.rec(c);
    C x = c.f;
    C y = x.f;
  }
  static void rec(C c) {
    c.f = new C();
    x = c.f;
    x.f = c;
  }
}
```

Figure 2.14: Example program illustrating recursive data structures.

![](bbox=[0.301, 0.381, 0.703, 0.574])

Figure 2.15: SDG (without summary edges) for Figure 2.14 including object
trees.

The idea is to start unfolding, when the same field has been observed earlier in this branch of the object tree and the base pointers of these locations have the same points-to-sets. In this case, locations are equivalent with respect to all properties used for computing data dependencies, if the second tree would just add the same information again, rendering one of these locations redundant. The transitive closure ~ R yields an equivalence relation which we leverage to find a unique representative:

When computing the quotient sets Ref/- and ImMod/-, we choose the short-est entry (i.e. the infimum in the extends relation) as representatives. These sets are finite due to the sets in the points-to-relation being finite. We will show later that including these quotient sets (i.e. these representatives) into the dependence graph is sufficient to compute correct slices with respect to field access. This is due to Definition 2.18 of data dependence, which is also based on the aliasing situation.