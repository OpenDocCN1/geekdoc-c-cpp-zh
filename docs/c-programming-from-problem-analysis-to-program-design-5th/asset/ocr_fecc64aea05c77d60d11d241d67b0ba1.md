```
```cpp
baseClass::baseClass(string s, int a)
{
    str = s;
    x = a;
}
```
```

```
```cpp
void derivedClass::print() const
{
    cout << "Derived class: " << y << endl;
    baseClass::print();
}
```
```

```
```cpp
derivedClass::derivedClass(string s, int a, int b)
    :baseClass("Hello Base", a + b)
{
    y = b;
}
```
```

19. Consider the following class definitions:

```
```cpp
class baseClass
{
public:
    void print() const;
    int getX() const;
    baseClass(int a = 0);

protected:
    int x;
};
```
```

```
```cpp
class derivedClass: public baseClass
{
public:
    void print() const;
    int getResult() const;
    derivedClass(int a = 0, int b = 0);

private:
    int y;
};
```
```

Suppose the definitions of the member functions of these classes are as follows:

```
```cpp
void baseClass::print() const
{
    cout << "In base: x = " << x << endl;
}
```
```

```
```cpp
baseClass::baseClass(int a)
{
    x = a;
}
```
```