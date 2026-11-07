What if you do something similar with Swap()?

```
    int m = 5;
    double x = 14.3;
    Swap<double>(m, x);  // almost works
```

This generates an explicit instantiation for type double. Unfortunately, in this case, the code won't work because the first formal parameter, being type double &, can't refer to the type int variable m.

Implicit instantiations, explicit instantiations, and explicit specializations collectively are termed specializations. What they all have in common is that they represent a function definition that uses specific types rather than one that is a generic description.

The addition of the explicit instantiation led to the new syntax of using template and template <> prefixes in declarations to distinguish between the explicit instantiation and the explicit specialization. As in many other cases, the cost of doing more is more syntax rules. The following fragment summarizes these concepts:

```
    ...
    template <class T>
    void Swap (T &, T &);   // template prototype

    template <> void Swap<job>(job &, job &);   // explicit specialization for job
    int main(void)
    {
        template void Swap<char>(char &, char &); // explicit instantiation for char
        short a, b;
        ...
        Swap(a,b);   // implicit template instantiation for short
        job n, m;
        ...
        Swap(n, m);  // use explicit specialization for job
        char g, h;
        ...
        Swap(g, h);  // use explicit template instantiation for char
        ...
    }
```

When the compiler reaches the explicit instantiation for char, it uses the template definition to generate a char version of Swap(). For the remaining uses of Swap(), the compiler matches a template to the actual arguments used in the function call. For example, when the compiler reaches the function call Swap(a,b), it generates a short version of Swap() because the two arguments are type short. When the compiler reaches Swap(n,m), it uses the separate definition (the explicit specialization) provided for the job type. When the compiler reaches Swap(g,h), it uses the template specialization it already generated when it processed the explicit instantiation.