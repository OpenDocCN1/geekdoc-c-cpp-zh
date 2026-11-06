# ### 3.6 Keywords and reserved names in C++

C++'s keywords are a superset of C's keywords. Here is a list of all keywords of the language:

```
```
alignof compl explicit namespace return typeid
and concept export new short typename
and_eq const extern not signed union
asm const_cast false not_eq sizeof unsigned
auto constexpr float nullptr static using
axiom continue for operator static_cast virtual
bitand decltype friend or struct void
bitor default goto or_eq switch volatile
bool delete if private template wchar_t
break do import protected this while
case double inline public throw xor
catch dynamic_cast int register true xor_eq
char else long reinterpret_cast try
class enum mutable requires typedef
```
```

Notes:

+   - The `export` keyword is removed from the language under the C++11 standard, but remains a keyword, reserved for future use.
+   - The *operator keywords*: `and`, `and_eq`, `bitand`, `bitor`, `compl`, `not`, `not_eq`, `or`, `or_eq`, `xor` and `xor_eq` are symbolic alternatives for, respectively, `&&`, `&=`, `&`, `|`, `~`, `!`, `!=`, `||`, `|^`, `^` and `^=`.
+   - C++11 also recognizes the special identifiers `final` and `override`. These identifiers are special in the sense that they acquire special meanings when declaring classes or polymorphic functions. Section 14.4 provides further details.

Keywords can only be used for their intended purpose and cannot be used as names for other entities (e.g., variables, functions, class-names, etc.). In addition to keywords identifiers starting with an underscore and living in the *global namespace* (i.e., not using any explicit namespace or using the mere `::` namespace specification) or living in the *std namespace* are reserved identifiers in the sense that their use is a prerogative of the implementer.