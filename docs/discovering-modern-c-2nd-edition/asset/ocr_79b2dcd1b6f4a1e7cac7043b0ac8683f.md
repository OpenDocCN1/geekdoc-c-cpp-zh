```
assert(size(v) <= 5);
int i = 0;
switch (size(v)) {
    case 5: v[i] = w[i] + x[i]; ++i;    // keep going
    case 4: v[i] = w[i] + x[i]; ++i;    // keep going
    case 3: v[i] = w[i] + x[i]; ++i;    // keep going
    case 2: v[i] = w[i] + x[i]; ++i;    // keep going
    case 1: v[i] = w[i] + x[i];         // keep going
    case 0: ;
}
```