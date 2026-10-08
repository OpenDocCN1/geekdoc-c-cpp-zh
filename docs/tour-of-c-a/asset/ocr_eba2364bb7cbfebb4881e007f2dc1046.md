```
bool is_identifier(const string& s)
{
    regex pat("[_[::alpha:]]\w*"); // underscore or letter
    // followed by zero or more underscores, letters, or digits
    return regex_match(s,pat);
}
```