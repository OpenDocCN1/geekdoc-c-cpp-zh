From a user’s point of view, string_rep doesn’t change the state of its Date, so it clearly should be a const member function. On the other hand, the cache and cache_valid members must change occasionally for the design to make sense.

Such problems could be solved through brute force using a cast, for example, a const_cast (§11.5.2). However, there are also reasonably elegant solutions that do not involve messing with type rules.

# 16.2.9.3 mutable

We can define a member of a class to be mutable, meaning that it can be modified even in a const object:

```
class Date {
public:
// ...
string string_rep() const;
private:
mutable bool cache_valid;
mutable string cache;
void compute_cache_value() const;
// ...
};
// stringrepresentation
// fill (mutable) cache
```

Now we can define string_rep() in the obvious way:

```
string Date::string_rep() const
{
if (!cache_valid) {
compute_cache_value();
cache_valid = true;
}
return cache;
}
```

We can now use string_rep() for both const and nonconst objects. For example:

```
void f(Date d, const Date cd)
{
string s1 = d.string_rep();
string s2 = cd.string_rep(); // OK! // ...
}
```

# 16.2.9.4 Mutability through Indirection

Declaring a member mutable is most appropriate when only a small part of a representation of a small object is allowed to change. More complicated cases are often