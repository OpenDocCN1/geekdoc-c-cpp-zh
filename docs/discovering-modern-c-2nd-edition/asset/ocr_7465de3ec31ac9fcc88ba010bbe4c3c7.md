```
void print_some_string(string_view sv)
{
    cout << sv << '\n';
}

print_some_string("const char*");
print_some_string("string"s);
```