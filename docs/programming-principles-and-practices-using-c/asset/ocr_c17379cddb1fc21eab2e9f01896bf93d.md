```
```cpp
double primary()
{
    Token t = get_token();
    switch (t.kind) {
    case '(':   // handle '(' expression ')'
        {   double d = expression();
            t = get_token();
            if (t.kind != ')') error("')' expected");
            return d;
        }
    case '8':   // we use '8' to represent a number
        return t.value;   // return the number's value
    default:
        error("primary expected");
    }
}
```
```

Basically there is nothing new compared to expression() and term(). We use the same language primitives, the same way of dealing with Token, and the same programming techniques.

# ## 6.6 Trying the first version

To run these calculator functions, we need to implement get_token() and provide a main(). The main() is trivial: we just keep calling expression() and printing out its result:

```
```cpp
int main()
try {
    while (cin)
        cout << expression() << "\n";
    keep_window_open();
}
catch (exception& e) {
    cerr << e.what() << "\n";
    keep_window_open ();
    return 1;
}
catch (...) {
    cerr << "exception\n";
    keep_window_open ();
    return 2;
}
```
```