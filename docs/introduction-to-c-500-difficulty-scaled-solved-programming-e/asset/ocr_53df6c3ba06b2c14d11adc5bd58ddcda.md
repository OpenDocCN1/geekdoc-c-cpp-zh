When c is destroyed, the destructors are called in reverse order, that is, first of C, then that of B, and last of A. Here is a more difficult example. Consider the following inheritance scheme, where each class contains the default constructor and destructor. In what order will they be called?

```
class A {...};
class B {......};
class C : public B, public A {......};
class D {......};
class E : public D {......};
class F : public E {......};
class G : public F, public C {{{...};
```

```
int main() {
  G g;
  ...
}
```

The construction order of the sub-objects is D, E, F, B, A, C, G. When g is destroyed, the destructors of the sub-objects are called in reverse order.

# Creation of Multiple Base Objects

If in the class hierarchy more than one path exists between a base class and a derived class, multiple objects of the base class are created and, therefore, multiple copies of its members. This may not be desirable. Can we avoid it? We'll answer it later, at first, consider the following program:

```
#include <iostream> // Example 21.5
using std::cout;
```

```
class A {
private:
  int r;
public:
  A(int k) : r(k) { cout << " A()"; };
  virtual ~A() { cout << " ~A()"; };
  void show_A() const { cout << " A:" << r; }
};
```

```
class B : public A {
private:
  int t;
public:
  B(int m) : A(m), t(m) { cout << " B()"; };
  ~B() { cout << " ~B()"; };
  void show_B() const;
};
```

```
void B::show_B() const {
  cout << " B:" << t;
  show_A();
}
```