```
void test()
{
    string input = "aa as; asdf ++e~asd asdfg";
    regex pat {R"(\s+(\w+))"};\n    for (sregex_iterator p(input.begin(),input.end(),pat); p!=sregex_iterator{}; ++p)
        cout << (*p)[1] << '\n';
}
```