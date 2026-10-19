3  The dot filename is treated as a reference to the current directory. The dot-dot filename is treated as a reference to the parent directory. What the dot-dot filename refers to relative to *root-directory* is implementation-defined. Specific filenames may have special meanings for a particular operating system.

4  A *root-name* identifies the starting location for pathname resolution (29.11.6). If there are no operating system dependent *root-names*, at least one implementation-defined *root-name* is required.

> [*Note 2:* Many operating systems define a name beginning with two *directory-separator* characters as a *root-name* that identifies network or other resource locations. Some operating systems define a single letter followed by a colon as a drive specifier — a *root-name* identifying a specific device such as a disk drive. — *end note*]

5  If a *root-name* is otherwise ambiguous, the possibility with the longest sequence of characters is chosen.

> [*Note 3:* On a POSIX-like operating system, it is impossible to have a *root-name* and a *relative-path* without an intervening *root-directory* element. — *end note*]

6  *Normalization* of a generic format pathname means:

+   1. If the path is empty, stop.
+   2. Replace each slash character in the *root-name* with a *preferred-separator*.
+   3. Replace each *directory-separator* with a *preferred-separator*.

> [*Note 4:* The generic pathname grammar defines *directory-separator* as one or more slashes and *preferred-separators*. — *end note*]

+   4. Remove each dot filename and any immediately following *directory-separator*.
+   5. As long as any appear, remove a non-dot-dot filename immediately followed by a *directory-separator* and a dot-dot filename, along with any immediately following *directory-separator*.
+   6. If there is a *root-directory*, remove all dot-dot filenames and any *directory-separators* immediately following them.

> [*Note 5:* These dot-dot filenames attempt to refer to nonexistent parent directories. — *end note*]

+   7. If the last filename is dot-dot, remove any trailing *directory-separator*.
+   8. If the path is empty, add a dot.

The result of normalization is a path in *normal form*, which is said to be *normalized*.

# 29.11.6.3  Conversions

# 29.11.6.3.1  Argument format conversions

> 1  [*Note 1:* The format conversions described in this subclause are not applied on POSIX-based operating systems because on these systems:
> 
> (1.1) — The generic format is acceptable as a native path.
> 
> (1.2) — There is no need to distinguish between native format and generic format in function arguments.
> 
> (1.3) — Paths for regular files and paths for directories share the same syntax.
> 
> — *end note*]

2  Several functions are defined to accept *detected-format* arguments, which are character sequences. A detected-format argument represents a path using either a pathname in the generic format (29.11.6.2) or a pathname in the native format (29.11.6). Such an argument is taken to be in the generic format if and only if it matches the generic format and is not acceptable to the operating system as a native path.

> 3  [*Note 2:* Some operating systems have no unambiguous way to distinguish between native format and generic format arguments. This is by design as it simplifies use for operating systems that do not require disambiguation. An implementation for an operating system where disambiguation is required is permitted to distinguish between the formats. — *end note*]

4  Pathnames are converted as needed between the generic and native formats in an operating-system-dependent manner. Let G(n) and N(g) in a mathematical sense be the implementation’s functions that convert native-to-generic and generic-to-native formats respectively. If g=G(n) for some n, then G(N(g))=g; if n=N(g) for some g, then N(G(n))=n.

> [*Note 3:* Neither G nor N need be invertible. — *end note*]

5  If the native format requires paths for regular files to be formatted differently from paths for directories, the path shall be treated as a directory path if its last element is a *directory-separator*, otherwise it shall be treated as a path to a regular file.