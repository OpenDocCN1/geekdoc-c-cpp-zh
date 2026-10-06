
# ISO/IEC 14882:2017(E)

## D.16.2 Class template wbuffer_convert

Class template wbuffer_convert looks like a wide stream buffer, but performs all I/O through an underlying byte stream that you specify when you construct it. Like class template wstring_convert, it lets you specify a conversion facet to perform the conversions, without affecting any states or locales.

```cpp
namespace std {
template <class Codec, class E = char, class Tr = char_traits<Elem>>
class wbuffer_convert : public basic_stream<Elem, Tr> {
public:
    using state_type = typename Codec::state_type;
    explicit wbuffer_convert(streambuf* bytebuf,
        Codec* pcvt = nullptr,
        state_type state = state_type());

    virtual ~wbuffer_convert();

    wbuffer_convert(const wbuffer_convert&) = delete;
    wbuffer_convert& operator=(const wbuffer_convert&) = delete;

    streambuf* rdbuf() const;
    streambuf* rdbuf(streambuf* bytebuf);

    state_type state() const;

private:
    streambuf* bufptr; // exposition only
    Codec* pcvt; // exposition only
    state_type cvstate; // exposition only
};
```

- The class template describes a stream buffer that controls the transmission of elements of Elem, whose character traits are described by the class Tr, and by a stream buffer of type streambuf. Conversion between a sequence of Elem and multibyte sequences is performed by an object of class Codec, which shall meet the requirements of the standard-conversion facet codecvt<Elem, char, mstate_t>.

- An object of this class template stores:
    - bufptr — a pointer to its underlying byte stream buffer
    - pcvt — a pointer to the allocated conversion object (which is freed when the wbuffer_convert object is destroyed)
    - cvstate — a conversion state object

```cpp
state_type state() const;
```
Returns: cvstate.

```cpp
streambuf* rdbuf() const;
```
Returns: bufptr.

```cpp
streambuf* rdbuf(streambuf* bytebuf);
```
Effects: Stores bytebuf in bufptr.
Returns: The previous value of bufptr.

```cpp
using state_type = typename Codecvt::state_type;
The type shall be a synonym for Codecvt::state_type.
explicit wbuffer_convert(
    streambuf* bytebuf = nullptr,
    Codecvt* pcvt = new Codecvt,
    state_type state = state_type());
```
Requires: pcvt != nullptr.
Effects: The constructor constructs a stream buffer object, initializes bufptr to bytebuf, initializes pcvt to pcvt, and initializes cvstate to state.

```cpp
virtual ~wbuffer_convert();
Effects: The destructor shall delete pcvt.
```

## Bibliography

The following documents are cited informatively in this document.

- ISO/IEC 10967-1:2012, Information technology — Language independent arithmetic — Part 1: Integer and floating point arithmetic

The arithmetic specification described in ISO/IEC 10967-1:2012 is called LIA-1 in this document.

Bibliography ©ISO/IEC 2017 – All rights reserved

## Cross references

This index lists each section and the corresponding section number and page number, in alphabetical order by label.

