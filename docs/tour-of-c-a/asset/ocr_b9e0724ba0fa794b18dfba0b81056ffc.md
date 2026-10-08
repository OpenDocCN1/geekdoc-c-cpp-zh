```
int sum(optional<int> a, optional<int> b
{
    int res = 0;
    if (a) res+=*a;
    if (b) res+=*b;
    return res;
}
```

int x = sum(17,19);    // 36
int y = sum(17,{});   // 17
int z = sum({},{});      // 0