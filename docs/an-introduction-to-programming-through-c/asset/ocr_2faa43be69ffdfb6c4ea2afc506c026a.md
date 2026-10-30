member function f of A which refers to m. Now, the code in B can refer to f, and hence it will indirectly refer to m.

# Case 3: m is a “protected” member of A:

The notion of protected is as follows. If a member of a class A is designated as protected then it can be accessed only inside the definition of A or of its subclasses. In other words, a protected member is less accessible than a public member (which is accessible everywhere), and more accessible than a private member, (which is accessible only in the definition of A). Note that m is to be considered a protected member of B as well.

We illustrate the above rules using the following code snippet.

```
class A{
private:
    int p;
protected:
    int q;
    int getp(){return p;}
public:
    int r;
    void init(){p=1; q=2; r=3;}
};

class B: public A{
    double s;
public:
    void print(){
        cout << p << endl;  // compiler error 1.  p is private.
        cout << q << ", "
             << r << ", "
             << getp() << endl;
    }
};

int main(){
    B b;
    b.init();
    cout << b.p        // compiler error 2.  p is private
         << b.q        // compiler error 3.  q is protected
         << b.r
         << b.getp()   // compiler error 4.  getp is protected.
         << endl;
    b.print();
}
```

If you compile this code, you will get the 4 compiler errors as marked. Compiler errors 1 and 2 are because p is private in A, and can hence not be accessed in the definition of B,