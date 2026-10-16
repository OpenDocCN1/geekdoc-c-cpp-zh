```
template<typename Ran, typename Pred = less<Value_type<Ran>>> // use a default template argument sort(Ran first, Ran last, Pred pred ={}) {
// ... use pred(x,y) ...
}
```

The difference between having two functions and having one with a default argument can be observed by someone taking pointers to functions. However, thinking of many of the variants of the standard algorithms as simply “the version with the default predicate” roughly halves the number of template functions you need to remember.

In some cases, an argument could be interpreted as either a predicate or a value. For example: bool pred(int); auto p = find(b,e,pred); // find element pred or apply predicate ‘pred()? (the latter) In general, a compiler cannot disambiguate such examples, and programmers would get confused even in the cases where the compiler could disambiguate.

To simplify the task for the programmer, the _if suffix is often used to indicate that an algorithm takes a predicate. The reason to distinguish by using two names is to minimize ambiguities and confusion. Consider:

```
using Predicate = bool(*)(int);
```

# Section 32.3 Policy Arguments 931

```
void f(vector<Predicate>& v1, vector<int>& v2) {
auto p1 = find(v1.begin(),v1.end(),pred); // find element with the value pred
auto p2 = find_if(v2.begin(),v2.end(),pred); // count elements for which pred() returns true
}
```

Some operations passed as arguments to an algorithm are meant to modify the element to which they are applied (e.g., some operations passed to for_each(); §32.4.1), but most are predicates (e.g., a comparison object for sort()). Unless otherwise stated, assume that a policy argument passed to an algorithm should not modify an element. In particular, do not try to modify elements through predicates:

```
int n_even(vector<int>& v) // don’t do this
// count the number of even values in v
{
return find_if(v.begin(),v.end(),[](int& x) {++x; return x&1; });
}
```

Modifying an element through a predicate obscures what is being done. If you are really sneaky, you could even modify the sequence (e.g., by inserting or removing an element using the name of a container being iterated over), so that the iteration would fail (probably in obscure ways). To avoid accidents, you may pass arguments to predicates by const reference.

Similarly, a predicate should not carry state that changes the meaning of its operation. The implementation of an algorithm may copy a predicate, and we rarely want repeated uses of a predicate on the same value to give different results. Some function objects passed to algorithms, such as random number generators, do carry mutable state. Unless you are