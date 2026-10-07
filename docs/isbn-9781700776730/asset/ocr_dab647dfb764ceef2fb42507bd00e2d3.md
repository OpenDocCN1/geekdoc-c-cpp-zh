# Virtual Function Mechanism

It is easier to understand how the compiler locates virtual functions at runtime considering the data structures involved and the memory layout used with class objects using virtual functions. Let's do an experiment and look at the sizes of some objects:

```
class Alpha {
private:
    int i;
public:
    void foo() {}
    void faa() {}
};

class Beta {
private:
    int i;
public:
    virtual void foo() {}
    void faa() {}
};

class Gamma {
private:
    int i;
public:
    virtual void foo() {}
    virtual void faa() {}
};

int main() {
    Alpha a;
    Beta b;
    Gamma g;

    cout << sizeof(Alpha) << endl; // 4
    cout << sizeof(Beta) << endl; // 8
    cout << sizeof(Gamma) << endl; // 8

    cout << sizeof(a) << endl; // 4
    cout << sizeof(b) << endl; // 8
    cout << sizeof(g) << endl; // 8

    void *voidPointer;
    cout << sizeof(voidPointer); // 4
    return 0;
}
```