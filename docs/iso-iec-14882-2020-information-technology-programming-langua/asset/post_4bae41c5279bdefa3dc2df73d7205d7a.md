
## 16.3.3.2 Exposition-only functions [expos.only.func]

1 Several function templates defined in Clause 17 through Clause 32 and Annex D are only defined for the purpose of exposition. The declaration of such a function is followed by a comment ending in exposition only.

2 The following are defined for exposition only to aid in the specification of the library:

```
template<class T> constexpr decay_t<T> decay-copy(T&& v)
    noexcept(is_nothrow_convertible_v<T, decay_t<T>>)
{ return std::forward<T>(v); } // exposition only
```

```
constexpr auto synth-three-way =
[]<class T, class U>(const T& t, const U& u)
requires {
    { t < u } -> boolean-testable;
    { u < t } -> boolean-testable;
}
{
    if constexpr (three_way_comparable_with<T, U>) {
        return t <=> u;
    } else {
        if (t < u) return weak_ordering::less;
        if (u < t) return weak_ordering::greater;
        return weak_ordering::equivalent;
    }
};
```

```
template<class T, class U=T>
using synth-three-way-result = decltype(synth-three-way(declval<T&>(), declval<U&>()));
```

## 16.3.3.3 Type descriptions [type.descriptions]

### 16.3.3.3.1 General [type.descriptions.general]

1 The Requirements subclauses may describe names that are used to specify constraints on template arguments.161 These names are used in library Clauses to describe the types that may be supplied as arguments by a C++ program when instantiating template components from the library.

2 Certain types defined in Clause 29 are used to describe implementation-defined types. They are based on other types, but with added constraints.

### 16.3.3.3.2 Exposition-only types [expos.only.types]

1 Several types defined in Clause 17 through Clause 32 and Annex D are defined for the purpose of exposition. The declaration of such a type is followed by a comment ending in exposition only.

> [Example 1:
```
namespace std {
    extern "C" using some-handler = int(int, void*, double); // exposition only
}
```
The type placeholder some-handler can now be used to specify a function that takes a callback parameter with C language linkage. — end example]

### 16.3.3.3.3 Enumerated types [enumerated.types]

1 Several types defined in Clause 29 are enumerated types. Each enumerated type may be implemented as an enumeration or as a synonym for an enumeration.162

2 The enumerated type enumerated can be written:

```
enum enumerated { V0, V1, V2, V3, ... };
```

## 16.3.3.3.5 Character sequences [character.seq]

### 16.3.3.3.5.1 General [character.seq.general]

1 The C standard library makes widespread use of characters and character sequences that follow a few uniform conventions:

- (1.1) — A *letter* is any of the 26 lowercase or 26 uppercase letters in the basic execution character set.
- (1.2) — The *decimal-point character* is the (single-byte) character used by functions that convert between a (single-byte) character sequence and a value of one of the floating-point types. It is used in the character sequence to denote the beginning of a fractional part. It is represented in Clause 17 through Clause 32 and Annex D by a period, ‘.’ , which is also its value in the "C" locale, but may change during program execution by a call to setlocale(int, const char*)¹⁶³ or by a change to a locale object, as described in 28.3 and Clause 29.
- (1.3) — A *character sequence* is an array object (9.3.4.5) *A* that can be declared as *T A[N]*, where *T* is any of the types char, unsigned char, or signed char (6.8.2), optionally qualified by any combination of const or volatile. The initial elements of the array have defined contents up to and including an element determined by some predicate. A character sequence can be designated by a pointer value *S* that points to its first element.

### 16.3.3.3.5.2 Byte strings [byte.strings]

1 A *null-terminated byte string*, or NTBS, is a character sequence whose highest-addressed element with defined content has the value zero (the *terminating null character*); no other element in the sequence has the value zero.¹⁶⁴

2 The *length of an NTBS* is the number of elements that precede the terminating null character. An *empty NTBS* has a length of zero.

3 The *value of an NTBS* is the sequence of values of the elements up to and including the terminating null character.

4 A *static NTBS* is an NTBS with static storage duration.¹⁶⁵

### 16.3.3.3.5.3 Multibyte strings [multibyte.strings]

1 A *null-terminated multibyte string*, or NTMBS, is an NTBS that constitutes a sequence of valid multibyte characters, beginning and ending in the initial shift state.¹⁶⁶

2 A *static NTMBS* is an NTMBS with static storage duration.

### 16.3.3.3.6 Customization Point Object types [customization.point.object]

