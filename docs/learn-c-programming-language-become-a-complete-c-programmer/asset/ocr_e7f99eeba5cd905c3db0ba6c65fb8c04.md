```
int a;
validate(int x) { if (0<x && x<=max) a=x; else throw Bad_X(x); }
public:
X(int x) { validate(x); }
X() { validate(42); }
X(string s) { int x = to<int>(s); validate(x); } // §25.2.5.1
// ...
};
```

Verbosity hinders readability and repetition is error-prone. Both get in the way of maintainability. The alternative is to define one constructor in terms of another:

```
class X {
int a;
public:
X(int x) { if (0<x && x<=max) a=x; else throw Bad_X(x); }
X() :X{42} { }
X(string s) :X{to<int>(s)} { } // §25.2.5.1
// ...
};
```

That is, a member-style initializer using the class’s own name (its constructor name) calls another constructor as part of the construction. Such a constructor is called a delegating constructor (and occasionally a forwarding constructor).

You cannot both delegate and explicitly initialize a member. For example:

```
class X {
int a;
public:
X(int x) { if (0<x && x<=max) a=x; else throw Bad_X(x); }
X() :X{42}, a{56} { } // error
// ...
};
```

Delegating by calling another constructor in a constructor’s member and base initializer list is very different from explicitly calling a constructor in the body of a constructor. Consider:

```
class X {
int a;
public:
X(int x) { if (0<x && x<=max) a=x; else throw Bad_X(x); }
X() { X{42}; } // likely error
// ...
};
```

The X{42} simply creates a new unnamed object (a temporary) and does nothing with it. Such use is more often than not a bug. Hope for a compiler warning.

An object is not considered constructed until its constructor completes (§6.4.2). When