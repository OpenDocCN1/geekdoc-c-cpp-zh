```
for (string s; cin>>s);
print_directory(s);
}
```

Had I wanted to list subdirectories, I would have said recursive_directory_iterator(p). Had I wanted to print entries in lexicographical order, I would have copied the paths into a vector and sorted that before printing.
Class path offers many common and useful operations:

| Path Operations (partial) |
| p and p2 paths |
| value_type | Character used by the native encoding of the filesystem: char on POSIX, wchar_t on Windows |
| string_type | ::::basic_string<value_type> |
| const_iterator | A Const BidirectionalIterator with a value_type of path |
| iterator | Alias for const_iterator |
| p=p2 | Assign p2 to p |
| /=p2 | p and p2 concatenated using the file-name separator (by default /) |
| p+=p2 | p and p2 concatenated (no separator) |
| s=p.native() | A reference to the native format of p |
| s=p.string() | p in the native format of p as a string |
| s=p.generic_string(p) | in the generic format as a string |
| p2=p.filename() | The filename of p |
| p2=p.extension() | The file extension part of p |
| i=p.begin() | The beginning iterator of p's element sequence
| i=p.end() | The end iterator of p's element sequence
| p2=p1, p1=p2 | Equality and inequality for p and p2 |
| p2<p1, p1<p2, p2>p1 | Lexicographical comparisons |
| p2=p2 | |
| iss>>p, os<<p | Stream I/O to/from p |
| u8path(s) | A path from UTF-8 encoded source s |

```
{
if (is_directory(p)) {
    cout << p << \
```