1 A *customization point object* is a function object (20.14) with a literal class type that interacts with program-defined types while enforcing semantic requirements on that interaction.

2 The type of a customization point object, ignoring cv-qualifiers, shall model semiregular (18.6).

3 All instances of a specific customization point object type shall be equal (18.2).

4 The type T of a customization point object shall model invocable<const T&, Args...> (18.7.2) when the types in Args... meet the requirements specified in that customization point object’s definition. When the types of Args... do not meet the customization point object’s requirements, T shall not have a function call operator that participates in overload resolution.

5 Each customization point object type constrains its return type to model a particular concept.

6 [Note 1: Many of the customization point objects in the library evaluate function call expressions with an unqualified name which results in a call to a program-defined function found by argument dependent name lookup (6.5.3). To preclude such an expression resulting in a call to unconstrained functions with the same name in namespace std, customization point objects specify that lookup for these expressions is performed in a context that includes deleted overloads matching the signatures of overloads defined in namespace std. When the deleted overloads are viable, program-defined overloads need be more specialized (13.7.7.3) or more constrained (13.5.5) to be used by a customization point object. — end note]

163) declared in <clocale> (28.5.1).

164) Many of the objects manipulated by function signatures declared in <cstring> (21.5.3) are character sequences or NTBSs. The size of some of these character sequences is limited by a length value, maintained separately from the character sequence.

165) A string-literal, such as "abc", is a static NTBS.

166) An NTBS that contains characters only from the basic execution character set is also an NTMBS. Each multibyte character then consists of a single byte.

## 16.3.3.4 Functions within classes [functions.within.classes]

1 For the sake of exposition, Clause 17 through Clause 32 and Annex D do not describe copy/move constructors, assignment operators, or (non-virtual) destructors with the same apparent semantics as those that can be generated by default (11.4.5.3, 11.4.6, 11.4.7). It is unspecified whether the implementation provides explicit definitions for such member function signatures, or for virtual destructors that can be generated by default.

## 16.3.3.5 Private members [objects.within.classes]

1 Clause 17 through Clause 32 and Annex D do not specify the representation of classes, and intentionally omit specification of class members (11.4). An implementation may define static or non-static class members, or both, as needed to implement the semantics of the member functions specified in Clause 17 through Clause 32 and Annex D.

2 For the sake of exposition, some subclauses provide representative declarations, and semantic requirements, for private members of classes that meet the external specifications of the classes. The declarations for such members are followed by a comment that ends with exposition only, as in:

```
streambuf* sb;    // exposition only
```

3 An implementation may use any technique that provides equivalent observable behavior.

## 16.4 Library-wide requirements [requirements]

### 16.4.1 General [requirements.general]

1 Subclause 16.4 specifies requirements that apply to the entire C++ standard library. Clause 17 through Clause 32 and Annex D specify the requirements of individual entities within the library.

2 Requirements specified in terms of interactions between threads do not apply to programs having only a single thread of execution.

3 16.4.2 describes the library's contents and organization, 16.4.3 describes how well-formed C++ programs gain access to library entities, 16.4.4 describes constraints on types and functions used with the C++ standard library, 16.4.5 describes constraints on well-formed C++ programs, and 16.4.6 describes constraints on conforming implementations.

## 16.4.2 Library contents and organization [organization]

### 16.4.2.1 General [organization.general]

1 16.4.2.2 describes the entities and macros defined in the C++ standard library. 16.4.2.3 lists the standard library headers and some constraints on those headers. 16.4.2.4 lists requirements for a freestanding implementation of the C++ standard library.

### 16.4.2.2 Library contents [contents]

1 The C++ standard library provides definitions for the entities and macros described in the synopses of the C++ standard library headers (16.4.2.3), unless otherwise specified.

2 All library entities except operator new and operator delete are defined within the namespace std or namespaces nested within namespace std.167 It is unspecified whether names declared in a specific namespace are declared directly in that namespace or in an inline namespace inside that namespace.168

3 Whenever a name x defined in the standard library is mentioned, the name x is assumed to be fully qualified as ::std::x, unless explicitly described otherwise. For example, if the Effects: element for library function F is described as calling library function G, the function ::std::G is meant.

### 16.4.2.3 Headers [headers]

1 Each element of the C++ standard library is declared or defined (as appropriate) in a header.169

2 The C++ standard library provides the C++ library headers, shown in Table 21.

3 The facilities of the C standard library are provided in the additional headers shown in Table 22.170
