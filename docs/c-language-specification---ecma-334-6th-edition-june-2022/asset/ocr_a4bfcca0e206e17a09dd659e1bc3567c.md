```
class X
{
    A.Stream s1; // Error, A is ambiguous
    A::Stream s2; // Ok
}
```

the name A has two possible meanings in the second namespace body because both the class A and the using alias A are in scope. For this reason, use of A in the qualified name A.Stream is ambiguous and causes a compile-time error to occur. However, use of A with the :: qualifier is not an error because A is looked up only as a namespace alias.

*end example*