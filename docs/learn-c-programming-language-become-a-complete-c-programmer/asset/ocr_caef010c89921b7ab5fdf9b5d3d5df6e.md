For this reason, {} initialization is sometimes referred to as universal initialization: the notation can be used everywhere. In addition, {} initialization is uniform: wherever you initialize an object of type X with a value v using the {v} notation, the same value of type X (X{v}) is created.

The = and () notations for initialization (§6.3.5) are not universal. For example:

```
struct Y : X {
Xm;
Y(int a) : X(a), m=a { }; // syntax error:can’t use = for member initialization
};
X g(1); // initializ global var iable
void f(int a) {
X def(); // function returning an X (surpr ise!?)
X* p {nullptr};
X var = 2; // initializ local var iable
p = new X=4; // syntax error:can’t use = for new
X a[](1,2,3); // error :can’t use () for array initialization
vector<X> v(1,2,3,4); // error :can’t use () for list elements
}
```

The = and () notations for initialization are not uniform either, but fortunately the examples of that are obscure. If you insist on using = or () initialization, you have to remember where they are allowed and what they mean.

The usual overload resolution rules (§12.3) apply for constructors. For example:

```
struct S {
S(const char*);
S(double*);
};
S s1 {“Napier”}; // S::S(const char*)
S s2 {new double{1.0}}; // S::S(double*);
S s3 {nullptr}; // ambiguous: S::S(const char*) or S::S(double*)?
```

Note that the {}-initializer notation does not allow narrowing (§2.2.2). That is another reason to prefer the {} style over () or =.

# 17.3.2.1 Initialization by Constructors

Using the () notation, you can request to use a constructor in an initialization. That is, you can ensure that for a class, you will get initialization by constructor and not get the memberwise initialization or initializer-list initialization (§17.3.4) that the {} notation also offers. For example:

```
struct S1 {
int a,b; // no constructor
};
```