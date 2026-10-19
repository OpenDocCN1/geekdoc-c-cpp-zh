# 12.4.4.3 Ranking implicit conversion sequences [over.ics.rank]

10 Otherwise, if the parameter type is not a class:

+   - if the initializer list has one element that is not itself an initializer list, the implicit conversion sequence is the one required to convert the element to the parameter type;

```
void f(int);
f( {'a'} );
// OK: same conversion as char to int
f( {1.0} );
// error: narrowing
```

+   - if the initializer list has no elements, the implicit conversion sequence is the identity conversion.

```
void f(int);
f( { } );
// OK: identity conversion
```

11 In all cases other than those enumerated above, no conversion is possible.

1 This subclause defines a partial ordering of implicit conversion sequences based on the relationships better conversion sequence and better conversion. If an implicit conversion sequence S1 is defined by these rules to be a better conversion sequence than S2, then it is also the case that S2 is a worse conversion sequence than S1. If conversion sequence S1 is neither better than nor worse than conversion sequence S2, S1 and S2 are said to be indistinguishable conversion sequences.

2 When comparing the basic forms of implicit conversion sequences (as defined in 12.4.4.2)

+   - a standard conversion sequence (12.4.4.2.2) is a better conversion sequence than a user-defined conversion sequence or an ellipsis conversion sequence, and

+   - a user-defined conversion sequence (12.4.4.2.3) is a better conversion sequence than an ellipsis conversion sequence (12.4.4.2.4).

3 Two implicit conversion sequences of the same form are indistinguishable conversion sequences unless one of the following rules applies:

```
void f1(int); // #1
void f1(std::initializer_list<long>); // #2
void g1() { f1({42}); } // chooses #2
```

```
void f2(std::pair<const char*, const char*>); // #3
void f2(std::initializer_list<std::string>); // #4
void g2() { f2({"foo","bar"}); } // chooses #4
```

```
void f(int (&&[])); // #1
```