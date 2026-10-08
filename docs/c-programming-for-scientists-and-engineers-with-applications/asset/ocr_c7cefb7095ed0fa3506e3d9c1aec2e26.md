```
int func1(int, float);
void func2(x, y, z)
func3(int a, float b, double c)
```

c. Which function or functions in the following code can call func1( ). Why? Which can call func2( )?

```
int func1(int, float);
int main()
{
    void func2(float, double);
    ......
    return 0;
}

void func2(float x, double y)
{
    ......
}

void func1(int a, float b)
{
    ......
}
```

d. Which function or functions in the following code can call func1( ) and func2( ). Why?

```
int main()
{
    void func2(float, double);
    ......
    return 0;
}

int func1(int, float);

void func2(float x, double y)
{
    ......
}
void func1(int a, float b)
{
    ......
}
```