# Functions 293

```
int main()
{
    test();
    a += 50;
    std::cout << a << ' ';
    last(200);
    return 0;
}
```

```
void test()
{
    int a = 300;
    if(a == 300)
{
        int a = 500;
        a++;
        std::cout << a << ' ';
    }
    a += 20;
    std::cout << a << ' ';
}
```

```
void last(int a)
{
    a++;
    std::cout << a << '\n';
}
```

The four variables are named different. Let's apply the scope rule. The tested in the if condition is one declared in test(), the statement a++ refers to the declared in the if block. Its scope is up to the end of the), and the next statement a=20 increases the value of the global which a of test(). Its scope is up to the end of the function. main() increases the value of the global which becomes 150. last() increases the local parameter a which becomes 201. As a result, the program outputs: 501 320 150 201. This program is just example to show you how the scope rule applies when using the same name; it is a bad programming approach. As you see, the code becomes harder to read, confusing, and error prone.
To access a global name we use the scope resolution operator ::. Since the global namespace has no name, nothing is added to the left of :: For example:

```
int a = 100;
void f()
{
    int a = 300;
    if(::a == 100) // Access the global variable.
{
}
```

The scope of names declared in a for statement is local, that is, it extends to its end. Thus, we use the same names in a function. For example:

```
void f()
{
    for(int i = 0; i < 5; i++)
{
        ...
    }
```