+   • The ability to pass values as template arguments. This implies opportunities for compile-time computation.

In other words, templates provide a powerful mechanism for compile-time computation and type manipulation that can lead to very compact and efficient code. Remember that types (classes) can contain both (§7.3.2) and values (§7.2.2).

The first and most common use of templates is to support generic programming, that is, programming focused on design, implementation, and use of general algorithms. Here, "general" means that an algorithm can be designed to accept a wide variety of types as long as they meet the algorithm's requirements on its arguments. Together with concepts, the template provides C++'s main support for generic programming. Templates provide (compile-time) parametric polymorphism.

# # 8.2 Concepts

Consider the sum() in §7.3.1:

Click here to view code image

```
template<typename Seq, typename Value>
Value sum(Seq s, Value v)
{
  for (const auto& x : s)
  {
    v+=x;
  }
  return v}
```

sum() requires that

+   • its first template argument is some kind of sequence of elements, and
• its second template argument is some kind of number.

To be specific, sum() requires that

+   • A sequence, Seq, that supports begin() and end() so that the range-for will work (§1.7; §14.1).
• An arithmetic type, Value, which supports += so that the elements of the sequence can be added.

We call such requirements concepts.

Examples of that might satisfy this requirement (and more) for being a sequence (also called a range) include the standard-library vector, list, and map. Examples of types that meet this fulfilled requirement (and more) for being an arithmetic type like int, double, and Matrix (for any reasonable definition of Matrix). We could say that the sum() is generic in two dimensions: the type of the data structure used to store elements (the “sequence”) and the type of elements.

# # 8.2.1 Use of Concepts

Most templates must meet specific requirements for the template to compile properly and for the generated code to work properly. That, most templates should be constrained templates (§7.2.1). The type-name introducer is the least constraining, requiring only