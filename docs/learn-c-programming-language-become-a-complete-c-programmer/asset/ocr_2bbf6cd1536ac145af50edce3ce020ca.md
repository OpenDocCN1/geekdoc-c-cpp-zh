programs, so be careful to minimize context dependencies of templates and be very suspicious about macros (§12.6).

If you need more control over the context of instantiation, you can use explicit instantiation and extern templates (§26.2.2).

# 23.7.1 Linkage

The rules for linkage of templates are the rules for linkage of the generated classes and functions (§15.2, §15.2.3). This implies that if the layout of a class template or the definition of an inline function template changes, all code that uses that class or function must be recompiled.

For templates defined in header files and included “everywhere” this can imply a lot of recompilation because templates tend to include a lot of information in header files, more than non-template code using .cpp files. In particular, if dynamically linked libraries are used, care has to be taken that all uses of a template are consistently defined.

Sometimes, it is possible to minimize the exposure to changes in complicated template libraries by encapsulating their use in functions with non-template interfaces. For example, I might like to implement some computations using a general numerical library supporting a wide variety of types (e.g., Chapter 29, §40.4, §40.5, §40.6). However, I often know the type used for my calculations. For example, in a program I may consistently use doubles and vector<double>. In that case, I could define:

```
double accum(const vector<double>& v)
{
return accumulate(v.begin(),v.end(),0.0);
}
```

Given that, I can use the simple non-templated declaration of accum() in my code: double accum(const vector<double>& v);

The dependence on std::accumulate has disappeared into a .cpp file that is not seen by the rest of my code. Also, I suffer the compilation-time overhead of a #include<numeric> only in that .cpp file.

Note that I took the opportunity to simplify the interface to accum() compared to std::accumulate(). The generality that is a key attribute of good template libraries can be seen as a source of complexity in a particular application.

I suspect that I would not use this technique for standard-library templates. Those are stable over years and known to the implementations. In particular, I did not bother to try to encapsulate vector<double>. However, for more complex, esoteric, or frequently changing template libraries, such encapsulation can be useful.

# 23.8 Advice

[1] Use templates to express algorithms that apply to many argument types; §23.1. [2] Use templates to express containers; §23.2.