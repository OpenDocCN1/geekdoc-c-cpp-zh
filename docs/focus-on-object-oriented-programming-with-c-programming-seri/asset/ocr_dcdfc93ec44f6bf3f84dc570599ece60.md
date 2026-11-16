Class constructors are often overloaded to accommodate different formats of class object initialization:

```
class Name {
    private:
        char first[80];
        char middle[80];
        char last[80];
    public:
        Name() { first[0] = middle[0] = last[0] = '\0'; }
        Name(char*, char*, char*);
};
```

A constant member function can be overloaded with a non-const instance that defines the same function arguments:

```
class Screen {
    public:
        char get(int x, int y);
        char get(int x, int y) const;
};
```

In this case, the constness of the class object determines which of the functions is involved:

```
int main() {
    const Screen sc;
    Screen s;
    char ch = sc.get(0, 0); // const member
    ch = s.get(0, 0); // non-const member
}
```