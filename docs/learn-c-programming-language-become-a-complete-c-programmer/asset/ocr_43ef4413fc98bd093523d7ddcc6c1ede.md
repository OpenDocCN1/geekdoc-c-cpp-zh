better handled by placing the changing data in a separate object and accessing it indirectly.
If that technique is used, the stringwith-cache example becomes:

```
struct cache { bool valid; string rep;
};

class Date {
public:
// ...
string string_rep() const; // string representation
private:
cache *c; // initialize in constructor
void compute_cache_value() const; // fill what cache refers to
// ...
};

string Date::string_rep() const
{
if (!c->valid) {
compute_cache_value();
c->valid = true;
}
return c->rep;
}
```

The programming techniques that support a cache generalize to various forms of lazy evaluation. Note that **const** does not apply (transitively) to objects accessed through pointers or references.

The human reader may consider such an object as “a kind of subobject,” but the compiler does not
know such pointers or references to be any different from any others. That is, a member pointer
does not have any special semantics that distinguish it from other pointers.

# 16.2.10 Self-Reference

The state update functions **add_year()**, **add_month()**, and **add_day()** (§16.2.3) were defined not to return values. For such a set of related update functions, it is often useful to return a reference to the updated object so that the operations can be chained. For example, we would like to write:

```
void f(Date& d)
{
// ...
d.add_day(1).add_month(1).add_year(1);
// ...
}
```

to add a day, a month, and a year to **d**. To do this, each function must be declared to return