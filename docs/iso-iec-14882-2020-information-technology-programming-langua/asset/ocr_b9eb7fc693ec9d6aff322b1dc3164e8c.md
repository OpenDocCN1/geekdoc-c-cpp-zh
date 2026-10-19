```
int compare(const string_type& s) const;\nint compare(basic_string_view<value_type> s) const;\nint compare(const value_type* s) const;
```

Effects: Equivalent to: return compare(path(s));

# 29.11.6.5.9 Decomposition

```
path root_name() const;
```

Returns: root-name, if the pathname in the generic format includes root-name, otherwise path().

```
path root_directory() const;
```

Returns: root-directory, if the pathname in the generic format includes root-directory, otherwise path().

```
path root_path() const;
```

Returns: root_name() / root_directory().

```
path relative_path() const;
```

Returns: A path composed from the pathname in the generic format, if empty() is false, beginning with the first filename after root_path(). Otherwise, path().

```
path parent_path() const;
```

Returns: *this if has_relative_path() is false, otherwise a path whose generic format pathname is the longest prefix of the generic format pathname of *this that produces one fewer element in its iteration.

```
path filename() const;
```

Returns: relative_path().empty() ? path() : *--end().

```
[Example 1:\n    path("/foo/bar.txt").filename();      // yields "bar.txt"\n    path("/foo/bar").filename();          // yields "bar"\n    path("/foo/bar/").filename();         // yields ""\n    path("/").filename();                 // yields ""\n    path("//host").filename();            // yields ""\n    path(".").filename();                // yields "."\n    path("..").filename();               // yields ".."\n— end example]
```

```
path stem() const;
```

Returns: Let f be the generic format pathname of filename(). Returns a path whose pathname in the generic format is\n— f, if it contains no periods other than a leading period or consists solely of one or two periods;\n— otherwise, the prefix of f ending before its last period.

```
[Example 2:\n    std::cout << path("/foo/bar.txt").stem();       // outputs "bar"\n    path p = "foo.bar.baz.tar";\n    for (; !p.extension().empty(); p = p.stem())\n        std::cout << p.extension() << '\\n';\n        // outputs: .tar\n        //           .baz\n        //           .bar\n— end example]
```

```
path extension() const;
```

Returns: A path whose pathname in the generic format is the suffix of filename() not included in stem().

```
[Example 3:\n    path("/foo/bar.txt").extension();        // yields ".txt" and stem() is "bar"]
```