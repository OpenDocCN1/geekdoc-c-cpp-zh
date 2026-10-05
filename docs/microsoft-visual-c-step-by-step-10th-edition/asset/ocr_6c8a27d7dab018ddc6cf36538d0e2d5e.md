```
struct Complex
{
    ...
    public static implicit implicit operator Complex(int from) => new Complex(from);
    ...
}
```