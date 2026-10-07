Next, the new fill() should look like this:

```
void fill(std::array<double, Seasons> & pa)  // changed
{
    using namespace std;
    for (int i = 0; i < Seasons; i++)
    {
        cout << "Enter " << Snames[i] << " expenses: ";
        cin >> pa[i];      // changed
    }
}
```

Note that (*pa)[i] gets changed to the simpler pa[i].

Finally, the only change to show() is to the function header:

```
void show(std::array<double, Seasons> & da)
```

+   6. a. This can be done by using a default value for the second argument:
```
double mass(double d, double v = 1.0);
```
It can also be done by using function overloading:
```
double mass(double d, double v);
double mass(double d);
```
b. You can’t use a default for the repeat value because you have to provide default values from right to left. You can use overloading:
```
void repeat(int times, const char * str);
void repeat(const char * str);
```
c. You can use function overloading:
```
int average(int a, int b);
double average(double x, double y);
```
d. You can’t do this because both versions would have the same signature.

```
7. template<class T>
T max(T t1, T t2)  // or T max(const T & t1, const T & t2)
{
    return t1 > t2? t1 : t2;
}
```

```
8. template<> box max(box b1, box b2)
{
    return b1.volume > b2.volume? b1 : b2;
}
```