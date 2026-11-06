**R10.12** What does the following program print?

```
~~~cpp
class B
{
public:
    void print(int n) const;
};

void B::print(int n) const
{
    cout << n << endl;
}

class D : public B
{
public:
    void print(int n) const;
};

void D::print(int n) const
{
    if (n <= 1) { B::print(n); }
    else if (n % 2 == 0) { print(n / 2); }
    else { print(3 * n + 1); }
}

int main()
{
    D d;
    d.print(3);
    return 0;
}
~~~
```

Determine the answer by hand, not by compiling and running the program.

**R10.13** Suppose the class D inherits from B. Which of the following assignments are legal?

```
~~~cpp
B b;
D d;
B* pb;
D* pd;
~~~
```

+   - **a.** `b = d;`
+   - **b.** `d = b;`
+   - **c.** `pd = pb;`
+   - **d.** `pb = pd;`
+   - **e.** `d = pd;`
+   - **f.** `b = *pd;`
+   - **g.** `*pd = *pb;`

**R10.14** Suppose the class Sub is derived from the class Sandwich. Which of the following assignments are legal?

```
~~~cpp
Sandwich* x = new Sandwich();
Sub* y = new Sub();
~~~
```

+   - **a.** `x = y;`
+   - **b.** `y = x;`
+   - **c.** `y = new Sandwich();`