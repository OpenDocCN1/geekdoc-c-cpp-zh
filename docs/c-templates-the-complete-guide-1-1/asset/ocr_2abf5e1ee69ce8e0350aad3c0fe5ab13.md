```
~~~cpp
template<typename T>
void exchange(T& a, T& b)
{
    T t(a);
    a = b;
    b = t;
}
~~~
```

As with the full specialization of variable templates, the type of a partial specialization is not required to match that of the primary template.

Click here to view code image

```
~~~cpp
template<typename T>
void exchange(T& a, T& b)
{
    T t(a);
    a = b;
    b = t;
}
~~~
```

The rules regarding the kinds of template arguments that can be specified for a variable template partial specialization are identical to those for class template specialization. Similarly, the rules to select a specialization for a given set of concrete template arguments are identical too.

# ## 16.6 ALTERNATES

Full template specialization was part of the C++ template mechanism from the start. Function template overloading and class template partial specialization, on the other hand, came much later. The HP aC++ compiler was the first to implement function template overloading, and EDG's C++ front end was the first to implement class template partial specialization. The partial-ordering process described in this chapter was originally invented by Steve Adamczyk and John Spicer (who are both of EDG).

The ability of template specialization to terminate an otherwise infinitely recursive template definition (such as the IsPrime<> example presented in Section 14.1 on page 246) was known for a long time. However, Erwin Unruh deserves the credit for noting that this could lead to the interesting possibility of computing results at compile time using the template instantiation mechanism to perform nontrivial computations at compile time. We devote Chapter 17 to this topic.

You may legitimately wonder why only class templates and variable templates can be partially specialized. The reasons are mostly historical. It is probably possible to define the same mechanism for function templates (see Chapter 17). In some ways, the effect of overloading function templates is similar, but there are also some subtle differences. These differences are mostly related to the fact that only the primary templates need to be looked up when a use is encountered. The specializations are considered only afterward, to determine which implementation should be used. In contrast, all overloaded function templates must be brought into an overload set by looking them up, and they may come from different namespaces or classes. This increases the likelihood of unintentionally overloading a template name somewhat.

Conversely, it is also imaginable to allow a form of overloading of class templates and variable templates. Here is an example:

Click here to view code image

```
~~~cpp
// invalid overloading of class templates
template<typename T1, typename T2> class Pair;
template<int N1, int N2> class Pair;
~~~
```

However, there doesn't seem to be a pressing need for such a mechanism.

1 This definition differs from that given in the C++ standard, but its consequences are equivalent.

2 Alias templates are the only form of template that cannot be specialized, even by a full specialization or a partial specialization. This restriction is unnecessary to make the use of template aliases transparent to the template argument deduction process (Section 15.2.3 on page 518).

3 The same prefix is not needed to declare full function template specializations. Earlier designs of the C++ language did not include this prefix, but the addition of member templates required additional syntax to disambiguate complex specialization cases.