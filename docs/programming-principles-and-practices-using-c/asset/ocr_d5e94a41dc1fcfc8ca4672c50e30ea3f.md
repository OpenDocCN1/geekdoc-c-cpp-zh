# **B.7.4 Output operations**

Output operations are found in `<ostream>` except for the ones writing out a string; those are found in `<string>`:

| Output operations |
| :---------------- | :----------------- |
| `out << x` | Write **x** to **out** according to **x**'s type. |
| `out.put(c)` | Write the character **c** to **out**. |
| `out.write(p,n)` | Write the characters **p[0]..p[n–1]** to **out**. |

Unless otherwise stated, an **ostream** operation returns a reference to its **ostream**, so that we can “chain” operations, for example, **cout << x<<y**;

# **B.7.5 Formatting**

The format of stream I/O is controlled by a combination of object type, stream state, locale information (see **`<locale>`**), and explicit operations. Chapters 10 and 11 explain much of this. Here, we just list the standard manipulators (operations modifying the state of a stream) because they provide the most straightforward way of modifying formatting.

Locales are beyond the scope of this book.

# **B.7.6 Standard manipulators**

The standard library provides manipulators corresponding to the various format states and state changes. The standard manipulators are defined in **`<ios>`**, **`<istream>`**, **`<ostream>`**, **`<iostream>`**, and **`<iomanip>`** (for manipulators that take arguments):

| I/O manipulators |
| :--------------- | :------------------------------------------------------- |
| `s<<boolalpha` | Use symbolic representation of **true** and **false** (input and output). |
| `s<<noblalpha` | `s.unsetf(ios_base::boolalpha)`. |
| `s<<showbase` | On output prefix **oct** by **0** and **hex** by **0x**. |
| `s<<noshowbase` | `s.unsetf(ios_base::showbase)`. |
| `s<<showpoint` | Always show the decimal point. |
| `s<<noshowpoint` | `s.unsetf(ios_base::showpoint)`. |
| `s<<showpos` | Show **+** for positive numbers. |