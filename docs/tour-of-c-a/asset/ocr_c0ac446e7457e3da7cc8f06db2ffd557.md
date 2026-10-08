```
void user(R2 r1, R2 r2)
{
    bool b4 = (r1==r2); // error: no non-default ==
    bool b5 = (r1<r2); // OK
}
```