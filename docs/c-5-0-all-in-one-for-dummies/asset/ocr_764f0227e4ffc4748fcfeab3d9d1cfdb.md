A distance of 2 billion inches is greater than the circumference of the Earth. In case 2 billion isn’t quite large enough for you, C# provides an integer type called `long` (short for `long int`) that can represent numbers almost as large as you can imagine. The only problem with a `long` is that it takes a larger train locker: A `long` consumes 8 bytes (64 bits) — twice as much as a garden-variety 4-byte (32-bit) `int`. C# provides several other integer variable types, as shown in Table 2-1.

| Type | Bytes | Range of Values | In Use |
|---|---:|---|---|
| `sbyte` | 1 | −128 to 127 | `sbyte sb = 12;` |
| `byte` | 1 | 0 to 255 | `byte b = 12;` |
| `short` | 2 | −32,768 to 32,767 | `short sh = 12345;` |
| `ushort` | 2 | 0 to 65,535 | `ushort ush = 62345;` |
| `int` | 4 | −2 billion to 2 billion | `int n = 1234567890;` |
| `uint` | 4 | 0 to 4 billion (exact values listed in the Cheat Sheet on this book’s Web site) | `uint un = 3234567890U` |
| `long` | 8 | −10²⁰ to 10²⁰ — “a whole lot” | `long l = 123456789012L` |
| `ulong` | 8 | 0 to 2 × 10²⁰ | `long ul = 123456789012UL` |

**Table 2-1 — Size and Range of C# Integer Types**

As I explain in the section “Declaring Numeric Constants,” later in this chapter, fixed values such as 1 also have a type. By default, a simple constant such as 1 is assumed to be an `int`. Constants other than an `int` must be marked with their variable type. For example, 123U is an unsigned integer, `uint`.

Most integer variables are called *signed*, which means they can represent negative values. Unsigned integers can represent only positive values, but you get twice the range in return. As you can see from Table 2-1, the names of most unsigned integer types start with a `u`, while the signed types generally don’t have a prefix.

![](bbox=[0.154, 0.836, 0.23, 0.903])

You don’t need any unsigned integer versions in this book.