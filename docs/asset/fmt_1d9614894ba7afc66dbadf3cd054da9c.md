
For `String<C>`, first consider the operations actually performed on the parameter `C` by the implementation of `String` (§19.3). That will be the minimal set of requirements for that implementation of `String`:

- [1] `C`s are copied by copy assignment and copy initialization.

- [2] `String` compares `C`s using `==` and `!=`.

- [3] `String` makes arrays of `C`s (that implies default construction of `C`s).

- [4] `String` takes the address of `C`s.

- [5] `C`s are destroyed when a `String` is destroyed.

- [6] `String` has `>>` and `<<` operators that somehow must read and write `C`s.

Requirements [4] and [5] are technical requirements that we usually assume for all data types, and I will not discuss types that fail to meet them; such types are almost all overly clever artifacts. The first requirement – that values can be copied – is not true for a few important types, such as `std::unique_ptr`, that represent real resources (§5.2.1, §34.3.1). However, it is true for almost all “ordinary types,” so we require it. The ability to invoke a copy operation goes together with the semantic requirement that a copy really is a copy of the original, that is, that – except for taking the address – the two copies behave identically. Therefore, the ability to copy usually (as for our `String`) goes together with the requirement to provide `==` with the usual semantics.

By requiring assignment, we imply that a `const` type cannot be used as a template argument. For example, `String<const char>` is not guaranteed to work. That’s fine in this case, as in most cases. Having assignment means that an algorithm can use temporary variables of its argument type, create containers of objects of an argument type, etc. It does not imply that we cannot use `const` to specify interfaces. For example:

```
template<typename T>
bool operator==(const String<T>& s1, const String<T>& s2)
{
if (s1.size()!=s2.size()) return false;
for (auto i = 0; i!=s1.size(); ++i)
if (s1[i]!=s2[i]) return false;
return true;
}
```

For `String<X>` we require that objects of type `X` can be copied. Independently, through the `const` in its argument types, `operator==( )` promises not to write to the `X` elements.

Should we require a move for an element type `C`? After all, we provide move operations for `String<C>`. We could, but it’s not essential: what we do with a `C` can be handled by copying, and if some copy is implicitly turned into a move (e.g., when we return a `C`), so much the better. In particular, potentially important examples, such as `String<String<char>>`, will work fine (correctly and efficiently) without adding move operations to the requirements.

So far, so good, but the last requirement (that we can read and write `C`s using `>>` and `<<`) seems excessive. Do we really read and write every kind of string? Maybe it would be better to say that if we read and write a `String<X>`, then `X` must provide `>>` and `<<`? That is, instead of placing a requirement on `C` for the whole `String`, we require it (only) for `String`s that we actually read and write.

This is an important and fundamental design choice: we can place a requirement on class template arguments (so that they apply to all class members) or just to template arguments on individual class function members. The latter is more flexible, but also more verbose (we have to express the requirement for each function that needs it) and harder for a programmer to remember.

Looking at the list of requirements so far, I note the absence of a couple of operations that are common for “ordinary characters” in “ordinary strings”:

- [1] No ordering (e.g., `<`)

- [2] No conversion to an integer value

After this initial analysis we can consider which “well-known concepts” (§24.3.2) our lists of requirements relate to. The central concept for “ordinary types” is `regular`. A `regular` type is a type that

- you can copy (using assignment or initialization) with the proper copy semantics (§17.5.1.3),

- you can default construct,

- doesn’t have problems with various minor technical requirements (such as taking the address of a variable),

- you can compare for equality (using `==` and `!=`).

That seems an excellent choice for our `String` template arguments. I considered leaving out the equality comparisons but decided that copying without equality is rarely useful. Typically, `Regular` is the safe bet, and thinking about the meaning of `==` can help avoid errors in the definition of copying. All the built-in types are regular.

But does it make sense to leave out ordering (`<`) for `String`? Consider how we use strings. The desired use of a template (such as `String`) should determine its requirements on its arguments. We do compare strings extensively, and in addition we use comparisons indirectly when we sort sequences of strings, we put strings into sets, etc. Also, the standard-library `string` does provide `<`. It is usually a good idea to look to the standard for inspiration. So, we require not just `Regular` for our `String`, but also ordering. That’s the concept `Ordered`.

Interestingly, there has been quite some debate on whether `Regular` should require `<` or not. It seems that most types related to numbers have a natural order. For example, characters are encoded in bit patterns that can be interpreted as integers, and any sequence of values can be lexicographically ordered. However, many types do not have a natural order (e.g., complex numbers and images) even though we could define one. Other types have several natural orderings, but no unique best ordering (e.g., records may be ordered by name or by address). Finally, some (reasonable) types simply don’t have an order. For example, consider:

```
enum class rsp { rock, scissors, paper };
```

The rock-scissors-and-paper game critically depends on

- `scissors<rock`,

- `rock<paper`, and

- `paper<scissors`.

However, our `String` is not supposed to take an arbitrary type as its character type; it is supposed to take a type that supports string operations (such as comparisons, sorting, and I/O), so I decided to require ordering.

Adding a default constructor and the `==` and `<` operator, to our requirements for `String`’s template argument allows us to provide several useful operations for `String`. In fact, the more we require of a template argument type, the easier the various tasks become for the template implementer and the more services the template can offer to its users. On the other hand, it is important not to load down a template with requirements that are only used rarely and by specific operations: each requirement places a burden on the implementer of argument types and limits the set of types that can be used as arguments. So, for `String<X>` we require:

- `Ordered<X>`

- `>>` and `<<` for `X` (only) if we use `String<X>`’s `>>` and `<<`

- Convertibility to an integer (only) if we define and use a conversion operation from `X`

So far, we have expressed our requirement of a character type for `String` in terms of syntactic properties, such as `X` must provide copy operations, `==`, and `<`. In addition, we must require that these operations have the right semantics; for example, a copy operation makes a copy, `==` (equality) compares for equality, and `<` (less than) provides ordering. Often, this semantics involves relations among the operations. For example, for the standard library, we have (§31.2.2.1):

- The result of a copy compares equal to anything the original compares equal to (`a==b` implies `T{a}==T{b}`) and the copy is independent of its source (§17.5.1.3).

- A less-than comparison (e.g., `<`) provides a strict weak order (§31.2.2.1).

The semantics are defined in English text or (better still) mathematics, but unfortunately we have no way of expressing semantic requirements in C++ itself (but see §24.4.1). For the standard library, you can find the semantic requirements written in formalized English in the ISO standard.
