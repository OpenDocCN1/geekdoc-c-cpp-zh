Remember that we left the `istream` to deal with the usual whitespace characters (e.g., newline and space) in the usual way, so we don't need to do anything special about those.

This leaves one mysterious function:

```
```cpp
Punct_stream::operator bool()
{
    return !(source.fail() || source.bad()) && buffer.good();
}
```
```

The conventional use of an `istream` is to test the result of `>>`. For example:

```
```cpp
while (ps>>s) { /* ... */ }
```
```

That means that we need a way of looking at the result of `ps>>s` as a Boolean value. The result of `ps>>s` is a `Punct_stream`, so we need a way of implicitly turning a `Punct_stream` into a `bool`. That's what `Punct_stream`'s `operator bool()` does. A member function called `operator bool()` defines a conversion to `bool`. In particular, it returns `true` if the operation on the `Punct_stream` succeeded.

Now we can write our program:

```
```cpp
int main()
{
    // given text input, produce a sorted list of all words in that text
    // ignore punctuation and case differences
    // eliminate duplicates from the output
    Punct_stream ps {cin};
    ps.whitespace("";,,?!()}<>@&$#%|^*\~");    // Note `"` means `"` in string
    ps.case_sensitive(false);

    cout << "please enter words\n";
    vector<string> vs;
    for (string word; ps>>word; )
        vs.push_back(word);          // read words

    sort(vs.begin(),vs.end());       // sort in lexicographical order
    for (int i=0; i<vs.size(0); ++i)    // write dictionary
        if (i==0 || vs[i]!=vs[i-1]) cout << vs[i] << "\n";
}
```
```

This will produce a properly sorted list of words from input. The test

```
```cpp
if (i==0 || vs[i]!=vs[i-1])
```
```