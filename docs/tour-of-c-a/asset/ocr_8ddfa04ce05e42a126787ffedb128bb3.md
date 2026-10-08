```
void user(forward_range auto& r)
{
    int count = 0;
    for (int x : r) {
        if (x % 2) {
            cout << x << '"';
            if (++count == 3) return;
        }
    }
}
```