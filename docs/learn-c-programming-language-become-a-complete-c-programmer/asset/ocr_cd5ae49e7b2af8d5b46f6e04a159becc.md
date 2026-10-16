The member initializer list starts with a colon, and the individual member initializers are separated by commas.

# Section 17.4.1 Member Initialization 501

The members’ constructors are called before the body of the containing class’s own constructor is executed (§17.2.3). The constructors are called in the order in which the members are declared in the class rather than the order in which the members appear in the initializer list. To avoid confusion, it is best to specify the initializers in the member declaration order. Hope for a compiler warning if you don’t get the order right. The member destructors are called in the reverse order of construction after the body of the class’s own destructor has been executed.

If a member constructor needs no arguments, the member need not be mentioned in the member initializer list. For example:

```
Club::Club(const string& n, Date fd)
: name{n}, founded{fd}
{
//...
}
```

This constructor is equivalent to the previous version. In each case, Club::officers and Club::members are initialized to a vector with no elements.

It is usually a good idea to be explicit about initializing members. Note that an “implicitly initialized” member of a built-in type is left uninitialized (§17.3.1).

A constructor can initialize members and bases of its class, but not members or bases of its members or bases. For example:

```
struct B { B(int); /*...*/};
struct BB : B { /*...*/ };
struct BBB : BB {

BBB(int i) : B(i) {}; // error : trying to initialize base’s base
//...
};
```

# 17.4.1.1 Member Initialization and Assignment

Member initializers are essential for types for which the meaning of initialization differs from that of assignment. For example:

```
class X {
const int i;
Club cl;
Club& rc;
//...
X(int ii, const string& n, Date d, Club& c) : i{ii}, cl{n,d}, rc{c} { }
};
```

A reference member or a const member must be initialized (§7.5, §7.7, §17.3.3).

However, for most types the programmer has a choice between using an initializer and