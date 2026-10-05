Consider this example:

```
int func(int a, int b)
{
    return a + b;
}
int func(int a, int b) noexcept
{
    return a + b;
}
int main()
{
    func(1, 3);
    return 0;
}
// error: redefinition of 'int func(int, int)'
```