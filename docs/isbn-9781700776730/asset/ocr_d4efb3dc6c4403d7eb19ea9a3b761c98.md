```
class Derived : public Base {
private:
    char *upper;
public:
    Derived(char *s) : Base(s) {
        upper = new char[strlen(s) + 1];
        strcpy(upper, touprpr(s));
    }
    ~Derived() {
        delete [] upper;
    }
    char *getUpper() {
        return upper;
    }
};
```

```
int main() {
    Derived d("Haley Laurel");

    cout << d.getStr() << endl;
    cout << d.getUpper() << endl;
    return 0;
}
```

output:
Haley Laurel
HALALY LAUREL

Note that the Derived constructor calls the Base constructor, which copies the string addressed by s to the heap. The Derived class constructor makes another copy of the string, and converts its characters to upper case, and assigns to uppercase the address of the copied string. If you create an object of type Derived, you create two copies of a string, one changed and one in uppercase.

A Derived class object must carefully delete any memory that it allocates. When the object goes out of scope, its destructor must delete this memory and return it to the heap for reuse. The Base class destructor must also delete the memory addressed by buf.

Unlike destruct, a destructor in a derived class does not explicitly call the base class destructor. C++ calls destructors automatically when objects of a class goes out of scope. When Derived object goes out of scope, C++ first calls the Derived class destructor, and then calls the Base class destructor. Note that the two strings are deleted in the reverse order in which they were constructed.

Focus on Object-Oriented Programming with C++