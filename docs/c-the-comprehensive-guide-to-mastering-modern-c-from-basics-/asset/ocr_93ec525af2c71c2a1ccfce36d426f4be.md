Here I use the aliases provided by the containers size_type and const_iterator. In this simple case, auto would have worked, but this demonstrates the aliases.

# Interlude: "pair" and "tuple"

As shown in Table 24.3, some containers internally use pair. As you progress through the chapter, you will encounter several methods that also return a pair as a return type. This is nothing but bundling two data types and their values together—essentially:

```
// https://godbot.org/z/xcrbvMlijz
struct PairIntDouble {
    int first;
    double second;
}
int main() {
    PairIntDouble p{2, 7123};
}
```

What I have done here specifically for int and double is possible with std::pair as a template class for any types. You can access the first element with first and the second with second.

A generalization of pair for any number of elements is tuple. For example, you use get<3>(t) to access the fourth element of t.

That should suffice for a discussion of pair and tuple for this chapter. A complete discussion of these two data types can be found in Chapter 28, Section 28.1.