```
Vector(Vector&&); // move constructor
Vector& operator=(Vector&&); // move assignment
// ... 
private:
int sz;
double* p;
};

Vector f(int ss)
{
Vector vs(ss);
// ... 
return v; // use move constructor
}
```

By default (that is, unless you define a copy constructor and a copy assignment), the compiler will generate move operations for you. The default meaning of move is memberwise move; see also $18.3.4.

# A.12.4 Derived classes

A class can be defined as derived from other classes, in which case it inherits the members of the classes from which it is derived (its base classes):

```
struct B {
int mb;
void fb() {};
};

class D : B {
int md;
void fd();
};
```

Here B has two members, mb and fb(), whereas D has four members, mb, fb(), md, and fd().

Like members, bases can be public or private:

```
class DD : public B1, private B2 {
// ...
};
```

So, the public members of B1 become public members of DD, whereas the public members of B2 become private members of DD. A derived class has no special