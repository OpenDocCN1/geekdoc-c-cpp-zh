```
constepr int p_rec(int i, int j, int k)
{
    return k == 0 ? g(i, j) : h(i, j, k-1, p_rec(i, j, k-1));
}
```