| label | page |
| :--- | :--- |
| accumulate (29.8.2) | 1126 |
| adjacent.difference (29.8.11) | 1134 |
| adjustfield.manip (30.5.6) | 1174 |
| alg.adj.find (28.5.8) | 1012 |
| alg.all_of (28.5.3) | 1009 |
| alg.any_of (28.5.2) | 1009 |
| alg.binary.search (28.7.3) | 1031 |
| alg.c.library (28.8) | 1046 |
| alg.clamp (28.7.9) | 1044 |
| alg.copy (28.6.1) | 1017 |
| alg.count (28.5.9) | 1013 |
| alg.equal (28.5.1) | 1014 |
| alg.fill (28.6.6) | 1022 |
| alg.find (28.5.5) | 1011 |
| alg.find.end (28.5.6) | 1011 |
| alg.find.first.of (28.5.7) | 1012 |
| alg.foreach (28.7.3) | 1040 |
| alg.generate (28.6.7) | 1022 |
| alg.heap.operations (28.7.3) | 1035 |
| alg.is_permutation (28.5.12) | 1015 |
| alg.lex.comparison (28.7.10) | 1045 |
| alg.merge (28.7.5) | 1035 |
| alg.min.max (28.7.2) | 1032 |
| alg.modifying.operations (28.6) | 1017 |
| alg.move (28.6.2) | 1018 |
| alg.none_of (28.5.3) | 1009 |
| alg.nonmodifying (28.7) | 1025 |
| alg.nth.element (28.7.3) | 1031 |
| alg.partitions (28.7.4) | 1033 |
| alg.permutation.generators (28.7.11) | 1045 |
| alg.random.search (28.6.12) | 1026 |
| alg.random.shuffle (28.6.13) | 1027 |
| alg.remove (28.6.8) | 1023 |
| alg.replace (28.6.5) | 1021 |
| alg.reverse (28.6.11) | 1025 |
| alg.rotate (28.6.11) | 1025 |
| alg.search (28.5.13) | 1016 |
| alg.set.operations (28.7.6) | 1036 |
| alg.sort (28.7.1) | 1028 |
| alg.sorting (28.7) | 1027 |
| alg.swap (28.6.3) | 1019 |
| alg.transform (28.6.4) | 1020 |
| alg.unique (28.6.9) | 1024 |
| alg.parallel.table (20.5.5.7) | 473 |
| alg.parallel.user (28.2) | 1006 |
| alg.syn (28.2) | 986 |
| alg.general (28.1) | 986 |
| alg.parallel (28.4) | 1006 |
| alg.parallel.defins (28.4.1) | 1006 |
| alg.parallel.exceptions (28.4.4) | 1008 |
| alg.parallel.except (28.4.3) | 647 |
| alg.parallel.overloads (28.4.5) | 1009 |
| alg.parallel.requirements (28.3.5) | 1065 |
| alloc.error (21.6.3) | 998 |
| alloc.adaptor (23.13.4) | 645 |
| alloc.adaptor.constructor (23.13.3) | 648 |
| alloc.adaptor.members (23.13.4) | 648 |
| alloc.adaptor.syn (23.13.5) | 645 |
| alg.adaptor.types (23.13.2) | 647 |
| alloc.globals (23.10.9) | 1064 |
| alloc.members (23.10.9) | 1064 |
| alloc.requirements (20.5.3.5) | 461 |
| alloc.requirements.completeness (20.5.3.1) | 461 |
| alloc.tag (23.10.6) | 600 |
| alloc.traits (23.10.8) | 601 |
| alloc.traits.types (23.10.8) | 602 |
| alloc.members (23.10.8) | 602 |
| alloc.uses (23.10.7) | 600 |
| alloc.uses.construction (23.10.7) | 601 |
| alloc.uses.trait (23.10.7) | 600 |
| any (28.5) | 580 |
| any.assign (23.8.2) | 583 |
| any.bad_any (23.8.2) | 581 |
| any.class (23.8.3) | 581 |
| any.cons (23.8.3) | 583 |
| any.modifiers (23.8.3) | 583 |
| any.observers (23.8.4) | 584 |
| any.synop (23.8.1) | 580 |
| arithmetic.operations (23.14.6) | 656 |
| arithmetic.operations.divide (23.14.6) | 657 |
| arithmetic.operations.minus (23.14.6.2) | 657 |
| arithmetic.operations.modulus (23.14.6.5) | 658 |
| arithmetic.operations.multipl (23.14.6.3) | 657 |
| arithmetic.operations.negate (23.14.6.6) | 658 |
| arithmetic.operations.plus (23.14.6.1) | 656 |
| array (23.6.7.1) | 897 |
| array.copy (26.3.7.2) | 869 |
| array.data (26.3.7.5) | 869 |
| array.fill (26.3.7.6) | 869 |
| array.overview (26.3.7.1) | 869 |
| array.size (26.3.7.4) | 869 |
| array.special (26.3.7) | 869 |
| array.swap (26.3.7.7) | 869 |
| array.syn (26.3.7.5) | 869 |
| array.zero (26.3.7) | 870 |
| as (21.6) | 998 |
| assert (21.6) | 998 |
| begin (21.6) | 998 |
| cast (21.6) | 998 |
| container (21.6) | 998 |
| copy (21.6) | 998 |
| dere (21.6) | 998 |
| end (21.6) | 998 |
| element (21.6) | 998 |
| exception (21.6) | 998 |
| exception (21.6) | 998 |
| except (21.6) | 998 |
| flag (21.6) | 998 |
| find (21.6) | 998 |
| find (21.6) | 998 |
| for (21.6) | 998 |
| for (21.6) | 998 |
| get (21.6) | 998 |
| get (21.6) | 998 |
| in (21.6) | 998 |
| in (21.6) | 998 |
| iterator (21.6) | 998 |
| it (21.6) | 998 |
| less (21.6) | 998 |
| less (21.6) | 998 |
| move (21.6) | 998 |
| move (21.6) | 998 |
| move (21.6) | 998 |
| next (21.6) | 998 |
| next (21.6) | 998 |
| next (21.6) | 998 |
| not (21.6) | 998 |
| prev (21.6) | 998 |
| prev (21.6) | 998 |
| push (21.6) | 998 |
| push (21.6) | 998 |
| ref (21.6) | 998 |
| ref (21.6) | 998 |
| size (21.6) | 998 |
| size (21.6) | 998 |
| size (21.6) | 998 |
| size (21.6) | 998 |
| sort (21.6) | 998 |
| sort (21.6) | 998 |
| swap (21.6) | 998 |
| swap (21.6) | 998 |
| swap (21.6) | 998 |
| swap (21.6) | 998 |
| transform (21.6) | 998 |
| transform (21.6) | 998 |
| unique (21.6) | 998 |
| unique (21.6) | 998 |
| unique (21.6) | 998 |
