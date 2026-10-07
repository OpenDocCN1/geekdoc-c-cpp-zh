Here is same class using pointers:

```
class Class Plus {
private:
    int i;
public:
    Plus(int x = 0) { i = x; }
    Plus operator+(Plus *arg) { return Plus(i + arg->i); }
    void print(char *msg) { cout << msg << endl; }
};
int main() {
    Plus a(13), b(34);
    Plus c;
    c = a + &b;
    return 0;
}
```

The program works but the syntax:

```
a + &b
```

is confusing to say the least! As a last ditch, you could attempt to make the syntax homogeneous:

```
&a + &b
```

This won't work with a member function so you might think it could work with a friend operator+() function instead of a member function. But it doesn't! The C++ compiler must have some way of determining that you want to call the operator+() for a particular class. If you say, &a + &b, the compiler's best guess is that you are adding two pointers!