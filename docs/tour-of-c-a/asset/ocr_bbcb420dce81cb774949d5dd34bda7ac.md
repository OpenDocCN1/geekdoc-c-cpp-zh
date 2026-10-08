that the argument be a type. Usually, we can do better than that. Consider that sum() again:

Click here to view code image

```
template<Sequence Seq, Number Num>
Num sum(Seq s, Num v)
{
    for (const auto& x : s)
        v+=x;
    return v;
}
```

That's clearer. Once we have defined what concepts Sequence and Number mean, the compiler can call back by using sum()'s interface, rather than looking at its implementation. This improves error reporting.

However, the performance of sum()'s interface is not complete: "I forget" to say that we should be able to add elements of a Sequence to a Number. We can do that:

Click here to view code image

```
template<Sequence Seq, Number Num>
requires Arithmetic<range_value_t<Seq>, Num>
Num sum(Seq s, Num n);
```

The range_value_t (16.4) of a sequence is the type of the elements in that sequence; it comes from the standard library which names the type of elements in a range (14.1). Arithmetic<X,Y> saves us from accidentally trying to calculate the sum() of a vector<string> or a vector<int> while still accessing vector-in or vector-complex<double>>. Typically, when an algorithm requires arguments of different types, there is a relationship between those that it is good to make explicit.

In this example, we might use +=, for simplicity and flexibility, we could not constrain our template argument too tightly. In particular, we might wanted to express sum in terms of += and rather than use a general concept (Arithmetic) rather than a narrow requirement to "have +=".

Partial specifications (like the first sum()) using concepts can be very useful. Unless the specification is complete, some errors will not be found until instantiation time. However, even partial specifications express intent and are essential for smooth incremental development where we don't initialize all the requirements we need. With mature libraries of concepts, initial specifications will be to perfect.

Surprisingly, requires Arithmetic<range_value_t<Seq>> is a requirements-clause. The template<Sequence Seq> notation is a shorthand for an explicit use of requires Sequence<Seq>. If I liked myself, I could equivalently have written

Click here to view code image

```
template<typename Seq, typename Num>
requires Sequence<Seq&& && Number<Num> && Arithmetic<range_value_t<Seq>, Num>
Num sum(Seq s, Num n);
```

On the other hand, we could also use the equivalence between the two notations to write:

Click here to view code image