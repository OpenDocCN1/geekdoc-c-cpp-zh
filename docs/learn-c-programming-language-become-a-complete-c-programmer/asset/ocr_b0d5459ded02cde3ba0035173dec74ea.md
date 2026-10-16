```
X::k++; // X's k
}
void f2() {
int i = 0;
using X::i; using X::j; using X::k;
// error :ideclared twice in f2()
// hides global k
i++; j++; // X::j
k++; // X::k
}
```

A locally declared name (declared either by an ordinary declaration or by a using-declaration) hides nonlocal declarations of the same name, and any illegal overloading of the name is detected at the point of declaration.

Note the ambiguity error for k++ in f1(). Global names are not given preference over names from namespaces made accessible in the global scope. This provides significant protection against accidental name clashes, and – importantly – ensures that there are no advantages to be gained from polluting the global namespace.

When libraries declaring many names are made accessible through using-directives, it is a significant advantage that clashes of unused names are not considered errors.

# 14.4.2 Namespace Aliases

If users give their namespaces short names, the names of different namespaces will clash:

```
namespace A {// shor tname,will clash (eventually)
// ...
}
A::String s1 = “Grieg”;
A::String s2 = “Nielsen”;
```

However, long namespace names can be impractical in real code:

Section 14.4.2 Namespace Aliases 407

```
namespace American_Telephone_and_Telegraph { // too long // ...
}
American_Telephone_and_Telegraph::String s3 = “Grieg”;
American_Telephone_and_Telegraph::String s4 = “Nielsen”;
```

This dilemma can be resolved by providing a short alias for a longer namespace name: // use namespace alias to shorten names:

```
namespace ATT = American_Telephone_and_Telegraph;
ATT::String s3 = “Grieg”;
ATT::String s4 = “Nielsen”;
```