```
void user(forward_range auto& r)
{
    auto odd = [](int x) { return x % 2; };

    for (int x : r | views::filter(odd) | views::take(3))
        cout << x << ' ';
}
```