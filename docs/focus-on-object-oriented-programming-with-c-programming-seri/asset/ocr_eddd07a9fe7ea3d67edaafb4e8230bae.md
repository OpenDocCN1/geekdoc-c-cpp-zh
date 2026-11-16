```
void foo(char* gptr) {
    pptr = "Hello C++";
}
output:
ptr = Hello C++
```

# Why References Are Essential

Let's look at this class that uses an overloaded addition operator:

```
class Plus {
    private:
        int i;
    public:
        Plus(int x = 0) { i = x; }
        Plus operator+(Plus arg) { return Plus(i + arg.i); }
        void print(char *msg) { cout << msg << endl;
    }
};

int main() {
    Plus a(13), b(34);
    Plus c;
    c = a + b;
    ...
    return 0;
}
```

The operator+() takes a single argument, which is the value to the right of the + sign. Note that the function is invoked for object on the left of the + sign.

The operator+() function creates a new Plus object by calling the Plus constructor. The argument to the Plus constructor is the sum of the private data parts of the two objects. The Plus constructor creates a new (temporary) Plus object which is copied out of the function as the return value of the operator. Note that all objects are passed and returned by value!

However, there are many occasions when you need to pass the address of an object. For example, objects may be too large to pass by value without destroying the efficiency of the program.