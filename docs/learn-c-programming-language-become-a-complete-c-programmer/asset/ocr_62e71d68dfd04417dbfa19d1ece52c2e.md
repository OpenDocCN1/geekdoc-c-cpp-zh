As long as we manage to pick distinct namespace names, such as **Graph_lib** and **Text_lib** (§14.4.2), we can now compile the two sets of declarations together without name clashes.

A namespace should express some logical structure: the declarations within a namespace should together provide facilities that unite them in the eyes of their users and reflect a common set of design decisions. They should be seen as a logical unit, for example, “the graphics library” or “the text manipulation library,” similar to the way we consider the members of a class. In fact, the entities declared in a namespace are referred to as the members of the namespace.

A namespace is a (named) scope. You can access members defined earlier in a namespace from later declarations, but you cannot (without special effort) refer to members from outside the namespace. For example:

```
class Glyph { /* ... */ };
class Line { /* ... */ };
```

```
namespace Text_lib {
class Glyph { /* ... */ };
class Word { /* ... */ }; // sequence of Glyphs
class Line { /* ... */ }; // sequence of Words
class Text { /* ... */ }; // sequence of Lines

File* open(const char*); // open text file
Word operator+(const Line&, const Line&); }

Glyph glyph(Line& ln, int i); // ln[i]
```

Here, the **Word** and **Line** in the declaration of **Text_lib::Line**. That local name lookup is not affected by the global **Line**. Conversely, the **Glyph** and **Line** in the declaration of the global **glyph()** refer to the global **::Glyph** and **::Line**. That (nonlocal) lookup is not affected by **Text_lib**’s **Glyph** and **Line**.

To refer to members of a namespace, we can use its fully qualified name. For example, if we want a **glyph()** that uses definitions from **Text_lib**, we can write:

```
Text_lib::Glyph glyph(Text_lib::Line& ln, int i); // ln[i]
```

Other ways of referring to members from outside their namespace are **using**-declarations (§14.2.2), **using**-directives (§14.2.3), and argument-dependent lookup (§14.2.4).

```
// concatenate Text_lib::operator+() refer to Text_lib::Word and
```

# 14.2.1 Explicit Qualification

A member can be declared within a namespace definition and defined later using the *namespacename :: member-name* notation. Members of a namespace must be introduced using this notation:

```
namespace namespace-name {
// declaration and definitions
}
```

For example: