The members of a class are private by default. That is, if the word private was missing in our example before declaring the code, the code would be private again. Although unnecessary, my preference is to add it, make clear the intention to declare variables as private. So we see that a class only allows the representation of a logical entity by encapsulating data (data encapsulation), and it also provides the ability to specify which data will be accessible from the external environment and to be hidden from direct access. As we'll see data hiding, it is very important to ensure the integrity of the object. By setting the users of the class, as programmers who use it in their programs. For example, in the following program, assume that you wrote the Test class and give it to another programmer who uses it to create Test objects. Find the errors:

```
#include <iostream> // Example 17.2
```

```
class Test
{
  private: /* Since the members of a class are private by default, we can omit
  the word private. */
    int a;
    void f1();
  protected:
    int b;
    void f2();
  public:
    int c;
    void f3();
};
```

```
void Test::f1()
{
    std::cout << a << ' << ' << b << ' << ' << c << ' << '\\n';
}
```

```
void Test::f2()
{
    a = 100;
}
```

```
void Test::f3()
{
    f1();
}
```

```
int main()
{
    Test t;

    t.a = 1;
    t.b = 2;
    t.c = 3;

    t.f1();
    t.f2();
    t.f3();
    return 0;
}
```